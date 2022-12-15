# Basic-Python-Encoding-Scaling-Loop-Dataframe
Basic Python: Encoding ,Scaling, Loop, Dataframe
<h2 > <mark style="color:blue;"> Basic Python: Encoding, Scaling, Loop, Dataframe </mark></h2>

<h3 > <mark style="color:blue;">1. Import Library </mark></h3>
- https://docs.python.org/3/library/index.html

<p><mark>1.1 Pandas</br></mark>
This is one of the open-source Python libraries which is mainly used in Data Science and machine learning subjects. This library mainly provides data manipulation and analysis tool, which are used for analyzing data using its powerful data structures for manipulating numerical tables and time series analysis.</p>

<p><mark>1.2 Numpy</br></mark>
In Python, NumPy is another library that is used for mathematical functions. The NumPy library is popular for array and matrix processing using a set of mathematical functions.  This library is mostly used in machine learning computations.</p>

import pandas as pd
import numpy as np

<h3 > <mark style="color:blue;">2. Encoding Techniques</mark></h3>

- <p> In this section, You will learn about several encoding techniques, which are strategies for dealing with categorical data in a dataset. The majority of machine learning algorithms only work with numerical data since they use mathematical approaches to conduct operations on the data. It is crucial to transform category data, which is often in string form, into numerical data since many machine learning algorithms only take numerical values.</strong></p>

![image.png](attachment:image.png)

df = pd.read_csv('mall_customers.csv') # Read CSV file in dataframe

df.head() #view data

df.shape # view data size (200,5) means: 200 rows and 5 column

df.info() # view info, like datatypes record size and nullable or not

df1=df.copy() # make df1 from coping df dataframe

df2=df.copy()

<h4 > <mark style="color:blue;">2.1 Label Encoding</mark></h4>

# https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html
from sklearn.preprocessing import LabelEncoder
le = LabelEncoder()

df.columns 

import warnings 
warnings.filterwarnings('ignore')  # for ignore unnecessary Warnings

from pandas.core.dtypes.common import is_numeric_dtype

for col in df.columns:
    if is_numeric_dtype(df[col]): # if datatypes of collumn are numerical , it will continue, otherwise encode.
        continue
    else:
        df1[col] = le.fit_transform(df1[col])


df1.head()

- <p> Here Gender column has two value: <b>Male, Famale</b>. For Label Encoding, it will short by alphabate of values first letter, like :<b> F,M </b>.</br>
- Each category in label encoding is given a value between 0 and n, where n is the number of categories in the column.</p>

df1.info()

df2.head()

<h3 > <mark style="color:blue;">3. Scaling Techniques</mark></h3>

![image-4.png](attachment:image-4.png)

<mark> 3.1 Absolute Maximum Scaling</mark> </br>
<mark> 3.2 Min-Max Scaling</mark></br>
<mark> 3.3 Normalization</mark></br>
<mark> 3.4 Standardization</mark></br>
<mark> 3.5 Robust Scaling </mark>

<h4 > <mark style="color:blue;">3.2 MinMaxScaler</mark></h4>

![image.png](attachment:image.png)

When using min-max, you must first take the dataset's minimum value out of the total set of values before dividing that result by the dataset's range (maximum-minimum). In this example, as opposed to the last one, when it was between -1 and +1, your dataset will always fall between 0 and 1. Once more, this method is susceptible to outliers.

from sklearn.preprocessing import MinMaxScaler
mmscaler=MinMaxScaler()

df2['Annual Income (k$)']=mmscaler.fit_transform(df2[['Annual Income (k$)']])

df2['Spending Score (1-100)']=mmscaler.fit_transform(df2[['Spending Score (1-100)']])

df2.head()

df3=df.copy()

df3.head()

<h5> <mark>We Can also use loop for this purpose </mark></h5>

from sklearn.preprocessing import MinMaxScaler
mmscaler=MinMaxScaler()

from pandas.core.dtypes.common import is_string_dtype

for coll in df3.columns[1:]: #df3.columns[1:] for except customerID column
    if is_string_dtype(df3[coll]):
        continue
    else:
        df3[coll] = mmscaler.fit_transform(df3[[coll]])

df3.head()

df4=df.copy() # copy df Dataset as df4

df4.head()

<h3 > <mark style="color:blue;">4. Lets try to seperate string and numerical column from Dataframe</mark></h3>

![image-3.png](attachment:image-3.png)

Pandas DataFrame is a two-dimensional, size-mutable tabular data format with named axes (rows and columns). A data frame is a two-dimensional data structure in which data is organized in rows and columns in a tabular form. Pandas DataFrame is made up of three major components: data, rows, and columns.

# Seperate String Column
str_colls=[]
for coll in df4.columns:
    if is_numeric_dtype(df4[coll]):
        continue
    else:
        str_colls.append(coll)

str_colls

# Seperate Numerical Column
num_colls=[]
for coll in df4.columns:
    if is_string_dtype(df4[coll]):
        continue
    else:
        num_colls.append(coll)

num_colls

<h4 > <mark style="color:blue;">4.1 Lets Try to add new column in Dataframe df4</mark></h4>

 - Create an Custome column named profession

profession=['Doctor','Engineer','Sweeper','Driver','Business'] # create a list

profession

import random
professions=[]
for i in range(40):
    # we need 200 data for dataframe, because our existing dataframe has 200 data
    # get random value from list to make 200 data (here 5 data has in profession list. so, 5*40=200 data)
    for j in profession:
        professions.append(random.sample(profession,1))

professions

profession=pd.DataFrame(professions,columns=['Profession']) # make an dataframe

profession

df4['Profession']=profession # add Profession in df4 dataframe

df4.head()

df4.to_csv('mall_customers1.csv')

df_mall_customers = pd.read_csv('mall_customers1.csv')

df_mall_customers.head()

- Let check above dataframe, there added another column autometically,that is 'Unnamed'

##### So, we need to follow as following step for this purpose. Like, index=False

df4.to_csv('mall_customers2.csv',index=False)

df_mall_customers2 = pd.read_csv('mall_customers2.csv')

df_mall_customers2.head(10)

df_mall_customers2.head(10).T

df_mall_customers2.info() # check datatype of dataframe

