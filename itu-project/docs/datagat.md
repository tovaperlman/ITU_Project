
# Data Gathering 

Utku did a lot of work on this. Yay Utku!!

## Internal Data
-  Surveys from ITU for Brazil and Thailand
The target variable for our modeling was the proportion of a population around a particular school that was connected to the internet. It therefore ranged from 0-1, with 0 being zero percent connected and 100 being 100% connected to the internet. We chose to measure this on a school level as one of our objectives, through working with UNICEF, was to detect schools that could be connected to the internet and further serve the community they are located. 

Within the Brazil Survey data, we received information on household internet connectivity on an enumeration area level. This presented a slight challenge as the level of granularity of the school data was slightly different from the enumeration data or census tract. Thus, we matched the school points to the enumeration area data. We could not use all the school points as we only had enumeration areas for a specific amount of tracts in Brazil. Thus we had to subset our school points data to around 11,000 points. Once we connected the schools to the enumeration areas we were able to build our training data set from that. 

-  School Points from UNICEF for Brazil
We got the school points in lat, long format from UNICEF for Brazil. Unfortunately, we were not able to obtain the school points for Thailand as well. We thus turned to OpenStreetMap to obtain school points for Thailand. We obtained many school points but filtered them to the schools that we were positive were schools as some were tagged as dance schools or even ATM's. Our school points script is thus specific for obtaining the OSM points. 

## External/Open Source Data

We now have to gather all the open data that we've used:

1. Open Cell ID
2. School Population Points using OSM
3. Satellite data

To see the full code for gather this data, click here. To gather the satellite data, we used Google Earth Engine for Python API. We gathered three different types of data: Global Human Modification Index, Nighttime Data, Normalized Difference Vegetation Index. Our hope with gathering this data is that it would provide an accurate proxy for households and schools with internet connection. If we knew a school was located in a place with a high average radiance, it might also mean there was high internet connectivity. The beauty of satellite data is that its continous for the entire globe. We initially struggled with learning how to crop the data for all the school points we wanted. Eventually, we set a 5 km buffer zone around each school point in both Brazil and Thailand and obtained specific satellite information that was input as a number into the training dataset. Below please find more information on each of the datasets we used.  

1. Global Human Modification Index (String for Image Collection ID is: 'CSP/HM/GlobalHumanModification'):
    - The global Human Modification dataset (gHM) provides a cumulative measure of human modification of terrestrial lands globally at 1 square-kilometer resolution. The gHM values range from 0.0-1.0 and are calculated by estimating the proportion of a given location (pixel) that is modified, the estimated intensity of modification associated with a given type of human modification or "stressor". 5 major anthropogenic stressors circa 2016 were mapped using 13 individual datasets:
       - human settlement (population density, built-up areas)
       - agriculture (cropland, livestock)
       - transportation (major, minor, and two-track roads; railroads)
       - mining and energy production
       - electrical infrastructure (power lines, nighttime lights)
2. NOAA Monthly Nighttime images using the VIIRS Satellite (String for Image Collection ID is: "NOAA/VIIRS/DNB/MONTHLY_V1/VCMSLCFG")
    - Monthly average radiance composite images using nighttime data from the Visible Infrared Imaging Radiometer Suite (VIIRS) Day/Night Band (DNB).

   - As these data are composited monthly, there are many areas of the globe where it is impossible to get good quality data coverage for that month. This can be due to cloud cover, especially in the tropical regions, or due to solar illumination, as happens toward the poles in their respective summer months. Therefore it is recommended that users of these data utilize the 'cf_cvg' band and not assume a value of zero in the average radiance image means that no lights were observed.
3. Normalized Difference Vegetation Index Band from the MODIS dataset (String for Image Collection ID is: 'MODIS/006/MOD13A2'):
    - Normalized Difference Vegetation Index or NDVI measures the vegetation or greenness present on the Earth's surface
    - The algorithm for this product chooses the best available pixel value from all the acquisitions from the 16-day period. The criteria used are low clouds, low view angle, and the highest NDVI/EVI value.
    
Descriptions taken from the Goole Earth Engine Data Catalog.



4. Facebook API data
5. Speedtest Data

## Data Dictionary

Show a table of each of the predictors and what their definitions are:

| Variable Name      | Description                          | Data Source  |
| ----------- | ------------------------------------ |----------------------- |
| `avg_d_kbp3`       | Average Download Speed | Speedtest Data |
| `avg_u_kbps`       | Average Upload Speed | Speedtest Data |
| `estimate_dau`    | Facebook Daily Active Users estimate | Facebook API|
| `estimate_mau`    | Facebook Daily Active Users estimate |Facebook API|
| `population`    | Population within a 1 km buffer zone, estimated with  | Population Data |
| `pop_norm`    | Facebook Daily Active Users estimate | Population Data |
| `mean_ghm`    | Mean Global Human Modification value | Global Human Modification Index |
| `mean_avg_rad`    | Mean value from the Average Radiance band | VIIRS Nighttime DNB |
| `mean_cf_cvg`    | Mean value from the cloud free coverage band |VIIRS Nighttime DNB |
| `slope_year_avg_rad`    | The yearly rate of change between 2019 and 2014 of Average Radiance |VIIRS Nighttime DNB |
| `change_year_avg_rad`    | The change between the average values of 2019 and 2014 of Average Radiance |VIIRS Nighttime DNB |
| `slope_year_cf_cvg`    | The yearly rate of change between 2019 and 2014 from the Cloud Free Coverage Band |VIIRS Nighttime DNB |
| `change_year_cf_cvg`    | The change between the average values of 2019 and 2014 from the Cloud Free Coverage Band |VIIRS Nighttime DNB |
| `slope_month_avg_rad`    | The monthly rate of change between 2019 and 2014 of the Average Radiance Band |VIIRS Nighttime DNB |
| `change_month_avg_rad`    | The change between the average of Dec 2019 and Jan 2014 of the Average Radiance Band |VIIRS Nighttime DNB |
| `slope_month_cf_cvg`    | The monthly rate of change between 2019 and 2014 from the Cloud Free Coverage Band |VIIRS Nighttime DNB |
| `change_month_cf_cvg`    | The rate of change between the average of Dec 2019 and Jan 2014 from the Cloud Free Coverage Band |VIIRS Nighttime DNB |
| `mean_NDVI`    | The average value of the Vegetation Index |MODIS Dataset |
| `slope_year_NDVI`    | The yearly rate of change between 2019 and 2014 of the Vegetation Index |MODIS Dataset |
| `change_year_NDVI`    | The change between 2019 and 2014 of the Vegetation Index |MODIS Dataset |
| `slope_month_NDVI`    | The monthly rate of change between 2019 and 2014 of the Vegetation Index |MODIS Dataset |
| `change_month_NDVI`    | The change between the average of May 2019 and May 2014 of the Vegetation Index |MODIS Dataset |

