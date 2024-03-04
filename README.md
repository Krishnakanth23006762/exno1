# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
import pandas as pd
import numpy as np
import seaborn as sns
import os 
df=pd.read_csv("SAMPLEIDS.csv")
df
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/f69feace-4bb9-461a-b4a8-d6c7e8fc2f02)
```
df.isnull().sum()
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/682177ed-babf-4708-81e4-848eb1f865df)
```
df.isnull().any()
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/72f3d5b5-cfef-4f0e-ba28-c8de2311f935)

```
df.dropna()
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/bbf5fb0c-6dbc-4780-8650-bbdb545d07fd)

```
df.fillna(0)
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/8885fb6f-904f-445d-a818-ed48d92717ac)

```
df.fillna(method = 'ffill')
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/f64d4820-2f5a-4c74-9aa5-0cb78e4b97e1)

```
df.fillna(method = 'bfill')
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/999dd847-8717-4da3-b312-43e52cb97452)
```
df_dropped = df.dropna()
df_dropped
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/036bbc68-a392-4df6-9100-cfe9139d6bc4)
```
df.fillna({'GENDER':'FEMALE','NAME':'PRIYU','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/6d95e76b-1f74-4db1-b821-0959824f53e0)
## IQR(Inter Quartile Range)
```
import pandas as pd
ir=pd.read_csv('iris.csv')
ir
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/69f1784b-b513-42df-93b6-235e4187fb22)
```
ir.describe()
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/57db5087-81f7-4ff7-89fe-688827f1cb3d)
```
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/44d569b2-c7ba-41f1-ae06-51d28390d6f0)
```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/2b825d4e-392b-43ac-b676-fb801d1979f5)
```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/f06614a0-6812-4b48-b848-2e350d3e6492)
```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/35f04aee-260e-49f4-b29f-963628ad4a5a)
```
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/75263bdb-7e10-4a6b-8319-b1da62a9f33e)
## Z score
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("heights.csv")
dataset
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/f61ff672-64dd-4388-b053-b322a36d19df)

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/a3351300-70e0-463b-b92f-67b10512b647)
```
low = q1 - 1.5*iqr
low
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/09dc59ba-f144-4dcf-87db-ccdaf6ad7475)
```
high = q3 + 1.5*iqr
high
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/0e3ac46f-4ac1-402f-ae1e-1d9a4d0a2ae9)
```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/1babf866-8614-4e31-b6bb-dc24926cadb6)
```
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/0d5b57eb-50e5-46cd-93e2-6b1a296f9f90)
```
df1 = df[z<3]
df1
```
![image](https://github.com/Krishnakanth23006762/exno1/assets/138849446/051c65fd-3c1c-4931-877f-e18dd7b798cf)

# Result
Hence the data was cleaned , outliers were detected and removed.          
