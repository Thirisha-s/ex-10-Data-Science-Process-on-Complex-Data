# ex-10-Data-Science-Process-on-Complex-Data
# AIM:
To Perform Data Science Process on a complex dataset and save the data to a file.

# ALGORITHM
# STEP 1 :
Read the given Data

# STEP 2 :
Clean the Data Set using Data Cleaning Process

# STEP 3 :
Apply Feature Generation/Feature Selection Techniques on the data set

# STEP 4 :
Apply EDA /Data visualization techniques to all the features of the data set

# CODE:
Developed by: THIRISHA.s
Register No: 212222230160
```
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
data=pd.read_csv("/content/StudentsPerformance - StudentsPerformance.csv.csv")
print(data)
data.info()
data.isnull().sum()
# data cleaning

data['test preparation course']=data['test preparation course'].fillna(data['test preparation course'].mode()[0])

data['math score']=data['math score'].fillna(data['math score']).fillna(data['math score'].mean())

data['writing score']=data['writing score'].fillna(data['writing score']).fillna(data['reading score'].median())

data.isnull().sum()

data.describe()

data.head()
removing outliers
Q1=data['math score'].quantile(0.25)

Q3=data['math score'].quantile(0.75)

IQR=Q3-Q1

lower=Q1-1.5*IQR

upper=Q3+1.5*IQR

df=data[(data['math score']>=lower) & (data['math score']<=upper)] 
print(df) 


outliers=data[(data['math score']<lower) | (data['math score']>upper)] 
print(outliers)

df.shape
Feature generation
from sklearn.preprocessing import OrdinalEncoder,LabelEncoder
df1=df.copy()
r=['group A','group B','group C','group D','group E']
enc=OrdinalEncoder(categories=[r])
enc.fit_transform(df1[['race/ethnicity']])
df1['neword1']=enc.fit_transform(df1[['race/ethnicity']])
df1 
df2=df1.copy()
le=LabelEncoder()
df2['neword2']=le.fit_transform(df2['race/ethnicity'])
df2
from sklearn.preprocessing import OneHotEncoder
df3=df.copy()
ohe=OneHotEncoder(sparse=False)
enc=pd.DataFrame(ohe.fit_transform(df3[['lunch']]))
df3=pd.concat([df3,enc],axis=1)
df3.head()
!pip install --upgrade category_encoders
from category_encoders import BinaryEncoder
be=BinaryEncoder()
df4=df.copy()
newdata=be.fit_transform(df4['test preparation course'])
df4=pd.concat([df,newdata],axis=1)
df4.head()
heatmap
data.corr()
plt.subplots(figsize=(7,5))
sns.heatmap(data.corr(),annot=True)
Data visualization
Scatter plot of math score vs. reading score

plt.scatter(data['math score'], data['reading score'])
plt.xlabel('Math Score')
plt.ylabel('Reading Score')
plt.title('Math Score vs. Reading Score')
plt.show()
sns.barplot(x='gender',y='reading score',data=df)
sns.boxplot(x="math score",data=df)
```
# OUTPUT:
DATA
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/7558bd5a-cc45-4402-bbfc-ee989beb6d6f)

# data.info()
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/a96e2540-0d4d-4a87-a4c0-16411e689331)

# data.isnull.sum()
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/580a75b4-cfc6-4103-9222-e145e9726d69)

# After removing null values
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/a42326be-9ee6-40f0-a678-462947aa3c20)

# data.discribe()
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/0f19096d-f2c9-4914-a170-44374cde99d1)

# data.head()
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/5b94f863-5bd5-4a18-879b-183ccc3b2bd5)

# New data after removing outliers
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/e5533ecb-48dc-4a63-9142-dd8aa73c99b2)

# Outliers
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/44c2e154-7c45-473e-a02c-760869376ac8)

# df.shape()
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/8d79b237-81ac-4ad1-b39c-a0d2e040e3f9)

# Ordinal Encoding
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/e187420a-a27b-4715-b7a2-39c3ff5c35b9)

# Label Encoding
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/274543ee-da70-44e1-9e82-b35f0c01d671)

# OneHot Encoding
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/28c70a48-59cd-4280-bbce-1e66ef355333)

# Binary Encoding
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/b11f94b8-2afb-4a6b-b5f7-c4e5fb6debae)

# Heatmap
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/b6189111-f2ed-415c-ae22-3b30c31b601c)

# Scatterplot
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/7c7c2481-2880-46a4-90c4-1953e11b223a)

# Barplot
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/2104e98b-0444-4b4a-8ea2-6d79196eba50)

# Boxplot
![image](https://github.com/Thirisha-s/ex-10-Data-Science-Process-on-Complex-Data/assets/120380280/2584989f-ded5-44a9-b90e-9212a48ac8f4)

# RESULT:
Hence, Data Science Process is performed on a complex dataset and saved the data to a file.
