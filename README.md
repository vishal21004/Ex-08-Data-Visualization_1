# Ex-09-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.

## PROGRAM:
Developed by:M.A.VISHAL
Register no: 212222230177
## CODE
```
# loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
```
## Removing unnecessary data variables
```
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()
```
## Detecting and removing outliers in current numeric data
```
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
## Data visualization
## Line plots
```
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
```
## Bar plots
```
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
```
## Histogram
```
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
```
## Count plot
```
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
```
## Barplot
```
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
## KDE plot
```
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
```
## Violin plot
```
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
```
## Point plot
```
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
```
## Pie Chart
```
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
````
## HeatMap
```
df4=df.copy()
encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])
scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region','Category','Sub-Category','Sales','Quantity','Discount','Profit'])
```
## Heatmap
```
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```
OUPUT

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/ed02c216-7961-4f61-9128-5270608e81d8)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/3b17fae5-8f75-43e9-9ecb-c5c1b5d4225d)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/16919d2d-122d-4c8e-9e14-8ce7eb2deb52)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/21a71adc-259c-439f-9177-81c3aae5eda0)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/7de17ee9-6f30-433c-90c1-20a3b378eccf)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/b45e2071-24c1-4e80-a132-23c01a7c0837)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/5d5c9319-8d5f-4da2-8fea-15628a561470)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/eb597b95-7c2e-41aa-9b06-d6a3bf7e1fb1)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/e131cc7c-6f55-46e1-93d8-64b7a7ae53cb)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/abbed1d1-f7d9-4255-bbb8-9f1b875b059a)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/586ec335-46b6-4237-b9c5-604555e33521)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/b66469df-3497-4f2c-8ce7-c236b940b2ec)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/21360478-984f-4a4a-970f-3ca3bac27e80)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/9f6c5b17-e34f-4d8b-8328-fb7812f2f705)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/80468219-1704-4535-b980-de2851a8d74b)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/a69f1e1c-ec04-4e64-bbb9-3f297ea1abb0)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/4dd7ca63-db56-4c87-857e-ef79a6d5ab4b)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/49615eee-0cea-4981-b583-1df0d01ee139)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/ca0af906-2f50-4928-8679-5ff6e346e17e)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/1fa34e6e-655f-4d2f-a216-418972a05035)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/f1b6d166-5eed-4362-a6f6-b56cbeecb1fb)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/36c851ad-b1d2-4e48-8e92-6a5442cef6e7)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/f3315e80-34f1-4e78-bbf3-6c1b97f8383b)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/804b1b5d-c32d-43ef-af3f-51ab991bf911)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/a4a07738-a4dc-4182-a9c0-47fd233c4162)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/13f98c53-cafb-435e-8f13-96513a21f406)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/ca13078f-b5c0-4592-b3bd-bc472f1cf1ee)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/3ac034ad-1acd-4935-838a-e2152619cf31)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/6a59153a-7850-4edf-805a-b44ba6780d47)

![image](https://github.com/Niroshassithanathan/Ex-08-Data-Visualization_1/assets/121418437/a2d59e4b-e780-4364-99d0-98e3c9ec40b4)

## Result:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file
















