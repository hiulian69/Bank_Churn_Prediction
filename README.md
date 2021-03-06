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

The goal of this project was to create a robust classifier und use the data in order to be able to predict and find a group of people who are most likely to churn. This information should ultimately allow employees of the bank to proactively target this group of customers to provide them with better services and turn customersâ€™ decisions in the opposite direction.

The dataset includes data of 10127 costumers with 21 features each. The feature that we aim to predict using a model is Attrition_Flag, where Existing Customer is 84% and Attrited Costumer is 16%.

Detailed description with all of the features is found in the document "Models"

## Understanding the Data: Read data, visualize, basic statistics, Feature Analysis

The first step was to get a better understanding of out dataset. We performed some descriptive statistics, identified which variables are continuous and categorical, as well as checking for missing data.

Features is data type is integer was investigated further for accurate classification (Months_on_book included as well)

![Alt Text](/Pictures/bar_graphs.png)



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
![Alt Text](/Pictures/Continuous_features.png)



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
* Multiply modal features will be binned for non-tree models (Total_Trans_Amt & Total_Trans_Ct)



## Data preprocessing, Normalization, Missing data, Categorical data, Feature Extraction & Selection

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
* Artificial Neural Network as Classifier


Creating a Neural Network didn't disappoint as result , however :

- having a dataset of only 10k entry is far from enough.
- small set of features
- NN works better with homogenous data
- unlike data from images, audio and language, there can be little variation in a column of a table

Best result of a NN with 3,953 was an accuracy of 0.94

![Alt Text](/Pictures/nn_result.png)

* Classical Mashine Learning algorithms

Different types of models have been created. For non-tree-based models,  one-hot encoding and scaling is necessary,  where as for treebased models label encoding and no scaling has been applied.

* Random Forrest classifier
* Logistic Regression Classifier
* AdaBoost Classifier
* GradientBoosting Classifier
* SVM Classifier
* KNeighbors Classifier
* CatBoost Classifier


## Evaluation and comparisons, various metrics

The models have been compared with regards to mean, standard deviation, accuracy mean, and accuracy standard deviation. 
Each model  went through the procedure of stratified cross validation with 10 spilt .

![Alt Text](/Pictures/Models.png)

Optimal number of trees for random forest model has been analyzed.


![Alt Text](/Pictures/Trees.png)


## Hyperparameter Optimization

Grid search CV was used for hyperparameter tuning in order to determine the optimal values of our best model, namely Gradient Boost classifier. For this phase of the project a tree based model was chosen , after observing that those models handle the data the best . Having scikit learn s GradientBoosting with best Accuracy score on a 10-split stratified K Fold , we decided to start search for best parameters for the problem. For that we used GridSearch algorithm.

parameters = {'n_estimators' : [150,200,250,300],
 'min_samples_split' : [0.2, 0.4, 0.6, 0.8, 1.0, 2], 
'learning_rate' : [0.01, 0.1, 1], 
'max_features':[None, 'log2', 'sqrt'], 
'max_depth' : [1,2,3,4,5,7],

with 4 x 6 x 3 x 3 x 6 parameters and again 10-split Folds , went to 38.000+ fits, which took 18 hours to complete . Best paramaters :

```
 {'learning_rate': 0.1,
  'max_depth': 5,
  'max_features': 'log2',
  'min_samples_split': 2,
  'n_estimators': 300,
  'random_state': 0})
```

Following results were obtained:
* accuracy score: 0.973


## Final evaluations 
You can see the visual representation of our results below in the form of a confusion matrix as well as the ROC curve

![Alt Text](/Pictures/Confussion_matrix.png)

![Alt Text](/Pictures/bar_graphs_1.png)

As expected, due to the unbalanced data set the model's precision score in predicting if a customer will churn outperforms the recall score. Capturing more data in the future would help the model in better generalizing which customers will churn. All things considered, the recall score of 87% is still pretty good.

In a sample of 100 people chosen by model as likely to churn we wolud have 93 people likely to churn which, compared to a random sample in whiich we wolud have 16, represents 77% of an increase in targeting.

Lowering the prediction probability cut-off threshold could potentially help with increasing the recall
* Precision would affected
* What is the cost of missclassifying customers who wouldn't end up churning

![Alt Text](/Pictures/ROC.png)




## Discussion, Conclusions, Future improvements

Following features have been identified as best predictors of churn:


![Alt Text](/Pictures/Important_features.png)

Attrited customers have

Lower:
* Number and Amount of Transaction in the last 12 months
* Total Revolving Balance on the Credit Card
* Total no. of products held by the customer
* Average Card Utilization Ratio
* No. of Contacts in the last 12 months
* Credit Limit on the Credit Card

Higher:
* No. of months inactive in the last 12 months

In additon to:
* negative change in Transaction Count (Q4 over Q1)
* no growth of Transaction Amount (Q4 over Q1)

Conclusions:
* Declining activity in account tends to lead to churn - good basis for marketing strategy
* Socio-demographic features have not been identified as important for churn prediction

Future improvements
* What needs to be taken into consideration when interpreting the models is that the predictions are based on a much smaller group of Attrited Costumers than Existing Customers




## Appendix: Required packages version

* seaborn==0.9.0
* scikit-learn==0.24.1
* pandas==0.25.1
* numpy==1.17.2
* matplotlib==3.1.1
* prettytable==2.1.0
* missingno==0.4.2


## Team Members

- Anja PeÄ‡nik
- Barbora Betkova
- Hunter Marsh
- Horia-Iulian State 





## Acknowledgements

Thank you to the whole Brainster Team for the great learning experience throughout the programm.
Special thanks to our instructors:
- Igor Trepveski
- Viktor Domanzetoski
- Blagoj Kostovski
- Filip Nikolovski
- Marko Karbevski
- Viktorija Doneva

And also our support Team:
- Aleksandar Chaminski
- Aleksandar Gjurchevski
- Maya Cvetanoska



