---
toc: true
layout: post
description: The Benefit and Otherwise of Using Scikit-learn For  Data Preprocessing.
categories: [markdown]
title: "Data Preprocessing:Pandas Vs Scikit-Learn"
---
![](/images/pipeline.jpg "Data Pipeline")

## Introduction

> When I was a child, I talked like a child, I thought like a child, I reasoned like a child. When I became a man, I set aside childish ways - 1 Corinthians 13:11

In a previous post, I posited that a key aspect of Data Science is the Data Science Process Life Circle. Essentially, DSLC is a bunch of activities and processes which underpinned the Data Science process. Some of the procedure which makes up the Data Science Process Life Circle are:

-  Obtain
- Scrub
- Explore
- Model
- Interpret

Given the topic of this post our discussion shall revolve around just two out of the above five procedures: *Scrub* and *Model*
Data scrubbing and Model Building are like siamese twins; the output of the former serves as the input for the latter.  In this relationship, the relevance of the Data preprocessing stage can not be overemphasized in the subsequent activity of Model Building.
As a matter of fact, the majority of Data Science practitioners holds the view that data preprocessing has a strong relationship with the model's performance.

Therefore today's post is centred around the tools for data preprocessing, their advantages and disadvantages, especially given model performance.

## Typical Data Preprocessing Activities
 I sensed some of us might be curious as to 'what are typical examples of this data preprocessing' stage. I'm happy to address such and similar curiosity.
 Data preprocessing is any activity or procedure carried out on a dataset necessary for building a model. Examples of typical data preprocessing activities are:

 - Detecting and handling missing values
 - Detecting and handling outliers
 - Creating new features from existing once
 - Drop existing features
 - transforming categorical features
 - transforming numerical features  e.t.c.

## Tools for Data Preprocessing
The above-listed activities of data preprocessing can be carried out with the aid of two broad tools or modules: Pandas Preprocessing and Scikit-learn Preprocessing.

### Preprocessing with Pandas
Pandas is one of the critical tools for data science in general. Its creation without missing words moved data science as a profession forward.
As a matter of fact, my mentor who introduced me to the beautiful world of data Science believed all preprocessing procedures in machine learning must be carried out with pandas. This view though not totally correct made be embraced and believed pandas as the sole data preprocessing tool. However, you could summit that I had a narrow perspective concerning data preprocessing. Still, I'm thankful for such short-sightedness as it allowed me to deepen my knowledge and understanding of Pandas.
some of the popular pandas methods and functions for data preprocessingg are as follows:

- `get_dummies()`
-  `fillna()`
- `replace()`
- `ffill()`
- `bfill()` e.t.c.

A major drawback in using pandas for data preprocessing is data leakage. Thus with pandas, the chance for data leakage is higher when pandas are used for data preprocessing. This is possible because pandas don't have the capability to preprocess and learn in one breathe like scikit-learn.

### Preprocessing with Scikit-learn
Scikit-learn is a python package which houses the algorithms with which models are built. Scikit-learn module is principally used for performing machine learning and model building. However, I recently came across a blogpost which brought to my awareness the advantages of doing data preprocessing in scikit-learn as against pandas. In that blog post, the author argued that when you use scikit-learn to preprocess data:

1. You can cross-validate the entire workflow
2. You can grid search model and preprocess hyperparameters
3. Avoids adding new columns to the source DataFrame
4. Pandas lacks separate fit/transform steps to prevent data leakage.

Since I encountered scikit-learn for preprocessing, I can categorically state that not only has my workflow become more simplified my model performance has also improved tremendously.


## Demonstrate scikit-learn for Data Preprocessing and model Building

### Import necessary modules and packages
```python
# import necessary package and classes
import pandas as pd
from sklearn.preprocessing import OneHotEncoder
from sklearn.impute import SimpleImputer
from sklearn.linear_model import LogisticRegression
from sklearn.compose import make_column_transformer
from sklearn.pipeline import make_pipeline
```
### Load the Dataset and select rows and columns
```python
# load dataset
df = pd.read_csv('http://bit.ly/kaggletrain', nrows=6)
cols = ['Embarked', 'Sex', 'Age', 'Fare']
X = df[cols]
```

### Initialize classes
```python
ohe = OneHotEncoder() #endcode 1 and 0 in place of categorical values
imp = SimpleImputer() #replace missing values with mean
clf = LogisticRegression() # our choice of algorithm for the model
```

### Preprocess and Fit Model

```python
ct = make_column_transformer(
     (ohe, ['Embarked', 'Sex']),
     (imp, ['Age']),
     remainder='passthrough')# ignore other columns while you preprocess the specified features/columns
     )

```

### Set step in to Pipeline

```python
pipe = make_pipeline(ct, clf)
```

From the above snippet of code, we can see that we could carry out some preprocessing activities like replacement of missing values, dummy creation e.t.c in one fell swoop under one function:make_column_transformer

## Conclusion
Machine learning tends to be complicated and complex very quickly. So it behoves the data science practitioner to avail himself of the right tools to reduce as much as a possible unnecessary complication. In the course of this post, we have discourse, demonstrated and drew our attention to the advantages of using python's scikit-learn package for data preprocessing against python's Pandas.
I hope you have learned something today. Bye!
