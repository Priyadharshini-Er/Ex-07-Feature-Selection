# Ex-07-Feature-Selection
## AIM
To Perform the various feature selection techniques on a dataset and save the data to a file. 

# Explanation
Feature selection is to find the best set of features that allows one to build useful models.
Selecting the best features helps the model to perform well. 

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature selection techniques to all the features of the data set
### STEP 4
Save the data to the file


# CODE
```
Developed By: PRIYADHARSHINI P
Reg.No: 212222100039

# PROGRAM FOR TITANIC

import pandas as pd
import numpy as np
df = pd.read_csv("titanic_dataset.csv")
df

df.isnull().sum()
from sklearn.preprocessing import LabelEncoder
from sklearn.impute import SimpleImputer
from sklearn.feature_selection import SelectKBest
from sklearn.feature_selection import chi2
df.drop(['PassengerId', 'Name', 'Ticket', 'Cabin'], axis=1, inplace=True)
le = LabelEncoder()
df['Sex'] = le.fit_transform(df['Sex'])
df['Embarked'] = le.fit_transform(df['Embarked'].astype(str))
imputer = SimpleImputer(missing_values=np.nan, strategy='median')
df[['Age']] = imputer.fit_transform(df[['Age']])
print("Feature selection")
X = df.iloc[:, :-1]
y = df.iloc[:, -1]
selector = SelectKBest(chi2, k=3)
X_new = selector.fit_transform(X, y)
print(X_new)
df_new = pd.DataFrame(X_new, columns=['Pclass', 'Age', 'Fare'])
df_new['Survived'] = y.values
df_new.to_csv('titanic_transformed.csv', index=False)
print(df_new)

# PROGRAM FOR CARPRICE.CSV

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df = pd.read_csv("CarPrice.csv")
df
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
from sklearn.feature_selection import SelectKBest, f_regression
from sklearn.ensemble import ExtraTreesRegressor
df = df.drop(['car_ID', 'CarName'], axis=1)
le = LabelEncoder()
df['fueltype'] = le.fit_transform(df['fueltype'])
df['aspiration'] = le.fit_transform(df['aspiration'])
df['doornumber'] = le.fit_transform(df['doornumber'])
df['carbody'] = le.fit_transform(df['carbody'])
df['drivewheel'] = le.fit_transform(df['drivewheel'])
df['enginelocation'] = le.fit_transform(df['enginelocation'])
df['enginetype'] = le.fit_transform(df['enginetype'])
df['cylindernumber'] = le.fit_transform(df['cylindernumber'])
df['fuelsystem'] = le.fit_transform(df['fuelsystem'])
X = df.iloc[:, :-1]
y = df.iloc[:, -1]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2,
random_state=1)
print("Univariate Selection")
selector = SelectKBest(score_func=f_regression, k=10)
X_train_new = selector.fit_transform(X_train, y_train)
mask = selector.get_support()
selected_features = X_train.columns[mask]
model = ExtraTreesRegressor()
model.fit(X_train, y_train)
importance = model.feature_importances_
indices = np.argsort(importance)[::-1]
selected_features = X_train.columns[indices][:10]
df_new = pd.concat([X_train[selected_features], y_train], axis=1)
df_new.to_csv('CarPrice_new.csv', index=False)
print(df_new)
```

# OUPUT FOR TITANIC
![image](https://github.com/Priyadharshini-Er/Ex-07-Feature-Selection/assets/119558093/7aa8f827-f016-405d-b4fd-9e184d5ff245)
![image](https://github.com/Priyadharshini-Er/Ex-07-Feature-Selection/assets/119558093/e426919e-9744-4c5b-9d47-a97a24b74f03)

![image](https://github.com/Priyadharshini-Er/Ex-07-Feature-Selection/assets/119558093/cef76cdb-7af7-4578-a664-a74ad9aeb65d)\

# OUTPUT FOR CARPRICE.CSV
![image](https://github.com/Priyadharshini-Er/Ex-07-Feature-Selection/assets/119558093/b6eeae38-9396-4e77-989b-c45653c5b3ce)
![image](https://github.com/Priyadharshini-Er/Ex-07-Feature-Selection/assets/119558093/c02aef08-ac73-48db-adec-fbb8f25e8469)

# RESULT:
Thus, the various feature selection techniques have been performed on a given dataset successfully.


