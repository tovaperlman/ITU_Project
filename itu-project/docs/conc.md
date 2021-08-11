## Conclusion

We have gained a variety of insights that can be used in future research and extension of the analyses. While our technical and methodological learnings have been outlined in the previous sections, the following conclusion will briefly provide a business interpretation of the project and then discuss limitations and possible next steps. 

### Business Interpretation 

We have developed a tool that is capable of providing multiple outcomes. First of all, after model application a prioritizing list of school within a country can be created. The priorization can be according to the absolute number of offline population served or sorted by lowest shares of online population. In addition, it is possible to exclude adapt the listing e.g. by excluding densely populated areas in order to get a list of schools in lowly populated areas, that would benefit most from internet connection. Moreover, the level of geographic aggregation of connectivity ratio can be modified up to federal state or full country level.
Our provided scripts in combination with the documentation can now assist institutions like Giga Initiative to manage resource allocation for connecting schools. This can be done within a country, between multiple countries and potentially on province, region or city level. Aside from that we have created a low-threshold tool for feature data gathering and EDA. Creating simple map graphics or correlation plots might already indicate the presence of clear tendencies. 

### Limitations
During our project we have faced limitations especially in the area of model evaluation. The results make sense within our model and data, however it is yet to determine how this transfers to reality. Future extension and application of our models can help to further evaluate our project outcome. In the special case of Thailand another problem became obvious: Since the used data inherited multiple sources of error it was not possible to separate these from each other. In this specific case, for instance, we  could not find out to which degree the geographic aggregation of the target variable or the fact that we used OSM schools impacted model performance and error. 

In addition to the limitations we faced, there are more limitations that could possibly be present in our work as well as in future extensions. 
As touched upon previously, we cannot evaluate yet how OSM school data performs compared to official school location data. If this datasource is supposed to be a cost and resource efficient replacement for UNICEF school data, its representativity should be reviewed. Furthermore, Facebook data could inherit a an "instability" of how to interpret the feature . If popularity of Facebook differs over time, between countries or according to demographic indicators utilization does not remain straight forward. When examining feature importances and impacts, larger number of Facebook users have generally led to higher predictions of online population. However, if a big internationalized metropolitan area (e.g. Buenos Aires) shows a low percentage of Facebook users, this could much rather be due to the fact that another social media platform (such as Instagram) has overtaken the popularity. An analysis of dispersion of Facebook users among social strata could prevent a misinterpretation of data.
Another potential source of bias could be the fact, that in our approach survey data is used as ground truth. Survey data are typically prone for biasing mechanisms like misreport or systematic non-response. Survey respondents have previously stated that they are not using the internet but in the same survey declared themselves as internet users. Non-response could be problematic if offline people tend to respond to the survey less likely. A potential corroborrating measure here could be comparing the distribution of demographic data within the survey (e.g income, gender) with other open (official) data sources. 
Ultimately, if the analyses will be extended to more countries the availability of microdata could bias the selection of countries that will be targeted. One could assume, that countries where no microdata on telecommunications exists could as well be countries with low connectivity. Further research should attempt to not disregard low connected countries systematically and potentially aim for a full open source data approach.


### Next Steps

#### Additional Methods
Multiple additional methods could be applied to our existing models and analyses: 

1. Full scoring on Brazil
Given our existing champion model, all schools outside the featured enumeration areas can now be scored with an estimated level of connectivtiy. This could be done for a sample of schools as a sanity check or for entire Brazil, which would yield a similar map like the Giga Initiative connectivtiy map. 
2. Statistical robustness checks
Especially two steps could be reasonable additions that take the geographic nature of the data into account: Estimating a Geographically Weighted Regression (GWR) and performing spatial cross-validation on the models.
3. Experiment with featured data
The manner in which we used some of the features could be varied. First of all, it could be fruitful to experiment with Facebook data as an alternative target variable. If model performance still remains on an acceptable level, this would render Microdata obsolete and would enable a global extension of our project. Furthermore, pulling OSM school locations for Brazil and applying the model to this sample could yield insights on the representativity of OSM data. Lastly, buffer zones around schools are currently constant in diameter, but could be varied according to specific variables (e.g. population data).  

#### Extension on other countries 
The existing model can be applied to every country, with OSM school location data available. However,model evaluation or model training for other countries requires two more components: Microdata (on household, individual or enumeration area level) and the respective shapefiles/geolocation of the enumeration area. Our analyses have indicated, that analyzing larger geographical aggregates like provinces diminishes model performance and interpretability. An enumeration area is assumed to be a largely homogeneous area, whereas the variation of connectivtiy within e.g. a federal state should be much higher. 

#### Further model training 
With more countries being included to the connectivity analysis, more options of model combinations open up. Given the requirements are met, an individual model can be trained for each country and evaluated separately. In addition, joint models with multiple countries could result in a high predictive power on a global level and increase model robustness. Comparing the performances of combined and single-country models can give insights on the impact of country specific differences. Furthermore, it might be a reasonable idea to train regional models (e.g. a model for South East Asian countries). Actors that are not able to provide enumeration area level microdata (e.g. due to anonymity restrictions) can obtain our provided scripts and additional content and run a custom model training. 

#### Additional data sources

1. Country-level data
When extending the models on multiple countries, it might make sense to include country level variables. Possbile additions could be urbanization rate, GDP, publich spendings on telecommunications or other indices of human/infrastructural development. In doing so, "country-specific intercepts" are featured in the estimation and will assist accounting for differences in overall connectivtiy between countries. 

2. Additional content from survey/school data
The original models we provide have so far only been utilizing the necessarily required features of survey and school data. Too keep our approach as reproducible as possible for many countries we have so far asbtained from using additional information within these data sources. However, usually the survey will contain more connectivity-related variables and items such as more survey questions on telecommunications (e.g reasons for (non-)connectivity), demographic information such as age or gender or information on household size or income. Similarly information in school location data such as pupil count or computer availability could potentially be used in further analyses, e.g. when trying to estimate the feasability of connection for a specific school. 

3. Further data 
Existing models could supposedly be improved by adding more features to the training data. Possible additions could stem from official data provided by ministries/regulators, platform/network/monitoring services like Google, Facebook or Cisco Analytics or (coverage) telecommunication data from telecommunication companies and operators. Nevertheless, at minimum a hypothetical logical connection between feature and target variable should always be existent. 


