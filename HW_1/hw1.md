## What version of pandas do you have
```
import pandas as pd
pd.__version__
```
2.3.2

## Records count
```
import pandas as pd

df = pd.read_csv('car_fuel_efficiency.csv')

len(df)
```
9704

## How many fuel types are present in the dataset?

```
len(df['fuel_type'].unique())
```
2

## How many columns in the dataset have missing values?

```
missing = 0
for column in df.columns:
    if df[column].notna().sum() != len(df):
        print(column)
        missing += 1
```
4

## Max fuel efficiency
`df.loc[df['origin']=='Asia']['fuel_efficiency_mpg'].max()`
23.759122836520497

## Infilling data
1. Median value of horsepower
`df['horsepower'].median()`
149.0
2. Mode of horsepower
`df['horsepower'].mode()`
152.0
3. Fill in missing values with mode
`df['horsepower'].fillna(152)`
4. New median is 152. So it increased

## Linear regression
```
X = np.asarray(df.loc[df['origin']=='Asia'][['vehicle_weight','model_year']])
X = X[0:7,:]
XTX = np.matmul(X.T,X)
XTX_inv = np.linalg.inv(XTX)
Y = np.asarray([1100, 1300, 800, 900, 1000, 1100, 1200])
sum(np.matmul(Y.T,np.matmul(X,XTX_inv)))
```
0.5187709081074007