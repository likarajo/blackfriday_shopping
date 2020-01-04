# Black Friday Shopping

## Background

Black Friday is an informal name for the Friday following Thanksgiving Day in the United States, which is celebrated on the fourth Thursday of November. It is regarded as the beginning of America's Christmas shopping season.

## Goal

Using the data of a store, explore trends in the Black Friday shopping based on features like gender, occupation, age etc. and predict the amount of money that a person is likely to spend on Black Friday depending on the features.

## Dataset

Kaggle Black Friday dataset (data from a single store): https://www.kaggle.com/karinne/black-friday<br>
Saved in: *data/black_friday/*

## Dependencies

* Pandas
* Seaborn
* Numpy
* Matplotlib
* Scikit-learn

`pip install -r requirements.txt`

---

## Data Analysis

### Parameters

* 12 parameters - 7 numerical and 12 object variables
  * User_ID - int64
  * Product_ID - object
  * Gender - object
  * Age - object
  * Occupation - int64
  * City_Category - object
  * Stay_In_Current_City_Years - object
  * Marital_Status - int64
  * Product_Category_1 - int64
  * Product_Category_2 - float64
  * Product_Category_3 - float64
  * Purchase - int64

### Gender distribution

* Almost 3 times more male customers than female customers.
* Maybe males are more likely to go out and buy something during the deals and rush.

### Gender and Age distribution

* Most customers belong to the age group between 26 and 35, for both genders.
* Younger and older population do not shop much on Black Friday.

### Customers and Products

* There 5,891 different customers who have bought something from the store.
* There 3631 different products sold in the store.

### Money spent per Occupation

* People having occupations 0 and 4 spent the most money during Black Friday sales.
* People with occupations 8, 18, 19 spenbt the least amount of money.

### City distribution

* There are three different cities from which the customers belong.
* 42% are from city A, 26.9% from B, andthe rest 31.1% from C.

---

## Data Preprocessing

### Check and handle missing values

* Total records in raw train set: 550068
* Total records in raw test set: 233599.
* There are missing values in *Product_Category_2*:
  * No. of data in *Product_Category_2* in train set = 376430; i.e. 31% missing.
  * No. of data in *Product_Category_2* in test set = 161255; i.e. 31% missing.
* We **fill the missing values in *Product_Category_2* with the mean value** of the existing values in this column.
* There are missing values in *Product_Category_3*:
  * No. of data in *Product_Category_3* in train set = 166821; i.e. 70% missing.
  * No. of data in *Product_Category_2* in test set = 71037; i.e. 70% missing.
* We **drop the *Product_Category_3* column** as there are a lot of missing values.

### Remove unrequired columns

* *User_ID* is is the number assigned automatically to each customer and so is not useful for prediction. Therefore we remove the column from our dataset.
* *Product_ID* is not a feature of the customer. Therefore we remove the same from our dataset.

### Convert Categorical features to Numeric

* Convert categorical values to **one-hot encoded vectors**.

### Prepare the Features and Labels

* The features are all the numeric columns along wioth the vectorized columns:<br>
'Occupation', 'Marital_Status', 'Product_Category_1', 'Product_Category_2', 'F', 'M', '0-17', '18-25', '26-35', '36-45', '46-50', '51-55', '55+', 'A', 'B', 'C', '0', '1', '2', '3', '4+'

* The label is the 'Purchase' column

### Split the data into Training and Test sets

* Test data: 40%

## Create and Train Model

```
Learned model: LinearRegression(copy_X=True, fit_intercept=True, n_jobs=None, normalize=False)
Intercept parameter: 12027.61271472023
                    Coefficient
Occupation             5.030011
Marital_Status       -60.424335
Product_Category_1  -408.954291
Product_Category_2   -72.068789
F                   -265.881866
M                    265.881866
0-17                -564.213500
18-25               -214.605258
26-35                -14.122454
36-45                 95.338560
46-50                 89.687620
51-55                381.530967
55+                  226.384065
A                   -283.925835
B                   -125.364273
C                    409.290108
0                    -28.095073
1                     -1.786906
2                      3.219490
3                      8.219723
4+                    18.442765
```

## Test and Evaluate the Model

* **Mean Absolute Error** (MAE): 3587.788450883482
* **Mean Squared Error** (MSE): 22017757.08262227

## Conclusion

* The amount of money spent by a customer on Black Friday sales is predicted based on their gender, age, occupation etc.

## More

* The product that the customer is more likely to purchase on Black Friday sales is predicted based on their gender, age, occupation etc.
  * In this case the label is *'Product_Category_1'*
