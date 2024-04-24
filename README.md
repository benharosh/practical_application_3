# Comparing Classifiers for Predictive Analysis in Banking Sector

## OVERVIEW

 In this practical application, the goal is to compare the performance of the classifiers - `K Nearest Neighbors`, `Logistic Regression`, `Decision Trees`, and `Support Vector Machines`. We will utilize a dataset related to marketing bank products over the telephone. [Notebook Link](https://github.com/benharosh/practical_application_3/blob/main/prompt_III.ipynb)

### Business Understanding

The business goal of this task is to find what features can best explain success when the client subscribes the deposit. Using classification models our goal is to increase campaign efficiency by identifying the main characteristics that affect success, helping in a better management of the available resources and by selecting high quality and affordable set of potential buying customers (subscribers).

### Data Understanding

After considering the business understanding, we want to get familiar with our data.  We'll describe some steps taken so we'd get to know the dataset and identify any quality issues within. We'll explore what information it contains and how this could be used to inform our business understanding. After exploring the data, we can see that:
* Data doesn't contain any nulls
* Data contains some categorical columns with 'unknown' values that can affect modeling
* We explored subscription acceptance rate for categorical features in order to understand which customers chose to accept subscription
* We looked into correlation matrix to see what numerical features have higher correlation to the target feature (yes/no subscription)

### Feature Engineering
We encoded categorical columns with `OneHotEncoder` and scaled numerical features with `StandardScaler`

### Modeling

* We splitted the data to train and test sets (0.25 test set size)
Since the data is imbalanced (89% no \ 11% yes) it was important to have a baseline model so we created one  with `DummyClassifier` which showed prediction accuracy that was similar (88.9%) to the natural data split.
* We built a simple `Logistic Regression` model with subset of our data, mainly contains categorical features to get a sense of a basic real calssification model performace. We received results similar to the dummy classifier.
* We compared the performance of the `Logistic Regression` model to `KNN` algorithm, `Decision Tree`, and `SVM` models. Using the default settings for each of the models we generated a table to compare the different models. 
* We aimed to improve our models performace by using `GridSearchCV` and tuning the different models hyperparameters.

### Findings
* `Logistic Regration` performed better (0.94 f1-score) than the rest of the models (0.83-0.84 f1-score). Since our data is heavily imbalanced we decided to focus on f1-score, and less on accuracy
* Following `GridSearchCV` and tuning the different models hyperparameters `Logistic Regression` model performance actually got worse (down to 0.875 f1-score), while `Decision Tree`'s f1-score improved to 0.94. `Decision Tree` was able to get to that score using a single split over the `nr.employed` feature.
* `Decision Tree` (with `GridSearchCV`) and `Logistic Regression` (basic model on minimal set of features) performed best 

### Recommendations
From the results, we can recommend the following things:
- Focus on customers that are: 
  * Their marital status is single
  * Their job status is student, entrepreneur or retired
  * Younger (<30) customers
- Run marketing campaigns when the interest rate (`Euribor 3 Month Rate`) is lower (<3.5%)
- Focus on economic context attribute as `nr.emplyoed` - number of employees (quarterly indicator)
