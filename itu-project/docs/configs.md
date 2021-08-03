# Configurations

We use configs.py to store the variable configurations that should be changed according to use-case:

* `WD` - Working Directory, e.g. '../../../files/'
* `AVAILABLE_COUNTRIES` - Countries for which survey data with an internet connectivity ground truth variable is available, e.g. list('bra', 'tha')
* `COUNTRY` - Country code for current use-case, e.g. 'tha'
* `FEATURES` - List of predictive features for use-case, e.g. list('speedtest', 'opencell', 'facebook', 'population', 'nightlight', 'ndvi')
