# Is this client suitable for granting a loan?

The banks have an important role in every economy because are the best instruments for the monetary policy to fulfill its role and multiply money through the granting of credits. For that reason, the banks have to be sure that their potential clients are suitable for a loan, since their probability of default is minimal.

The purpose of this project consist in set up a model that can be used by a bank to properly classify its customers. In this way, this project analyses historical data containing relevant information of the debtors and with a machine learning model predict the probability that a customer of a bank will experience financial distress in the next two years.

## Problem

The credit risk is one of the most important risks that a bank must analyze and mitigate everyday. These institutions have to determine if their potential clients are going to pay or not their debts. If some of these clients go into default, the banks have to spend on provisions, that depending on their magnitude, they could considerably affect their profits. That is why it is important to have the best models possible to predict the probability that a potential client could default in the future.

## Data exploration

The dataset was obtain from the [Kaggle](https://www.kaggle.com/c/GiveMeSomeCredit) competition 'Give me some credit'. It has information from 150,000 clients about their financial behavior and some personal data like age and number of dependents in their family. The target variable 'SeriousDlquin2yrs' its a dummy that takes the value of 1 if the person experienced 90 days past due deliquency or worse, and 0 otherwhise.

The first step of this proyect consist in explore and analyse the data. In that way, here are the descriptive statistics of the variables in this dataset.

![image](https://user-images.githubusercontent.com/89614195/173729531-1dfd5d8a-e64f-43c9-ab22-e9b1da7022cc.png)

From this statistics we can conclude that there could be some problems with the data, which has to be solved before modelling. First, there are variables like MonthlyIncome and NumberOfDependents that has missing values.

![image](https://user-images.githubusercontent.com/89614195/173729423-94c5c50f-6ec9-4d1f-8bb3-fc2fd0467ca8.png)

Second, there are variables with values that are not reasonable and that could be signs of the presence of errors in the dataset. For example, the variable DebtRatio that represents the monthly payments to the debts over the gross income of the clients has high values that are not logical. Third, in some variables it can be seen that the maximums deviate considerably from the mean and the 75% percentile, which could reflect the presence of outliers.

![image](https://user-images.githubusercontent.com/89614195/173733064-dbf05c72-87ad-486a-a9eb-fdb5ae94272b.png)

## Data cleaning

The next step in building the model consist in analyze the data and determine if it should be modified or deleted in order to have the best possible estimate. In this sense, in order to eliminate the presence of outliers and inconsistencies in the database, the interquartile range (IQR) was used.

Since the DebtRatio has a relevant number of records that they are not reasonable, it was made a exhaustive analysis to determine the steps to follow. Looking at the box-plot of this variable, it can be seen that there are several records considerably away from their IQR. Going deeper into the subject, it turns out
evident that these records present inconsistencies, since the vast majority of records with high DebtRatio have no monthly income. Also when analyzing this range one would expect that if a client has a hight DebtRatio, its probability of default will increases, but in this cases the opposite happens, this decreases compared to the total database.

From this finding, several assumptions could be made to determine the reason for the presence of all these errors in the DebtRatio variable with the aim of not deleting all these records, but the data scientist could make the wrong assumption and generate considerable distortion in the results of the classification. It is for that reason that it was decided to eliminate these observations.

Another aspect that was observed in this step was that the database was unbalanced, this means that the dependent variable has many customers that have not defaulted (93.34%) and few defaulted (6.62%). In this sense, we used the SMOTE algorithm in order to balance the data (50/50). At the end of this step, there were 185,434 observations in the dataset that were used to fit the machine learning model.

## Modelling and evaluation

To estimate the probability of default and classify the clients based on some of its characteristics, it was decided to use the AdaBoost and the XGBoost models.
These are some of the predictive algorithms most used today due to the good results they generate and the little computational power required.

In this way, the database was divided into one for training the model and another to testing it. Once the AdaBoost and XGBoost algorithms were executed, we obtain
estimates and review their results.

The results of the AdaBoost were the following:

![image](https://user-images.githubusercontent.com/89614195/173738192-c2f4bcf0-a911-4d72-92ed-9f7d2076071d.png)

Meanwhile the results of the XGBoost were:

![image](https://user-images.githubusercontent.com/89614195/173738229-9ed131f2-8579-478e-a677-59b99b05496d.png)

Analyzing the results, it was concluded that between these two models it was better to select the XGBoost, but with the aim of improving the model, it was executed again with the GridSearchCV algorithm with these parameters:

![image](https://user-images.githubusercontent.com/89614195/173738734-cdd0fa94-ff2d-4a76-9e03-8bc806155422.png)

This XGBoost model ('learning_rate': 0.1, 'max_depth': 7, 'n_estimators': 300) generates the following results:

![image](https://user-images.githubusercontent.com/89614195/173738782-6419a30a-be38-4a8d-a8fe-3e4dea9bb56f.png)

This results confirm the good performance of the model to determine the probability of non-compliance by customers of this banking entity.

## Conclusion

As it could be observed, there are several stages that a data scientist must execute in order to respond to the problem that may arise. In this case, this project consisted in the construction of a robust model that allowed the properly classification of the customers of this bank. However, we learned the importance of data quality in order to achieve the best possible results in modelling. In that way, the improvements that must be taken into account are aimed at guaranteeing the best  possible data gathering, that will result in least number of incosistencies in the values of the observations.
