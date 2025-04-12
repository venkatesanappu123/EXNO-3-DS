## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
```
import pandas as pd
df=pd.read_csv("/content/Encoding Data.csv")
df
```
![Screenshot 2025-04-07 112846](https://github.com/user-attachments/assets/868bcd51-7221-497c-9fd5-7ca0bc8a5018)
```
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
pm=['Hot','Warm','Cold']
e1=OrdinalEncoder(categories=[pm])
e1.fit_transform(df[["ord_2"]])
```
![Screenshot 2025-04-07 112929](https://github.com/user-attachments/assets/f3ac54bd-5db3-4b85-b445-b5cb4357263f)
```
df['bo2']=e1.fit_transform(df[["ord_2"]])
df
```
![Screenshot 2025-04-07 113001](https://github.com/user-attachments/assets/1568d2f4-cc9d-4e38-8d0e-bcdf1584e97f)
```
le=LabelEncoder()
dfc=df.copy()
dfc['ord_2']=le.fit_transform(dfc['ord_2'])
dfc
```
![Screenshot 2025-04-07 113040](https://github.com/user-attachments/assets/35c9108c-6761-43b3-878b-38ecc8765c57)
```
from sklearn.preprocessing import OneHotEncoder
ohe=OneHotEncoder(sparse_output=False)
df2=df.copy()
enc=pd.DataFrame(ohe.fit_transform(df2[["nom_0"]]))
df2=pd.concat([df2,enc],axis=1)
df2
```
![Screenshot 2025-04-07 113130](https://github.com/user-attachments/assets/7805d318-3bf4-401c-91f1-c1f09fcb5723)
```
pd.get_dummies(df2,columns=["nom_0"])
```
![Screenshot 2025-04-07 113208](https://github.com/user-attachments/assets/64571ad9-9bfe-4256-93a5-a17ad967319c)
```
pip install --upgrade category_encoders
```
![Screenshot 2025-04-07 113235](https://github.com/user-attachments/assets/5165f689-5e12-4467-bd51-fb35233e390e)
```
from category_encoders import BinaryEncoder
df=pd.read_csv("/content/data.csv")
df
```
![image](https://github.com/user-attachments/assets/42e8868e-7196-4904-8575-aa33839863fb)
```
be=BinaryEncoder()
nd=be.fit_transform(df['Ord_2'])
dfb=pd.concat([df,nd],axis=1)
dfb1=df.copy()
dfb
```
![Screenshot 2025-04-07 113356](https://github.com/user-attachments/assets/36f658cb-50ab-41e1-ad5f-cd8639c1b279)
```
from category_encoders import TargetEncoder
te=TargetEncoder()
CC=df.copy()
new=te.fit_transform(X=CC["City"],y=CC["Target"])
CC=pd.concat([CC,new],axis=1)
CC
```
![Screenshot 2025-04-07 113426](https://github.com/user-attachments/assets/e5306eaf-a5c6-499b-b52b-7c11bf67294d)
```
import pandas as pd
from scipy import stats
import numpy as np
df=pd.read_csv("/content/Data_to_Transform.csv")
df
```
![Screenshot 2025-04-07 113733](https://github.com/user-attachments/assets/2db43f84-e167-4927-a8aa-6ed5a05f97cc)
```
df.skew()
```
![Screenshot 2025-04-07 113808](https://github.com/user-attachments/assets/2f480543-01b8-4367-b649-f5e3d31bdc0e)

```
np.log(df["Highly Positive Skew"])
```
![Screenshot 2025-04-07 113907](https://github.com/user-attachments/assets/9da0fd7e-6898-4b51-bcc9-d34d947ace32)
```
np.reciprocal(df["Moderate Positive Skew"])
```
![image](https://github.com/user-attachments/assets/b14961bd-f6ff-4e1c-a65b-f360bf5798ac)
```
np.sqrt(df["Highly Positive Skew"])
```
![image](https://github.com/user-attachments/assets/61723f84-9a56-4bcc-b0db-9cc8363ed543)
```
np.square(df["Highly Positive Skew"])
```
![image](https://github.com/user-attachments/assets/2199b100-e05c-4c6f-91ac-0f7b234f37ca)
```
df["Highly Positive Skew_boxcox"], parameters=stats.boxcox(df["Highly Positive Skew"])
df
```
![image](https://github.com/user-attachments/assets/a9e29fce-ca39-4c6c-afbc-b499a126516a)
```
df["Moderate Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Moderate Negative Skew"])
df
```
![image](https://github.com/user-attachments/assets/0fa61e48-7ce9-4adf-acf2-85b4d4c0cc36)
```
import seaborn as sns
import statsmodels.api as sm
import matplotlib.pyplot as plt
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/1b1f730e-7f64-4474-ba94-a8884a69302d)
```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew_1"]),line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/a39b5576-3fa6-4b98-b8f6-2c9cebcb7ee4)
```
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/223d9096-f47d-4fcd-b1f8-fe176b758cd5)
```
df["Highly Negative Skew_1"]=qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df["Highly Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/4ca510a6-0cf7-4202-adce-fbd7c0f3713f)
```
sm.qqplot(df['Highly Negative Skew_1'],line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/26136a36-3758-437d-9daf-d3c1d150111d)
```
dt=pd.read_csv("/content/titanic_dataset.csv")
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
dt["Age_1"]=qt.fit_transform(dt[["Age"]])
sm.qqplot(dt['Age'],line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/02b35501-632c-4b86-abf3-48477688f58a)
```
sm.qqplot(dt['Age_1'],line='45')
plt.show()
```
![image](https://github.com/user-attachments/assets/c23b95ff-0b0e-426b-8eb2-360c222afd7c)
# RESULT:
       
Thus the given data, Feature Encoding, Transformation process and save the data to a file was performed successfully.
       
