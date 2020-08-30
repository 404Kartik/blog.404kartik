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

**name**|**state**|**birthyear**
:-----:|:-----:|:-----:
0|Mary|VIC
1|David|NSW
2|Jack|VIC
3|John|SA
4|Robin|QLD
An alternative is to first define an empty data frame with column names
and then append rows to it as dictionaries whose keys are the columns.

In [5]:

    df = pd.DataFrame(columns=['name', 'state', 'birthyear'])
    df = df.append({'name': 'Mary', 'state': 'VIC', 'birthyear': 1980}, ignore_index=True)
    df = df.append({'name': 'David', 'state': 'NSW', 'birthyear': 1992}, ignore_index=True)
    # etc.
    df

Out[5]:
**name**|**state**|**birthyear**
:-----:|:-----:|:-----:
0|Mary|VIC
1|David|NSW

A second alternative, which is a bit shorter, is to append rows as lists
at the end of the data frame.

In [6]:

    df = pd.DataFrame(columns=['name', 'state', 'birthyear'])
    df.loc[len(df)] = ['Mary', 'VIC', 1980]
    df.loc[len(df)] = ['David', 'NSW', 1992]
    # etc.
    df

Out[6]:

**name**|**state**|**birthyear**
:-----:|:-----:|:-----:
0|Mary|VIC
1|David|NSW

This tutorial will mostly focus on data frames, since real-world
datasets are generally multi-dimensional tables rather than just one
dimensional arrays.

