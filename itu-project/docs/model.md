# Modeling Section:

The model we need to train is a regression model as we are attempting to predict a number between 0-100 of internet connectivity. Later on, we attempted to turn this into a classification problem to check our work and it did not provide any higher accuracy. 

## Model Training

We tried out 7 different models in order to determine which model had the best accuracy. In addition, we built a custom metric in order to score both our test set within our cross validation and our final holdout set. Below please find a code snippet of our custom metric. We built this as we understood that it was more important to have better accuracy on schools with lower internet connectivity than higher. Before insitituting the custom metric, our models were good with predicting the average values, but they did poorly at either end of the spectrum and particularly on the low values. In order to remedy this issue, we first dropped any rows that had an internet connectivity of zero (there were 23 of them). Secondly, we instituted our custom metric which trained the model to minimize the error score within the 0 - 30 level of predictions. Our best model had an average error of .06 and for specifically predicting schools below 30% connected, had an average error of .05. This means that for schools that are predicted to be below 30%, we can trust their predictions as on average they are only off by 5 percentage points from the ground truth value. 

1. Linear Regression
2. Random Forest
2. XGBoost
3. LightGBM
5. SVM
6. Neural Net
7. Random Forest Classifier

We can also talk about the parameters we set in our model_config file, the hyperparameters we searched, etc

We can show a graph comparing all the models

Additionally, here are all the predictors we used and their correlations with each other. As we can see, there is not high multi-collinearity. 

## Model Evaluation and Results 

As you can see from the above graph, our winning model was the XGboost model which produced an error of .06 with the hyper parameters of: . 

Here is a map of our predictions for schools within Brazil. We predicted X amount of schools that have less than 30% internet connectivity which ITU and UNICEF should prioritize to connect. 

Here is also a map of ground truth data. There are 69 schools in Brazil that have less than 30% internet connectivity. 

Here is also a graph of our feature importances for our final model.

Here are the examinations of the shapely values for feature importances. 

How our predictions did for Brazil, show the maps, pretty well!

## Model Application

This is where we show our application of our Brazil model to the Thailand Data and display how well it did.

Our next big step was applying the best model to Thailand data. We were nervous to apply the model as we were not sure that the same assumptions that are true for Brazil would hold true for Thailand. While the satellite data and ground may look the same, the national level economic and political indicators were not accounted for in the model.

We load the model from mlflow where it was pickled as an artifact. Here's some code showing how it was reloaded.

We then input the thailand school points as well as all of the same predictors into the model to be predicted. 

Here are the maps show the schools prediction from 0-100 in Thailand.

Then we aggregated up to a province level as we only have the survey data on that level. This proved challenging for a number of reasons. For one, the level of granularity for the school level is very overshadowed when aggregated to a province level, as there are only 77 provinces within Thailand. It is an unhelpful ground truth to evaluate our predictions which are on a school level. It is therefore hard to know if we can trust our predictions for the schools. 

