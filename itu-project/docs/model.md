# Modeling Section:

The model we need to train is a regression model as we are attempting to predict a number between 0 and 1 of internet connectivity. Later on, we attempted to turn this into a classification problem to check our work but it did not provide any higher accuracy. 

## Mlflow Set-up

In order to track our models, we set up autologging in mlflow. [Mlflow](https://www.mlflow.org/docs/latest/index.html) is an exciting and experimental way of logging models. We set up our model training so that our python script for each model would create a new experiment for each run, it would log each of our model parameters when we did hyperparameter tuning and then log the best parameter at the top. In this way we were able to compare the various parameters logged in each run to determine how to change the grid space of the hyperparameters. We also were then able to compare models to each other. Within mlflow, we also logged the predictors for each run and the requirements for packages and dependencies to run. Each run also logs the best model as an artifact, so one can easily take the model and apply it to new data. We are including both here in order to make this as reproducible as possible. Below you can see a screenshot of a mlflow which logs our best runs, with our best hyperparameters and using our custom metric for evaluation.  On the side, you can also see the list of other experiments we ran with different models. 
![mlflow_setup](Images/mlflow_setup.PNG)s

Here you can see how easy it is to reload the model and apply on new data:
![mlflow_pred](Images/mlflow_pred.PNG)


## Model Configuration
Once we have mlflow set up and our model_config.yaml file set up, we can run many different experiments using our .py scripts by changing a few things within our yaml file. Click here (INSERT YAML Script) to see the full yaml file. Below you can also see how it was set up. We use this to steer our scripts and set our parameters. We set up the input data at the top which is our training data, then label the target and predictor variables as well as the name of the experiment and a brief description in run_name. Under the parameters section, we set parameters like test size (which is crucial), the amount of cross validation folds to do, the number of iterations and the threshold for our custom metric. The threshold tells the model which percent of schools with low internet connectivity to focus on. Then within parameters, there are different sections based on what type of model you might decide to run. Our .yaml file contains parameters for grid search within Random Forest, LightGBM and XGBoost.

![model_config](Images/model_config_yaml.PNG)

## Model Training

We tried out 7 different models in order to determine which model had the best accuracy. We experimented with various parameters, as well as different combinations of predictors. Below is the final list of predictors we used and a heat map displaying their collinearity. As you can see, there is not high multi-collinearity among our predictors except with the mean global human modification and the mean average radiance. However, we felt both predictors were important and had high feature importance in the model so we decided to keep both in. 
![heatmap](Images/heatmap.PNG)


Another way that we improved accuracy was by building a custom metric in order to score both our test set within our cross validation and our final holdout set. The metric calculates errors specifically by taking the prediction below .3 (or another threshold, we also experimented with .5) subtracting that from the ground truth below .3 (or another threshold), taking the absolute value and then returning the average of all those errors. Below please find a code snippet of our custom metric.
`def custom metric`

![custom_metric](Images/custom_metric.PNG)

 We built this as we understood that it was more important to have better accuracy on schools with lower internet connectivity than higher. Before insitituting the custom metric, our models were good with predicting the average values, but they did poorly at either end of the spectrum and particularly on the low values. In order to remedy this issue, we first dropped any rows that had an internet connectivity of zero (there were 23 of them). We dropped the zero's because our project partners informed us that they were most likely due to incomplete data and because they skewed our results. Because there were only 23 of them, we felt it did not impact the data class balancing. Secondly, we instituted our custom metric which trained the model to minimize the error score under the .3 level of prediction. 
 
 Our best model had an average error of .06 and specifically for under the .3 threshold, had an average error of .05. This means that for schools that are predicted to be below 30%, we can trust the model's predictions, as on average the predictions are only off by 5 percentage points from the ground truth value. 

 Below, you can see the list of all the models we tried. Feel free to try out running these models yourselves or reading the code by clicking on the hyper linked script. There is further documentation within each script on how it runs, and how it works with mlflow logging.

1. Linear Regression (see train_Linear_Regression.py)
2. Random Forest (See Jupyter Notebook for full training and evaluation of errors)(see also train_Random_Forest_clean.py file, with mlflow logging and one without)
2. XGBoost (See train_XGBoost_Exp1.py file with mlflow logging and without)
3. LightGBM (See Jupyter Notebook for full training and evaluation of errors)(see also lightgbm_mlflow_train.py)
5. SVM (see SVM_mlflow_train.py file)
6. Neural Net (see nn_mlflow_Train.py file)
7. Random Forest Classifier (See Jupyter Notebook for training, was used as a check on other models)

Here we see a comparison of all the models. It is clear that Random Forest and XGBoost both have the lowest average error among all the models, therefore they are the winners. 
Click on this link to see a notebook with the model comparisons (Also save as HTML to embed into documentation)
![model_graph](Images/model_graph.PNG)

## Model Evaluation and Results 

As you can see from the above graph, our winning model was the XGboost model which produced an error of .06 and a low average error of .05 with the hyper parameters of: eta: .2, max_depth: 9, n_estimators: 550. 

Click on this link for the notebook with the Random Forest Predictions and click on this link for the notebook with the XGBoost Predictions.

Here is a map of our predictions for schools within Brazil. Figure 1 displays the location for all the schools were the ground truth is less than 30% connected to the internet. There are 69 schools in Brazil that have less than 30% internet connectivity. Figure 2 shows the errors in schools where the prediction is less than 30% connected to the internet. While we can see that there are fewer schools that are predicted than that exist, we can trust that our predictions are correct, as the error score is low. This map was made using the Random Forest model which predicts 14 schools. The XGBoost model predicts 29 schools below 30%. Additionally, our predicted schools match up with our ground truth schools. In Figure 3, we see the predictions for all the schools in the test set mapped out. This gives us an understanding of where the higher and lower connected schools are located regionally. It appears that the higher connected schools are on the coast (the yellows and light greens) while the lower connected schools are located more in land. In Figure 4, we see the errors mapped out for the schools in the test set. As we can see most schools have a low error score, which means we can mostly trust the predictions. The schools with higher error scores are also the schools that have less connectivity, which provides even more motivation to use our custom metric as we want to focus on having a lower error score for schools that are less connected. Thus the 14 schools depicted in Figure 2 are the ones that ITU and UNICEF should prioritize to connect. 

![Brazil_Map_predictions](Images/Brazil_map_pred.PNG)

We also see that our predictions closely mirror the ground truth within the country, as well as an external data source titled Digital 2021: Brazil. Thus we can trust that our model performs well on Brazilian school data. 

![Brazil_Table](Images/Brazil_table.PNG)

Next, we will test to see how well this model performed on our Thailand data. 

## Model Interpretation
As part of our winning models, we wanted to see which predictors had high feature importance within the model. Below, is the graph for both Random Forest and XGBoost feature importances. As one can see, the highest feature importances are the nighttime average radiance predictor and the Facebook monthly active users.

![feature_importance](Images/RF_ft_impt.PNG)

![XGBoost_Shap_impt](Images/Shap_ft_impt.png)

Here are the examinations of the shapely values for feature importances. 

@Jacob or Utku to put in pics

