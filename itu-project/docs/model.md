# Modeling Section:

The model we need to train is a regression model as we are attempting to predict a number between 0-100 of internet connectivity. Later on, we attempted to turn this into a classification problem to check our work and it did not provide any higher accuracy. 

## Mlflow Set-up

In order to track our models, we set up autologging in mlflow. Mlflow is an exciting and experimental way of logging models. We set up our model training so that our python script for each model would create a new experiment for each run, it would log each of our model parameters when we did hyperparameter tuning and then log the best parameter at the top. In this way we were able to compare the various parameters logged in each run to determine how to change the grid space of the hyperparameters. We also were then able to compare models to each other. Within mlflow,we also logged the predictors for each run and the requirements for packages and dependencies to run. We are including both here in order to make this as reproducible as possible. Below you can see a screenshot of a mlflow which logs our best runs, with our best hyperparameters and using our custom metric for evaluation.  

## Model Configuration
Once we have mlflow set up and our model_config.yaml file set up, we can run many different experiments using our .py scripts by changing a few things within our yaml file. Click here to see the full yaml file. Below you can also see how it was set up. We use this to steer our scripts and set our parameters. 

![model_config](Images/model_config_yaml.PNG)

## Model Training

We tried out 7 different models in order to determine which model had the best accuracy. In addition, we built a custom metric in order to score both our test set within our cross validation and our final holdout set. Below please find a code snippet of our custom metric.
`def custom metric`

 We built this as we understood that it was more important to have better accuracy on schools with lower internet connectivity than higher. Before insitituting the custom metric, our models were good with predicting the average values, but they did poorly at either end of the spectrum and particularly on the low values. In order to remedy this issue, we first dropped any rows that had an internet connectivity of zero (there were 23 of them). Secondly, we instituted our custom metric which trained the model to minimize the error score within the 0 - 30 level of predictions. Our best model had an average error of .06 and for specifically predicting schools below 30% connected, had an average error of .05. This means that for schools that are predicted to be below 30%, we can trust their predictions as on average they are only off by 5 percentage points from the ground truth value. 

1. Linear Regression (see train_Linear_Regression.py)
2. Random Forest (See Jupyter Notebook for full training and evaluation of errors)(see also train_Random_Forest_clean.py file, with mlflow logging)
2. XGBoost (See train_XGBoost_Exp1.py file with mlflow logging)
3. LightGBM (See Jupyter Notebook for full training and evaluation of errors)(see also lightgbm_mlflow_train.py)
5. SVM (see SVM_mlflow_train.py file)
6. Neural Net (see nn_mlflow_Train.py file)
7. Random Forest Classifier (See Jupyter Notebook for training, was used as a check on other models)

We can also talk about the parameters we set in our model_config file, the hyperparameters we searched, etc

We can show a graph comparing all the models.
Click on this link to see a notebook with the model comparisons (Also save as HTML to embed into documentation)

Additionally, here are all the predictors we used and their correlations with each other. As we can see, there is not high multi-collinearity. 

## Model Evaluation and Results 

As you can see from the above graph, our winning model was the XGboost model which produced an error of .06 with the hyper parameters of: . 

Click on this link for the notebook with the Random Forest Predictions and click on this link for the notebook with the XGBoost Predictions

Here is a map of our predictions for schools within Brazil. We predicted X amount of schools that have less than 30% internet connectivity which ITU and UNICEF should prioritize to connect. 

Here is also a map of ground truth data. There are 69 schools in Brazil that have less than 30% internet connectivity. 

How our predictions did for Brazil, show the maps, pretty well!

Also show how they compare to external information, the list that Jacob made

## Model Interpretation
Here is also a graph of our feature importances for our final model.

Here are the examinations of the shapely values for feature importances. 

