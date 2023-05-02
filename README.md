# ccdefaultmodel


Problem:

Credit card defaulting occurs when a client fails to make their credit payments for 30 days. This is important for banks, as it can provide more insight into their clients and help create better models for risk. In 2006, the credit card issuers in Taiwan faced the cash and credit card debt crisis and the crisis caused damage in consumer finance confidence. For our project, we used a dataset of default payments of credit card clients in Taiwan from 2005 to predict whether or not a client is going to default based on their habits. 


Dataset: 

For our project, we used the dataset “Default of Credit Card Clients Dataset” from Kaggle. After performing exploratory data analysis to examine the data, as shown in Fig 1.1, we see that our data consists of 24 numerical features, which are columns in the data set used for prediction, and 1 numerical target column, the value we try to predict. We decided to leave out the feature “ID”, as IDs are randomised and do not provide insight into whether or not a client will default. After looking at the features, we examined the distribution of our target class “default.payment.next.month” and discovered that there was a class imbalance, meaning that we had more cards not defaulting than defaulting. This class imbalance can cause a high accuracy in our models so accuracy will not be a very telling indicator of whether our model is working or not. We will instead use F1 scoring, which is a harmonic mean indicator that describes how well our model predicts positive results. 


Fig 2.1


Fig 2.2


Modelling

Before applying models to our data, we had to preprocess the data so our models would be more accurate. We applied scaling to numerical features, such as AGE and LIMIT_BAL, so their magnitudes do not skew our models. Then we applied one-hot-encoding to our categorical values, such as MARRIAGE, EDUCATION, and SEX, so categories are properly interpreted in ourr models. 

The first model we used was the DummyClassifier from scikit-learn. This model acts as our baseline model as it creates a prediction function based on the distribution of our target class without regards to our feature columns. Our scores to beat are a test score and a train score of around 0.50, as we can see in Fig 3.1.


Fig 3.1

	This data was then trained through other models, such as Logistic Regression, Random Forest Classifier, and LGBM Classifier. From comparing the test and train scores in Fig 3.2, we decided on using LGBM Classifier as it performed the best. Random Forest Classifier was a close second, however its train scores indicated that it was overfit, meaning that it corresponded too closely to the data it was trained on. 
	
	We then used GridSearchCV to perform hyperparameter optimization- looking for the best settings to use LGBM Classifier with. Our best performing model ended up with a train score of 0.7 train score and a test score of 0.69 . 



Results and Interpretations 

	With our best model we obtained a train score of 0.70 and a test score of 0.69 using a F1 type scoring system. Compared to our baseline scores of 0.50 and 0.50 from the Dummy Classifier, we can see that our LGBM model is better than just predicting values using the distribution of the target class. This shows that our model is working as intended and better than just guessing.

	
Fig 4.1

We then used the results from ELI5 (Fig 4.1) which helps describe the model and the importance of our features. From our analysis, we can see that our most important features are the PAY, BILL_AMT, PAY_AMT columns with PAY_0 being our most important feature. This makes intuitive sense because whether or not a person pays in the first month could tell a lot about the coming months. EDUCATION did not play as big of a role as we had suspected but this could be due to unknowns in the data in this column. 


Caveats

While working with these models and probabilities, we could have potentially introduced caveats that could render our results as incorrect, misleading, overconfident, or otherwise problematic. The first of the caveats being optimization bias, optimization bias occurs when we perform comparisons between a lot of models and by chance select a model that has a high score. However, our score on our test set performs very similarly to our score on our train set and the amount of models we compared was relatively low, so there's a low chance of optimization bias. Another caveat is that we may not have tested enough models to have found the best model. During this project, we were only able to test Ridge, LGBM, Logistic Regression, and Random Forest Classifier. There could’ve been a model that we did not get to test that performs better than LGBM for this use case. The last caveat is during our hyperparameter optimization. For this project, due to limitations, we decided to only use GridSearchCV to look for the best parameters. There could have been parameters that laid outside of ranges we searched in and therefore there could have been better hyperparameters for the model. We could have potentially used RandomSearchCV to search across big ranges of data instead.   



