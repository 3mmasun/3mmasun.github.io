---
layout: post
title: "Pandas Basics"
date: 2020-02-05 16:00:00 +0800
tags: [machine-learning, data-science, pandas]
# img: "/assets/img/machine.jpg"
# description:
---

### Installation

```bash
pyenv activate guild # guild is the environment name
pip3 install numpy pandas # install numpy and pandas in the 'guild' environment
jupyter notebook # start up jupyter
```

### cheatsheet

`transactions_df` is a Pandas Dataframe that looks like this:

| | order_id | product | quantity | price | customer_id | transaction_date |
|:------:|:------:|:------:|:------:|:------:|:------:|:------:|:
| 0 | 1 | Pasta | 43 | $11.39 | 4 | 17/6/19 |
| 1 | 2 | Lamb | 71 | $3.72 | 5 | 4/9/19 |
| 2 | 3 | Cake | 81 | $3.09 | 76 | 24/10/19 |
| 3 | 4 | Wine | 69 | $7.09 | 20 | 29/4/19 |

```python
# overview
import pandas as pd
tranx = pd.read_csv('transactions.csv')
tranx.info()
tranx.shape
tranx.head(10) # first 10 rows
tranx["price"].describe()
transactions['price'].dtype

# null
tranx.isnull()
tranx.notnull()
tranx.dropna()
tranx.dropna(subset=["price"])
tranx.fillna()
tranx.fillna(value={"price":0.0, "quantity":0})

# selecting
tranx["price"] # column 'price'
tranx.iloc[0] # first row
tranx.nlargest(2,columns=["price"])
tranx.nsmallest(2,columns=["price"])

# sorting & grouping
tranx.sort_values(["price"], ascending=False)
tranx.groupby("customer_id").sum("price")
tranx.groupby("customer_id").sum("price")

# filter row
new_df = tranx[(tranx['product']=='Honey')['price']==0.0)]

# column operations
### strip_off_dollar is a function that takes 1 parameter
tranx['price'] = tranx['price'].apply(strip_off_dollar)
tranx['total'] = tranx['price'] * tranx["quantity"]
```
