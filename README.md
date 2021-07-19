# Bank_Churn_Prediction

## Table of Contents
* [Introduction] (## Introduction: General Information about the Project)
* [Understanding the Data] (## Understanding the Data: Read data, visualize, basic statistics)
* [Data Preprocessing] (## Data preprocessing, normalization, missing data, categorical data)
* [Feature Analysis, Extraction and Selection] (## Feature Anaysis, Extraction & Selection)
* [Classification Models] (## Classification models)
* [Evaluation and Comparison] (## Evaluation and comparisons, various metrics)
* [Hyperparamter Optimization] (## Hyperparameter Optimization)
* [Final Evaluations and Comparisons] (## Final evaluations and comparisons)
* [Discussion, Conclusion, Future Improvements] (## Discussion, Conclusions, Future improvements)
* [Appendix: Technologies Used] (## Appendix: Technologies used)
* [Acknowledgements] (## Acknowledgements)



## Introduction: General Information about the Project

The goal of this project was to create a robut classifier und use the data in order to be able to predict and find a group of people who are most likely to churn. This information should ultimately allow employees of the bank to proactively target this group of customers to provide them with better services and turn customers’ decisions in the opposite direction.

The dataset includes data of 10127 costumers with 21 features each. The feature that we aim to predict using a model is Attrition_Flag, where Existing Customer is 84% and Attrited Costumer is 16%.

Detailed description with all of the features is found in the document "Models"

## Understanding the Data: Read data, visualize, basic statistics

The first step was to get a better understanding of out dataset. We performed some descriptive statistics, identified which variables are continues and categorical, as well as checking for missing data.

Continuous variables:
* Months_on_book
* Credit_Limit
* Avg_Open_To_Buy
* Total_Amt_Chng_Q4_Q1
* Total_Ct_Chng_Q4_Q1
* Avg_Utilization_Ratio
* Total_Revolving_Bal
* Total_Trans_Amt
* Total_Trans_Ct

![Alt Text](/Pictures/Continuous_variables.png)

Categorical variables:
* Gender
* Age
* Education Level
* Marital Status
* Income category
* Card Category
* Dependent count
* Total relationship count
* Months inactive 12 months
* Contracts count 12 months

![Alt Text](/Pictures/Categorical_variables.png)


Following observations have been made:
* From the graphs we can see that Dependent_count Total_Relationship_Count,Months_Inactive_12_mon and Contacts_Count_12_mon are technically categorical variables as opposed to appearing as continuous at first
* From the scatter plot we indentify that Credit_Limit and Avg_Open_To_Buy are highly correlated (Avg_Open_To_Buy will be dropped while running models)
* Edcuation Level, Matrial_Status and Income_Category have an unkown attribute.
    * Education_Level the distribution between unkown and uneducated are simliar
    * Martial_Status unkown and divorce follow a similiar distribution
* All of the continous varaiabls will need to be scaled to deal with the varying magnitudes

## Feature Analysis, Extraction & Selection



Logistic regression was conducted in order to understand the importance of the features.

![Alt Text](/Pictures/Important_features.png)

## Data preprocessing, normalization, missing data, categorical data

Data preprocessing included following steps:
* Creating various age groups for the age feature
* One hot encoding for all categorical variables
* Label encoding or ordinal encoding depeneding on the categorical variable
* Scaling variables:
    * Standard scaler
    * Robust scaler
        *Credit_Limit', 'Total_Amt_Chng_Q4_Q1','Total_Trans_Amt'- These features will be scaled using robust scaler due to assimetrical distribution
* Handling unknown variables
    * Income_Category: Filling ordinal missing values with modes
    * Marital Status: filling missing values with dominant value 
    * Education Level:The category unknown has been left on purpose as this category was too large to impute 


As we will be testing various models with our dataset it is necessary to conduct different preprocessing for different types of models.

Therefore a function has been created which allows us to decide what type of preprocessing should be done depending on which model will be used consequently. The function allows the user to decide wheter one hot encoding and/ or scaling should be used.



## Classification models

Different types of models have been created. For non treebased models  one hot encoding and scaling is necessary where as for treebased models label encoding and no scaling is necessary.

* Random Forrest classifier
* Logistic Regression Classifier
* AdaBoost Classifier
* GradientBoosting Classifier
* SVM Classifier
* KNeighbors Classifier
* CatBoost Classifier


<<<<<<< Updated upstream
* Artificial Neural Network as Classifier
=======
>>>>>>> Stashed changes

## Evaluation and comparisons, various metrics

The models have been compared with regards to mean, standard deviation, accuracy mean, and accuracy standard deviation. 
Each model  went through the procedure of stratified cross validation with 10 spilt .

![Alt Text](/Pictures/Models.png)

<<<<<<< Updated upstream
Optimal number of trees for random forest model has been analyzed.






## Final evaluations and comparisons
=======
![Alt Text](/Pictures/Models2.png)
>>>>>>> Stashed changes


Optimal number of trees for random forest model has been analyzed

![Alt Text](/Pictures/Models2.png)


## Hyperparameter Optimization

Grid search CV was used for hyperparameter tuning in order to determine the optimal values of our best model, namely Gradient Boost classifier. For this phase of the projected   a tree based model was chosen , after observing that those models handle the data the best . Having scikit learn s GradientBoosting with best Accuracy score on a 10-split stratified K Fold , we decided to start search for best parameters for the problem. For that we used GridSearch algorithm.

parameters = {'n_estimators' : [150,200,250,300],
 'min_samples_split' : [0.2, 0.4, 0.6, 0.8, 1.0, 2], 
'learning_rate' : [0.01, 0.1, 1], 
'max_features':[None, 'log2', 'sqrt'], 
'max_depth' : [1,2,3,4,5,7],

with 4 x 6 x 3 x 3 x 6 parameters and again 10-split Folds , went to 38.000+ fits, which took 18 hours to complete . Best paramaters :

```
GradientBoostingClassifier(max_depth=5, max_features='log2', n_estimators=300,
                           random_state=0)
```

Following results were obtained:
* accuracy score: 0.972


You can see the visual representation of our results below in the form of a confusion matrix as well as the ROC curve

![Alt Text](/Pictures/Confussion_matrix.png)

![Alt Text](/Pictures/ROC.png)

Random CV

## Final evaluations and comparisons

Picture of the decision tree from Anja

Interpretation of the coefficients


## Discussion, Conclusions, Future improvements
which features are the most important
how will you explain the model to the management of the bank
how much benefit/improvement should the bank expect

Conclusion
*

Future improvements
* What needs to be taken into consideration when interpreting the models is that the predictions are based on a much smaller group of Attrited Costumers than Existing Customers


## Appendix: Technologies used

import numpy as np
import pandas as pd

import matplotlib.pyplot as plt
import seaborn as sns
from prettytable import PrettyTable
import sklearn.preprocessing
from sklearn.compose import ColumnTransformer
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import OneHotEncoder
from sklearn.preprocessing import MinMaxScaler
from sklearn.pipeline import Pipeline,make_pipeline
from sklearn.feature_selection import SelectKBest,chi2
from sklearn.tree import DecisionTreeClassifier

from sklearn.preprocessing import LabelEncoder
from sklearn.preprocessing import StandardScaler
from sklearn.preprocessing import RobustScaler

from numpy import mean
from numpy import std
from sklearn.datasets import make_classification
from sklearn.model_selection import cross_val_score
from sklearn.model_selection import RepeatedStratifiedKFold
from sklearn.model_selection import train_test_split


from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from sklearn.svm import SVC
from sklearn.neighbors import KNeighborsClassifier
from sklearn.ensemble import AdaBoostClassifier
from sklearn.ensemble import GradientBoostingClassifier

from category_encoders.cat_boost import CatBoostEncoder


## Acknowledgements

Thank you to the whole Brainster Team for the great learning experience throughout the programm.
Special thanks to our instructors:
- Igor Trepveski
- Viktor Domanzetoski
- Blagoj Kostovski
- Filip Nikolovski
- Marko Karbevski

And also our support Team:
- Aleksandar Chaminski
- Aleksandar Gjurchevski
- Maya Cvetanoska

Anja, Hunter, Julian, & Barbora

