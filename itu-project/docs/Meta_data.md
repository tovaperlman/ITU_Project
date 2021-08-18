# Meta Data Information

## Folder Structure
Below is the folder structure for the Github Repository. All of the notebooks and scripts are organized within the below folder structure and data is inputted with relative file paths. Therefore, once you set your own working directory, everything within should run on its own. 

- files/
  - src/
    - scripts/
      - configs.py
      - main.py
      - data_pipeline.py
      - country.py
      - opendata.py
      - school.py
      - survey.py
      - opendata_facebook.py
      - opendata_scrap.py
  - data/
    - geodata/
    - school_loc/
    - enumeration_area/
    - fb/
    - opencellid/
    - satellite/
    - speedtest/
    - survey/
    - training_sets/
    - worldpop/
  - notebooks/
    - Model_Application.ipynb
    - Model_Comparison.ipynb
    - Satellite_Data_EDA.ipynb
    - Training_Data_EDA.ipynb
    - Training_Light_GBM.ipynb
    - Training_Random_Forest.ipynb
    - Training_Random_Forest_Classifier.ipynb
    - Training_XGBoost.ipynb
  - model/
    - RF_model.sav
    - xgboost_model.pkl
  - conf/
    - model_config.yaml
    - predict_config.yaml
  

## Configurations

We use configs.py within the scripts folder to store the variable configurations that should be changed according to use-case:

* `WD` - Working Directory, e.g. '../../../files/'
* `AVAILABLE_COUNTRIES` - Countries for which survey data with an internet connectivity ground truth variable is available, e.g. list('bra', 'tha')
* `COUNTRY` - Country code for current use-case, e.g. 'tha'
* `FEATURES` - List of predictive features for use-case, e.g. list('speedtest', 'opencell', 'facebook', 'population', 'satellite'). This exemplary list contains each of the five open data sources we have used and they must be sytactically entered as shown.

## Data Dictionaries

Data dictionaries should be created for each predictor and survey dataset. Dictionaries for the open-source data and Brazilian, Thai and Philippino survey data already exist and should be located in the data/meta/ folder. 

An exemplary data dictionary (for speedtest data) is shown below:

| Number      | Name      | Description                        | Type     | Binary     | Role         | Use     | Comment               |
| ----------- | ---------- | ----------------------------------- | ----------- | ----------- | --------------- | ----------- | ----------------------- |
| 1       | `avg_d_kbps` | The average download speed of all tests performed in the tile, represented in kilobits per second | num | N | predictor | Y | mbps can also be used |
| 2       | `avg_u_kbps` | The average upload speed of all tests performed in the tile, represented in kilobits per second | num | N | predictor | Y | mbps can also be used |
| 3       | `avg_lat_ms` | The average latency of all tests performed in the tile, represented in milliseconds | num | N | predictor | N | |
| 4       | `tests` | The number of tests taken in the tile | num | N | predictor | N | |
| 5       | `devices` | The number of unique devices contributing tests in the tile | num | N | predictor | N | |