# Bank_Churn_Prediction

<<<<<<< HEAD
## Introduction: General Information about the Project

The goal of this project was to create a robut classifier und use the data in order to be able to predict and find a group of people who are most likely to churn. This information should ultimately allow employees of the bank to proactively target this group of customers to provide them with better services and turn customers’ decisions in the opposite direction.

The dataset includes data of 10127 costumers with 21 features each. The feature that we aim to predict using a model is Attrition_Flag, where Existing Customer is 84% and Attrited Costumer is 16%.

## Understanding Data: Read data, visualize, basic statistics

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

![Alt Text](/Users/barborabetkova/Desktop/Pictures Brainster/Categorical_variables.png)


Following observations have been made:
* From the graphs we can see that Dependent_count Total_Relationship_Count,Months_Inactive_12_mon and Contacts_Count_12_mon are technically categorical variables as opposed to appearing as continuous at first
* From the scatter plot we indentify that Credit_Limit and Avg_Open_To_Buy are high correlated (Avg_Open_To_Buy will be dropped while running models)
* Edcuation Level, Matrial_Status and Income_Category have and unkown attribute.
    * Education_Level the distribution between unkown and uneducated are simliar
    * Martial_Status unkown and divorce follow a similiar distribution
* All of the continous varaiabls will need to be scaled to deal with the varying magnitudes



## Data preprocessing, normalization, missing data, categorical data

Data preprocessing included following steps:
* Creating various age groups for the age feature
* One hot encoding for all categorical variables
* Label encoding or ordinal encoding depeneding on the categorical variable
* Scaling variables:
    * Standard scaler
    * Robust scaler
* Handling unknown variables
    * Income_Category: Filling ordinal missing values with modes
    * Marital Status: filling missing values with dominant value 
    * Education Level:The category unknown has been left on purpose as this category was too large 


As we will be testing various models with our dataset it is necessary to conduct preprocessing for different types of models.

Therefore a function has been created which allows us to decide what type of preprocessing should be done depending on which model will be used consequently. The function allows the user to decide wheter one hot encoding and/ or scaling should be used.


## Feature Anaysis, Extraction & Selection



## Classification models

Different types of models have been created. For non treebased models  one hot encoding and scaling is necessary where as for treebased models label encoding and no scaling is necessary.

* Random Forrest classifier
* Logistic Regression Classifier
* AdaBoost Classifier
* GradientBoosting Classifier
* SVM Classifier
* KNeighbors Classifier
* CatBoost Classifier


## Evaluation and comparisons, various metrics

The models have been compared with regards to mean, standard deviation, accuracy mean, and accuracy standard deviation


Optimal number of trees for random forest model has been analyzed


## Hyperparameter Optimization


## Final evaluations and comparisons


## Discussion, Concusions, Future improvements
which features are the most important
how will you explain the model to the management of the bank
how much benefit/improvement should the bank expect




# Project Name
> Outline a brief description of your project.
> Live demo [_here_](https://www.example.com). <!-- If you have the project hosted somewhere, include the link here. -->

## Table of Contents
* [General Info](#general-information)
* [Technologies Used](#technologies-used)
* [Features](#features)
* [Screenshots](#screenshots)
* [Setup](#setup)
* [Usage](#usage)
* [Project Status](#project-status)
* [Room for Improvement](#room-for-improvement)
* [Acknowledgements](#acknowledgements)
* [Contact](#contact)
<!-- * [License](#license) -->


## General Information
- Provide general information about your project here.
- What problem does it (intend to) solve?
- What is the purpose of your project?
- Why did you undertake it?
<!-- You don't have to answer all the questions - just the ones relevant to your project. -->


## Technologies Used
- Tech 1 - version 1.0
- Tech 2 - version 2.0
- Tech 3 - version 3.0


## Features
List the ready features here:
- Awesome feature 1
- Awesome feature 2
- Awesome feature 3


## Screenshots
![Example screenshot](./img/screenshot.png)
<!-- If you have screenshots you'd like to share, include them here. -->


## Setup
What are the project requirements/dependencies? Where are they listed? A requirements.txt or a Pipfile.lock file perhaps? Where is it located?

Proceed to describe how to install / setup one's local environment / get started with the project.


## Usage
How does one go about using it?
Provide various use cases and code examples here.

`write-your-code-here`


## Project Status
Project is: _in progress_ / _complete_ / _no longer being worked on_. If you are no longer working on it, provide reasons why.


## Room for Improvement
Include areas you believe need improvement / could be improved. Also add TODOs for future development.

Room for improvement:
- Improvement to be done 1
- Improvement to be done 2

To do:
- Feature to be added 1
- Feature to be added 2


## Acknowledgements
Give credit here.
- This project was inspired by...
- This project was based on [this tutorial](https://www.example.com).
- Many thanks to...


## Contact
Created by [@flynerdpl](https://www.flynerd.pl/) - feel free to contact me!


<!-- Optional -->
<!-- ## License -->
<!-- This project is open source and available under the [... License](). -->

<!-- You don't have to include all sections - just the one's relevant to your project -->
=======


A manager at the bank is disturbed with more and more customers leaving their credit card services. They would really appreciate if one could predict for them who is gonna get churned so they can proactively go to the customer to provide them better services and turn customers' decisions in the opposite direction.

This project is about predicting and finding the group of people , who are most likely to churn . We got the dataset of 10127 costumers with 21 features each.
With other words , the main goal of the project is to easearch and find best model and results for predicting the target feature : Attrition_Flag, where 
Existing Customer is 84% and Attrited Costumer is 16% => imbalance that would make it hard for any model to adapt.

##Planning the Preprocessing 
## DATA ANALYSING & CLEAINING

## MODELS IMPLEMENTATION

>>>>>>> b254f4429c6f24b9b2e7bec27e93a75fb929a278
