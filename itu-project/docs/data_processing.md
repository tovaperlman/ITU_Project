# Instructions to Create Model-Ready Dataset

1. Create an environment from the itu_env.yml file: 'conda env create --name itu --file=path/to/itu_env.yml' -> 'conda activate itu'.

2. To generate a dataframe comprising any target variables and predictors that you wish to use, first set up the use-case configurations in configs.py. Details of the configurable variables and their expected assignments can be found in the 'configurations' section of the documentation.

3. Having correctly set the desired configurations, all you need to do is run 'main.py'. Following this, a dataset for model training and/or application will be saved within a training_sets folder, which is situated within the data directory.
