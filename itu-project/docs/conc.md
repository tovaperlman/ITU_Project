# Conclusion

# Discussion

## Limitations


## Next Steps

### Additional Methods
Multiple additional methods could be applied to our existing models and analyses: 
#### 1. Full scoring on Brazil
Given our existing champion model, all schools outside the featured enumeration areas can now be scored with an estimated level of connectivtiy. This could be done for a sample of schools as a sanity check or for entire Brazil, which would yield a similar map like the Giga Initiative connectivtiy map. 
#### 2. Statistical robustness checks
Especially two steps could be reasonable additions that take the geographic nature of the data into account: Estimating a Geographically Weighted Regression (GWR) and performing spatial cross-validation on the models.
#### 3. Experiment with featured data
The manner in which we used some of the features could be varied. First of all, it could be fruitful to experiment with Facebook data as an alternative target variable. If model performance still remains on an acceptable level, this would render Microdata obsolete and would enable a global extension of our project. Furthermore, pulling OSM school locations for Brazil and applying the model to this sample could yield insights on the representativity of OSM data. Lastly, buffer zones around schools are currently constant in diameter, but could be varied according to specific variables (e.g. population data).  

### Extension on other countries 
The existing model can be applied to every country, with OSM school location data available. However,model evaluation or model training for other countries requires two more components: Microdata (on household, individual or enumeration area level) and the respective shapefiles/geolocation of the enumeration area. Our analyses have indicated, that analyzing larger geographical aggregates like provinces diminishes model performance and interpretability. An enumeration area is assumed to be a largely homogeneous area, whereas the variation of connectivtiy within e.g. a federal state should be much higher. 

### Further model training 
With more countries being included to the connectivity analysis, more options of model combinations open up. Given the requirements are met, an individual model can be trained for each country and evaluated separately. In addition, joint models with multiple countries could result in a high predictive power on a global level and increase model robustness. Comparing the performances of combined and single-country models can give insights on the impact of country specific differences. Furthermore, it might be a reasonable idea to train regional models (e.g. a model for South East Asian countries). Actors that are not able to provide enumeration area level microdata (e.g. due to anonymity restrictions) can obtain our provided scripts and additional content and run a custom model training. 


If we had another few months, we would have trained a model on Thailand and perhaps one on the Phillipines. Then we would have loved to combine them into one model to predict for a fourth country. As mentioned prior, we do not have national level statistics or information in any of these models since they are trained on one country exclusively. If we were able to combine different models, we could better know if there is some variance explained by regional or national levels of information as opposed to granular scale information. 