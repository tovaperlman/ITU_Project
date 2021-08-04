# Feature Engineering

Having retrieved data of many different types, at different geospatial resolutions, from an array of different sources, it was necessary to develop a robust and comprehensive feature engineering pipeline, which produces clean datasets, ready for model application.

## Data Cleaning

* `Numerical Variables` - Impute missing values as variable median.
* `Categorical Variables` - Fill missing values with 'missing' label; perform one-hot encoding.

## Target Variable

* `Brazil` - A4A
* `Thailand` - H107

## Joining Locations

The map_feature method within the FeatureEngineering class, is used to perform a spatial join between school locations and the locations at which values of each feature are defined. In essence, we are finding the correct value of each feature at each given school location. To do so, we first ensure that the dataframe corresponding to each feature collection is loaded as a geodataframe, with an appropriately defined 'geometry' column. From here, we define a variable 'centroids'. If the feature's geometry is a polygon, or multipolygon, centroids is indeed defined as a list of the associated centroids. If the feature's geometry is already in point form, centroids is automatically defined as a list of these points. If, instead, the feature's geometry is defined by latitude and longitude columns, rather than a single geometry column, this will be handled appropriately, so long as these column names are exactly 'latitude' and 'longitude', or 'lat' and 'lon'.

For the unexpected instance in which schools have already been matched to feature values, we look for a 'source_school_id' column and merge the school data to the feature data according to these school ids. 

The build_tree method is then called to implement Scikit-learn's KDTree package and thus build a kd tree of the previously defined centroids.This tree is then queried with the school locations to get the nearest neighbours, with the query returning dist (geographic distance) and ind (index associated with this location). The rows in the school_data dataframe are then assigned the correct values for each new column. For any variable named 'range', such as the mobile cell tower range variable from the OpenCellID dataset, values are converted to a 0 or 1, corresponding to range > dist and range <= dist respectively. 

It should be noted that the map_feature method should only be used for features that span the majority of a country.

## Features Used