# OBJECTIVE
To build a predictive machine learning model which predicts the next hour's electricity demand.
# DATASETS
## We were provided with the following datasets:
- ### PGCB_date_power_demand.xlsx: 
   Contains demand and generation data at different time on different days 
- ### weather_data.xlsx: 
   Contains environmental data (eg; temperature, humidity etc.)
- ### economic_full_1.csv: 
   World Bank data containing varios macroeconomic indicators.  
# WORKFLOW
1. ## EDA
- We perform EDA on raw data to undestand the basic characteristics such as
  shape , data type (of columns) of different datasets

- We sort the datetime column and detect that how many unique differences 
between two consecutive datetime exist so that we can check how irregular 
timestamp frequency is.

- Also, we use **.describe()** to get some idea about the outliers majorly in 
*'demand_mw'* and *'generation_mw'* column.
2. ## DATA CLEANING
-  We remove the duplicate entries and set the timestamp frequency as 1 hour.

- It includes dealing with missing values. The columns that have a large amount of
  missing values are dropped and remaining missing values are dealt by using **.ffill()**
  which fills the missing values by the prvious value.

- We use IQR (Interquantile method) method to remove the spikes in the data.
3. ## FEATURE ENGINEERING
- We create lag features (*l1*, *l2*, *l24*, *l168* etc.) which store the demand 1 hour ago, 2 hour ago, 1  day ago, 1 week ago respectively. This is very helpful as electricity demand is highly periodic.

- Rolling mean featurea are also created.

- SUitable columns from the economic and weather dataset are now merged with the demand datatset.
4. ## EDA
- Some basic EDA is now performed on the organised dataset to understand how different features influence
  the target(value to be predicted.).
5. ## MODEL TRAINING
- We use Random Forest Regressor to train the model.

- Values prior to 2024 are used to train the dataset and the values after 2024 are used to evaluate the    model.
6. ## MODEL EVALUATION 
- We use Mean Absolute Percentage Error (MAPE) to evaluate the model.

- Model achieved approximately 3.9% MAPE.

# FEATURE IMPORTANCE
1. The feature *generation_mw* has the largest influence on the electricity demand. Lag features also  significantly influence the demand.

2. If we train the model without *generatioon_mw* feature, the MAPE value increases to approx. 5.5% and *l1* is now the most influencing feature.

3. ### 10 most influencing features are:
  
 -  generation_mw                     
 -  l1                                
 -  load_shedding                     
 -  sunshine_duration (s)             
 -  solar                             
 -  l3                                
 -  rolling_24                        
 -  l2                                
 -  soil_temperature_0_to_7cm (°C)    
 -  l24                               
