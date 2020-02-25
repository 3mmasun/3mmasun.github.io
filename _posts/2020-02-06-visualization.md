---
layout: post
title: "Visualization"
date: 2020-02-06 16:00:00 +0800
tags: [machine-learning, data-science]
# img: "/assets/img/machine.jpg"
# description:
---

### Installation

The code below require **matplotlib** and **seaborn** library to be installed

```bash
# activate python environment 'guild'
pyenv activate guild
# install matplotlib and seaborn in the 'guild' environment
pip3 install matplotlib seaborn
 # start up jupyter in the same shell
jupyter notebook
```

## What are the different charts
A reference taken from Kaggle

![different charts](https://i.imgur.com/2VmgDnF.png)

### To visualize relationships:
- sns.pairplot
- sns.heatmap(df.corr())
- sns.scatterplot
- sns.barplot

### To visualize distribution:
- sns.jointplot
- sns.scatterplot with alpha to show density
- sns.distplot
- sns.kdeplot

### To visualize trends:
- sns.swarmplot
- sns.regplot
- sns.lmplot

### Cheatsheet

```python
import matplotlib.pyplot as plt
import seaborn as sns

#style
plt.style.available
plt.style.use('Solarize_Light2')

#plot
fig, ax = plt.subplots(1)
ax.plot(neg_pos, neg_square, linestyle='dotted', color='red', label='Power of 2')
ax.set_xlabel('x')
ax.set_ylabel('^2')
ax.set_xlim(-120, 120)
ax.set_ylim(-1000, 12000)
ax.set_title('Power chart')
plt.grid(True)
ax.legend(loc='center')
ax.annotate('power of 50', xy=(50,2500), xytext=(75, 2500),
           arrowprops=dict(arrowstyle='->'))
plt.show()

# scatter plot
plt.style.use('seaborn-darkgrid')
fig,ax = plt.subplots(1,figsize=(10,10))
plt.scatter(boston['RM'], boston['MEDV'])
ax.set_xlabel('Room')
ax.set_ylabel('Median Value')
ax.set_title('Housing Prices in Boston')
plt.show()

# bar chart vertical
fig,ax = plt.subplots(figsize=(20,15))
ax.bar(sg_desc['Area Name'], sg_desc['Population'])
plt.xticks(sg_desc['Area Name'], rotation='vertical', size='18')
plt.yticks(size='18')
ax.set_xlabel('Area Name')
ax.set_ylabel('Population')
ax.set_title('Region by population')
plt.show()

# bar chart horizontal
fig,ax = plt.subplots(figsize=(20,15))
ax.barh(sg_desc['Area Name'], sg_desc['Population'])
plt.xticks(size='18')
plt.yticks(size='15')
ax.set_ylabel('Area Name')
ax.set_xlabel('Population')
ax.set_title('Region by population')
plt.show()

# pie chart
plt.style.use('seaborn-whitegrid')
top10 = sg_desc.head(10)
region_pie,population_pie=top10['Area Name'],top10['Population']
fig, ax=plt.subplots(1,1, figsize=(11,11))
plt.pie(population_pie, labels=region_pie, autopct='%1.1f%%', textprops=dict(size="15"))
plt.title('Top 10 populated regions')
plt.show()

# seaborn barplot
fig, ax=plt.subplots(figsize=(15,10))
sns.barplot(x='Area Name', y='Population', hue='Gender', data=sg_pop)
plt.show()

# histogram
fig, ax = plt.subplots(1, figsize=(8,6))
plt.xlabel('Population')
plt.ylabel('Number of Areas')
plt.grid(False)
sns.distplot(sg['Population'], bins=10, hist=True, kde=False, hist_kws={'edgecolor':'black'})
plt.show()

# box plot
fig,ax = plt.subplots(figsize=(10,8))
plt.style.use('fivethirtyeight')
boxplot=sg.boxplot(column=['No Religion', 'Buddhism', 'Taoism', 'Islam', 'Hinduism', 'Catholic', 'Other Christians'], figsize=(10,10))
```
