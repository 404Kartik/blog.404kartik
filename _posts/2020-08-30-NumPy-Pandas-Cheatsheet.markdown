---
layout: post
title:  "Learning NumPy and Pandas"
description: NumPy and Pandas cheatsheet
date:   2020-08-30 21:03:36 +0530
categories: NumPy Pandas Python
---


Hello everyone! Today I want to write about the Pandas library . Pandas stands for “Python Data Analysis Library”. According to the Wikipedia page on Pandas, “the name is derived from the term “panel data”, an econometrics term for multidimensional structured data sets.” But I think it’s just a cute name to a super-useful Python library!
Pandas is quite a game changer when it comes to analyzing data with Python and it is one of the most preferred and widely used tools in data munging/wrangling if not THE most used one.


In [2]:

    import pandas as pd
    import numpy as np

Series and Data Frames[¶](https://www.featureranking.com/tutorials/python-tutorials/pandas/#Series-and-Data-Frames) {#Series-and-Data-Frames}
-------------------------------------------------------------------------------------------------------------------

There are two main data structures in Pandas: `Series` and `DataFrame`.

`Series` is like a Python list: it is a one-dimensional data structure
that can store values with labels (or index). We can initialize a Series
with a list as below.

In [3]:

    x = pd.Series([34, 23, -5, 0])
    print(x)

    0    34
    1    23
    2    -5
    3     0
    dtype: int64

If you would like to see the list of methods that you can use with a
Series, use the code completion feature in Jupyter Notebook: type "x."
in a cell and then hit the Tab button.

A `DataFrame` is just a table with rows and columns, much like an Excel
spreadsheet. An easy way to create a DataFrame object is by using a
dictionary:

In [4]:

    data = {'name': ['Mary', 'David', 'Jack', 'John', 'Robin'],
            'state': ['VIC', 'NSW', 'VIC', 'SA', 'QLD'],
            'birthyear': [1980, 1992, 2000, 1980, 1995]}
    df = pd.DataFrame(data)
    df

Out[4]:

name

state

birthyear

0

Mary

VIC

1980

1

David

NSW

1992

2

Jack

VIC

2000

3

John

SA

1980

4

Robin

QLD

1995

An alternative is to first define an empty data frame with column names
and then append rows to it as dictionaries whose keys are the columns.

In [5]:

    df = pd.DataFrame(columns=['name', 'state', 'birthyear'])
    df = df.append({'name': 'Mary', 'state': 'VIC', 'birthyear': 1980}, ignore_index=True)
    df = df.append({'name': 'David', 'state': 'NSW', 'birthyear': 1992}, ignore_index=True)
    # etc.
    df

Out[5]:

name

state

birthyear

0

Mary

VIC

1980

1

David

NSW

1992

A second alternative, which is a bit shorter, is to append rows as lists
at the end of the data frame.


