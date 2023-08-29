# Ex02-Outlier

# AIM
You are given bhp.csv which contains property prices in the city of banglore, India. You need to examine price_per_sqft column and do following,

(1) Remove outliers using IQR

(2) After removing outliers in step 1, you get a new dataframe.

(3) use zscore of 3 to remove outliers. This is quite similar to IQR and you will get exact same result

(4) for the data set height_weight.csv find the following

(i) Using IQR detect weight outliers and print them

(ii) Using IQR, detect height outliers and print them

# ALGORITHM

# STEP 1:Read the given Data.

# STEP 2:Get the information about the data.

# STEP 3:Detect the Outliers using IQR method and Z score.

# STEP 4:Remove the outliers:

# STEP 5:Plot the datas using box plot.

# PROGRAM

```python

import pandas as pd
df=pd.read_csv("/content/bhp.csv")
df.head()
df.describe()
df.info()
df.shape

import seaborn as sns
sns.boxplot(x="price_per_sqft",data=df)

### removing ouliers of bhp.csv file using IQR
Q1=df['price_per_sqft'].quantile(0.25)
Q3=df['price_per_sqft'].quantile(0.75)
IQR=Q3-Q1
lower=Q1-1.5*IQR
upper=Q3+1.5*IQR
newdata=df[(df['price_per_sqft']>=lower) & (df['price_per_sqft']<=upper)] 
print(newdata)   #new dataframe.
outliers=df[(df['price_per_sqft']<lower) | (df['price_per_sqft']>upper)]
print(outliers)
newdata.shape
sns.boxplot(x="price_per_sqft",data=newdata)


### removing ouliers of bhp.csv file using Zscore of 3

from scipy import stats
import numpy as np
z_score=np.abs(stats.zscore(df['price_per_sqft']))
newdata2=df[(z_score<3)]
print(newdata2)
outlier2=df[(z_score>=3)]
print(outlier2)
newdata2.shape
sns.boxplot(x="price_per_sqft",data=newdata2)

import pandas as pd
dataset=pd.read_csv("/content/height_weight.csv")
dataset.shape
dataset.describe()
dataset.info()
import seaborn as sns
sns.boxplot(x='height',data=dataset)

### Using IQR detect height outliers and print them( height_weight.csv)

Q1_height=dataset['height'].quantile(0.25)
Q3_height=dataset['height'].quantile(0.75)
IQR_HEIGHT=Q3_height-Q1_height
l_height=Q1_height-1.5*IQR_HEIGHT
u_height=Q3_height+1.5*IQR_HEIGHT
outliers_height=dataset[(dataset['height']<l_height) | (dataset['height']>u_height)]
print(outliers_height)
newdata_height=dataset[(dataset['height']>=l_height) & (dataset['height']<=u_height)]
print(newdata_height)
sns.boxplot(x='height',data=newdata_height)


### Using IQR, detect weight outliers and print them( height_weight.csv)

Q1_weight=dataset['weight'].quantile(0.25)
Q3_weight=dataset['weight'].quantile(0.75)
IQR_WEIGHT=Q3_weight-Q1_weight
l_weight=Q1_weight-1.5*IQR_WEIGHT
u_weight=Q3_weight+1.5*IQR_WEIGHT
outliers_weight=dataset[(dataset['weight']<l_weight) | (dataset['weight']>u_weight)]
print(outliers_weight)
newdata_weight=dataset[(dataset['weight']>=l_weight) & (dataset['weight']<=u_weight)]
print(newdata_weight)
sns.boxplot(x='weight',data=newdata_weight)
```

# OUTPUT

# bhp.csv

```python
df.head()
```
![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/46ff061b-f277-4429-a77d-ad6a12052f16)

```python
df.describe()
```
![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/a7c8242c-959d-45a5-a0b3-f1a08ac0aec7)

```python
df.info()
```
![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/e075b836-a6be-4154-83a4-2faf0e586903)

```python
df.shape
```
![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/6da5287e-1b02-4171-be42-4222f1d53c04)

# BOXPLOT BEFORE REMOVING OUTLIERS

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/031bb65d-2e75-4657-abf9-8f4ab0f5ce9d)

# NEW DATA USING IQR

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/007e71e5-3960-4b6b-beba-45496fc8bf33)

# OUTLIERS

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/ec62f525-214d-4f04-8bc9-8e35f3210ac9)

```PYTHON
newdata.shape
```
![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/a13cc6df-b298-4f64-b176-040a5ef60455)

# BOXPLOT AFTER REMOVING OUTLIERS USING IQR

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/1dc978f6-d136-46f9-b129-6da4ff24f87f)

# ZSCORE OF 3

# NEWDATA USING ZSCORE

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/2312b8e7-58f6-4ea6-8489-889678233ebe)

# OUTLIERS

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/022b795c-2317-466a-9531-f20a1686ab20)

```PYTHON
newdata2.shape
```

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/93f0565b-c593-4f18-ab6d-5d6da50a2b55)

# BOXPLOT AFTER REMOVING OUTLIERS USING ZSCORE

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/f6d905d9-23eb-4874-bfd4-dd43d2b60722)

# height_weight.csv

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/7a6ad63d-f945-4bc0-9cdd-d9688ca3bb49)

```python
dataset.describe()
```

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/4e972165-0a04-40d6-8e4a-37f390b2737b)

```python
dataset.info()
```

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/c394ddda-c278-4225-8269-7169dad94bf9)

# BOXPLOT BEFORE REMOVING OUTLIERS

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/77903a42-a43b-4450-95e5-ac3a8e8414c4)

# HEIGHT OUTLIERS

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/4e38da2d-71f9-490c-b71b-f4a9c3ab4eba)

# DATASET AFTER REMOVING HEIGHT OUTLIERS

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/7d8c6621-4fdb-48cf-9603-d7586622adf0)

# BOXPLOT AFTER REMOVING HEIGHT OUTLIERS

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/883194c5-c898-4a07-a041-e8be56956824)

# WEIGHT OUTLIERS

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/77f87270-5e66-4e93-a4af-0ab3655398bb)

# DATASET AFTER REMOVING WEIGHT OUTLIERS

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/f2c97d88-d462-480c-aa9e-6c7c82015845)

# BOXPLOT AFTER REMOVING WEIGHT OUTLIERS

![image](https://github.com/Sachin-vlr/ODD2023---Datascience---Ex-02/assets/113497666/56610523-3cb3-4ee3-ab8f-5283f756b841)

# RESULT:
The given datasets are read and outliers are detected and are removed using IQR and z-score methods.