Loading Data: Course Grades[¶](https://www.featureranking.com/tutorials/python-tutorials/pandas/#Loading-Data:-Course-Grades) {#Loading-Data:-Course-Grades}
-----------------------------------------------------------------------------------------------------------------------------

This sample data contains course assessment results and students' final
grades (Pass or Fail) for a class with 40 students.

-   `Student ID`: Unique ID number for each student in the data.

-   `Gender`: The gender of student.

-   `Project Phase 1`: The mark student received by completing the first
    part of project. The marks are out of 20.

-   `Project Phase 2`: The mark student received by completing the
    second part of project. The marks are out of 30.

-   `Mid-Semester Test`: The mark student received from the mid-semester
    test. The marks are out of 100.

-   `Final Exam`: The mark student received from the final exam. The
    marks are out of 100.

-   `Grade`: The grade student received indicating whether they passed
    or failed.

Now let's load the data into a DataFrame object from the Cloud.

In [7]:

    # for Mac OS users only!
    # if you run into any SSL certification issues, 
    # you may need to run the following command for a Mac OS installation.
    # $/Applications/Python 3.x/Install Certificates.command
    import os, ssl
    if (not os.environ.get('PYTHONHTTPSVERIFY', '') and
        getattr(ssl, '_create_unverified_context', None)): 
        ssl._create_default_https_context = ssl._create_unverified_context

    import io, requests
    grades_url = 'https://raw.githubusercontent.com/vaksakalli/python_tutorials/master/sample_grades.csv'
    url_content = requests.get(grades_url).content
    grades = pd.read_csv(io.StringIO(url_content.decode('utf-8')))

    # alternatively, you can download this CSV file to 
    # where this notebook is on your computer
    # and then use the read_csv() method:
    # ### grades = pd.read_csv('sample_grades.csv', header=0)

The method `head()` prints the first five rows by default.

In [8]:

    grades.head()

Out[8]:

**Student ID**|**Gender**|**Project Phase 1**|**Project Phase 2**|**Mid-Semester Test**|**Final Exam**|**Grade**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
0|101|Male|18.25|15.5|94|61.0
1|102|Female|17.75|30.0|79|62.0
2|103|Male|0.00|0.0|78|15.0
3|104|Male|20.00|25.0|69|65.0
4|105|Male|18.75|30.0|96|51.0
Alternatively, we can define the number of header rows we want to print.

In [9]:

    grades.head(2)

Out[9]:
**Student ID**|**Gender**|**Project Phase 1**|**Project Phase 2**|**Mid-Semester Test**|**Final Exam**|**Grade**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
0|101|Male|18.25|15.5|94|61.0
1|102|Female|17.75|30.0|79|62.0


`tail()` prints the last five rows by default.

In [10]:

    grades.tail()

Out[10]:

**Student ID**|**Gender**|**Project Phase 1**|**Project Phase 2**|**Mid-Semester Test**|**Final Exam**|**Grade**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
35|136|Male|18.50|22.0|26|68.0
36|137|Female|20.00|26.0|89|63.0
37|138|Male|18.75|30.0|59|52.0
38|139|Male|19.00|30.0|70|NaN
39|140|Male|20.00|29.0|84|77.0

`sample()` randomly selects rows from the entire data.

In [11]:

    grades.sample(5, random_state=99)

Out[11]:

**Student ID**|**Gender**|**Project Phase 1**|**Project Phase 2**|**Mid-Semester Test**|**Final Exam**|**Grade**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
25|126|Female|20.00|22.5|83|56.0
36|137|Female|20.00|26.0|89|63.0
29|130|Male|19.50|13.0|62|39.0
22|123|Male|19.75|30.0|74|61.0
28|129|Male|20.00|30.0|64|86.0


### Sorting[¶](https://www.featureranking.com/tutorials/python-tutorials/pandas/#Sorting) {#Sorting}

We can sort the data with respect to a particular column by calling
`sort_values()`. Let's sort the data by Final Exam scores in descending
order. If you want the sorting to be permanent, you must specifically
set the `inplace` argument to `True`. This is a **fundamental rule** in
Pandas: in most cases, if you don't set the `inplace` argument to
`True`, you will need to set the output of the command to another
variable to save its effect. Another nice feature of Pandas is **method
chaining**: notice below how we chain two methods together.

In [12]:

    grades.sort_values(by='Final Exam', ascending=False).head()

Out[12]:

**Student ID**|**Gender**|**Project Phase 1**|**Project Phase 2**|**Mid-Semester Test**|**Final Exam**|**Grade**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
27|128|Female|20.0|30.00|84|91.0
28|129|Male|20.0|30.00|64|86.0
26|127|Female|20.0|35.00|84|83.0
14|115|Male|19.5|26.00|100|79.0
13|114|Male|20.0|22.75|85|78.0

The function `shape` counts the number of rows and columns. Thus, number
of rows and columns can be obtained as `grade.shape[0]` and
`grade.shape[1]` respectively.

In [13]:

    grades.shape

Out[13]:

    (40, 7)

`info()` provides a concise summary of the columns.

In [14]:

    grades.info()

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 40 entries, 0 to 39
    Data columns (total 7 columns):
    Student ID           40 non-null int64
    Gender               37 non-null object
    Project Phase 1      40 non-null float64
    Project Phase 2      37 non-null float64
    Mid-Semester Test    40 non-null int64
    Final Exam           36 non-null float64
    Grade                40 non-null object
    dtypes: float64(3), int64(2), object(2)
    memory usage: 2.3+ KB

`describe()` generates descriptive statistics. Keep in mind that this
function excludes *null* values.

In [15]:

    grades.describe()

Out[15]:

Student ID	Project Phase 1	Project Phase 2	Mid-Semester Test	Final Exam
count	40.000000	40.000000	37.000000	40.000000	36.000000
mean	120.500000	16.987500	23.750000	72.100000	56.055556
std	11.690452	5.964626	7.509716	19.664885	20.520296
min	101.000000	0.000000	0.000000	26.000000	6.000000
25%	110.750000	17.687500	20.000000	59.750000	45.500000
50%	120.500000	19.500000	25.500000	76.000000	60.000000
75%	130.250000	20.000000	30.000000	86.000000	71.750000
max	140.000000	20.000000	35.000000	100.000000	91.000000

#To ensure all the columns are listed (including categoricals), we can
add the `include = all` parameter.

In [16]:

    grades.describe(include='all')

Out[16]:

**Student ID**|**Gender**|**Project Phase 1**|**Project Phase 2**|**Mid-Semester Test**|**Final Exam**|**Grade**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
count|40.000000|37|40.000000|37.000000|40.000000|36.000000
unique|NaN|4|NaN|NaN|NaN|NaN
top|NaN|Male|NaN|NaN|NaN|NaN
freq|NaN|22|NaN|NaN|NaN|NaN
mean|120.500000|NaN|16.987500|23.750000|72.100000|56.055556
std|11.690452|NaN|5.964626|7.509716|19.664885|20.520296
min|101.000000|NaN|0.000000|0.000000|26.000000|6.000000
25%|110.750000|NaN|17.687500|20.000000|59.750000|45.500000
50%|120.500000|NaN|19.500000|25.500000|76.000000|60.000000
75%|130.250000|NaN|20.000000|30.000000|86.000000|71.750000
max|140.000000|NaN|20.000000|35.000000|100.000000|91.000000

