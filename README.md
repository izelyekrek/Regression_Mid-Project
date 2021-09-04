# Regression_Mid-Project

# 1 The objective of the project
The main objective of this project is to build a model that will predict the price of a house based on features provided in the dataset. 
The senior management also wants to explore the characteristics of the houses using some business intelligence tool.
Moreover, the first mission for this project is to check if some variables are explained by the target column 'Price' which is the market value of the houses. The second purpose is to see if the linear regression model fits to this data with the target.

# 2 The organization of the project 
For this project, we will see the use of different tools for answering questions and creating a linear regression model. The steps are :

    1) Answering to some questions on the SQL workbench
    2) Cleaning, analysing, creating the linear regression model and fitting it to the dataset
    3) Answering some question on the business intelligence tool which is Tableau
    
# 3 SQL questions and queries
Before we move to the main objective of this project, a few SQL questions were answered where different tools where used such as dropping a column, order by, grouping by, count, avg (average), where, having with subqueries, standard deviation for calculating the correlation and rank statement. 
The queries for these questions can be find in the file named "SQL questions and queries".

# 4 Imported libraries
In order to analyse and built my model, I imported the needed libraries such as :

    - pandas
    - numpy
    - matplotlib
    - scipy.stats
    - sklearn.metrics (mean_squared_error, r2_score, mean_absolute_error)
    - sklearn.linear_model (LinearRegression)
    - sklearn.preprocessing (OneHotEncoding, Normalizer)
    - statsmodels.api
    - seaborn

# 5 Explanation of how the data was processed (including the cleaning and selection of the variables to include in the model)
After importing the libraries, I imported the dataset and checked a few information about it such as :

    - the dataset shape : 
        - 21597 rows
        - 21 columns

    - the type of the columns : numerical or categorical. 

<img src="Images/columnstype.png">
    
We can see that there is only 1 categorical column and the rest is numerical. Moreover, a few columns can be convert to categorical because there are only a few unique values in each column. These columns, with respectively the different variables, are : 

        - 'bedrooms' : from 1 to 10 and 33
        - 'bathrooms' : from 0.5 until 5.25 by step of 0.25
        - 'floors' : from 1 to 3.5 by step of 0.5
        - 'waterfront' : 0 (no waterfront) and 1 (with waterfront)
        - 'view' : from 0 to 5
        - 'grade' : from 3 to 12
        
    - checking the difference between the 75% and the max row to see in which columns there is a huge gap and which one to clean the outliers. 
    
    We can see here that there is a big difference in the columns : 'sqft_living','sqft_lot', 'sqft_living15','sqft_lot15','sqft_basement' and 'sqft_above'
    
Before to build the linear regression model, I cleaned the dataset step by step :

## 5.1 Null values

Checking null values is important. As we can see there is not null values in the dataframe.

<img src="Images/null_values.png">

## 5.2 Removing duplicates

We can see taht there is no duplicates because we still have the same amount of rows. 

## 5.3 Checking and cleaning the outliers 
As we saw the big gap between the 75% and the max row in a few columns.
When I clean them once with a def function, I loose a lot of data so I decided to do it column by column. 
As I decided at the beginning to just keep the sqft_libing15 and sqft_lot15 of 2015 because for me the most logic was to keep the most recent measures of the houses. 
I cleaned the outliers of the following columns : 'sqft_living15','sqft_basement' and 'sqft_above'.
I meant to not clean the sqft_lot15 column, even there is a huge gap between the 75% and the max, because when I do the correlation later we realise that the sqft_lot15 column has really low correlation (that means that I will drop it) so I decided that it will be useless to clean before the outliers of this column and also because it will make loose a lot of rows for nothing. 

## 5.4 Checking for correlation
After cleaning my dataset, I check for the correlation to drop some columns if necessary to built correctly my model. 
As said at the beginning, our target value is the 'price', so we look to the correlation score of the column's regarding to the price column. 

<img src="Images/hmap.png">

As we can see, in the following columns, the correlation with the target is low : 'condition','yr_built','yr_renovated','zipcode','long','sqft_lot15'. 
So I dropped these columns from my dataset.

## 5.5 Encoding the categorical columns :
I converted some numerical columns to categorical because they have a few unique values.
After that, I used the OneHot encoding method for encoding the categorical columns into numerical columns :

    - OneHot encoding : Assign a unique integer to each label based on alphabetical order.
    
# 6 Fitting the model
After all of this steps, it's now time to fit the dataset to the linear regression model and to test different combination to improve our model. 
For this analyse, we will just concentrate on the R2 (R-squared) score to approve or not that the combination is improving the model.

To facility the comprehension of the different score, I decided to collect them in a table. 
More the R2 score is high, more this combination will make better predictions in the future. 

Let's first check the for the R2 with only the dataset after cleaning it but without encoding the categorical columns :

<img src="Images/R2_score.png">

--> Our R2 score is 0.648. 

Now we are going to try different combination to see if we can increase this R2 score :

    - Normalizer : to change the values of numeric columns in the dataset to a common scale, without distorting differences in the ranges of values.
    - Standardizer : to convert data to a common format to enable users to process and analyze it.
    - KNN regressor : approximates the association between independent variables and the continuous outcome by averaging the observations in the same neighbourhood.
    
The score for each combination are : 

<img src="Images/Final_scores.png">

# Conclusion
In my opinion, the R2 score didn't improve that much because the correlation between the target value "price" and the other columns are not high a lot. 

We just had 3 columns with a correlation score above 0.5. 

So, I will keep the combination KNN regressor and OneHot encoding as a model which has the highest score 0.664. 



