---
layout: post
title: "Airbnb Barcelona Price Prediction"
date: 2020-03-15 10:00:00 +0800
tags: [machine-learning]
img: "/assets/img/barcelona.jpeg"
description: explore data cleaning and transformation
---

This post documents the steps involved training a simple model to predict the price in Airbnb Barcelona listing, covering following section:
- Data Exploring
- Transformation
- Training the model
- Encode model and upload

The repository is [here](https://github.com/3mmasun/airbnb-ml) if you would like to check the code.

[image source](https://images.unsplash.com/photo-1539037116277-4db20889f2d4?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2250&q=80)

# Data Exploring
Airbnb data can be obtained from [http://insideairbnb.com/get-the-data.html](http://insideairbnb.com/get-the-data.html)

Here we used the data from Dec 2019 for Barcelona, Spain. You can obtain a copy [here](https://github.com/3mmasun/airbnb-ml/tree/master/barcelona-12-2019)

The original data in listings.csv.gz has over 100 columns, the final data frame used for price prediction only had 43 columns including 'Price' target. Many of them were dropped because they were mostly no value, or same value, or duplicate of other columns.


## Object Columns

`cat_df = airbnb_df.select_dtypes(include=['object']).copy()`

| Column                           | Transformation                                                                        |
| -------------------------------- | ------------------------------------------------------------------------------------- |
| host_id                          | none                                                                                  |
| host_response_time               | drop_rows_occurs_less_than(1) ->fillna_with_lowest_occurance ->dic_host_response_time |
| host_is_superhost                | encode_boolean_to_float ->fillna False                                                |
| host_verifications               | extract_num_of_items_for_column                                                       |
| host_has_profile_pic             | encode_boolean_to_float ->fillna False                                                |
| host_identity_verified           | encode_boolean_to_float ->fillna False                                                |
| neighbourhood_group_cleansed     | drop_rows_occurs_less_than(1) ->encode_category_dic                                   |
| is_location_exact                | encode_boolean_to_float                                                               |
| property_type                    | encode_category_dic                                                                   |
| room_type                        | encode_category_dic                                                                   |
| bed_type                         | encode_category_dic                                                                   |
| amenities                        | extract_num_of_items_for_column                                                       |
| has_availability                 | encode_boolean_to_float                                                               |
| instant_bookable                 | encode_boolean_to_float                                                               |
| cancellation_policy              | drop_rows_occurs_less_than(2) -> encode_category_dic                                  |
| require_guest_profile_picture    | encode_boolean_to_float                                                               |
| require_guest_phone_verification | encode_boolean_to_float                                                               |

## Numeric Columns

`numeric_df = airbnb_df.select_dtypes(include=['float64', 'int32']).copy()`

| Column                                       |
| -------------------------------------------- |
| host_response_rate                           |
| latitude                                     |
| longitude                                    |
| accommodates                                 |
| bathrooms                                    |
| bedrooms                                     |
| beds                                         |
| price                                        |
| security_deposit                             |
| cleaning_fee                                 |
| guests_included                              |
| extra_people                                 |
| availability_365                             |
| number_of_reviews                            |
| review_scores_rating                         |
| review_scores_accuracy                       |
| review_scores_cleanliness                    |
| review_scores_checkin                        |
| review_scores_communication                  |
| review_scores_location                       |
| review_scores_value                          |
| calculated_host_listings_count               |
| calculated_host_listings_count_entire_homes  |
| calculated_host_listings_count_private_rooms |
| calculated_host_listings_count_shared_rooms  |
| review_per_month                             |

## Folder structure
```
airbnb-ml
  |-- src
    |-- transform.py
    |-- __init__.py
    |-- tests
      |-- test_transform.py
```

## Testing Framework
```bash
# requirements-dev.txt
nose==1.3.7
nose-watch==0.9.2
rednose==1.3.0
```

# Transformation
```python
def drop_rows_occurs_less_than(df, column_name, low_bound):
    counts = df[column_name].value_counts()
    to_remove = counts[counts <= low_bound].index
    new_df = df[~df[column_name].isin(to_remove)]
    return new_df

def fillna_with_lowest_occurance(df, column_name):
    df = df.fillna(
        value={column_name: df[column_name].value_counts().index[-1]})
    return df

def encode_boolean_to_float(df, column_name):
    df[column_name] = df[column_name].astype(float)
    return df

def extract_num_of_items_for_column(df, column_name):
    df[column_name] = df[column_name].apply(extract_num_of_items)
    return df

def extract_num_of_items(input):
    input = input.split(",")
    return len(input)
```

## Transformation: Categorical Column
Some of the columns contain categorical data, instead of one-hot encoding, I wrote a function to label them

```python
def encode_category_dic(dataframe):
    def h(dica, columnName):
        labels = dataframe[columnName].astype(
            'category').cat.categories.tolist()
        encode_dic = {columnName: {k: v for k, v in zip(
            labels, list(range(1, len(labels)+1)))}}
        return dict(dica, **encode_dic)
    return h

def foldleft(func, acc, xs):
    return functools.reduce(func, xs, acc)

# usage
category_columns = [
    "neighbourhood_group_cleansed",
    "property_type",
    "room_type",
    "bed_type",
    "cancellation_policy"
]

category_encoder = trans.encode_category_dic(airbnb)
category_dic = trans.foldleft(category_encoder, {}, category_columns)
airbnb = airbnb.replace(category_dic)
```

# Training the model
Models like SVCRegressor, LinearRegression and DecisionTree produced very bad results. R<sup>2</sup> score ranged from 0.09-0.12

In the end, **RandomForestRegressor** produced the best model, R<sup>2</sup> score ~0.8
```python
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestRegressor

y = airbnb["price"]
X = airbnb.drop(columns=['price'])
x_train, x_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
rnd_regr = RandomForestRegressor(
    min_samples_leaf=4,
    random_state=0,
    n_estimators=100)
rnd_regr.fit(x_train, y_train)
```

# Encode model and upload to S3
```python
import s3fs

with s3.open('airbnb-barcelona/models/rnd_reg.price', 'wb') as f:
    joblib.dump(rnd_regr, f)
```
