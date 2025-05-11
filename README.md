# Final-Project-Statistical-Modelling-with-Python

## Project/Goals
The goal of this project was to see if there exists a correlation between specific social venues and the number of bikes available
in the surrounding bike stations.

## Process
### 1. Get bike station information 
- I obtained the list of all the bike stations in Tokyo using the citybik.es API.
- Tokyo had multiple networks running; therefore, I used the DOCOMO network.
- I made an API call, converted the response, and stored the JSON file for exploration.
- Parsed through the JSON file to locate station information.
- Convert desired station information into a dataframe while creating a key column.

### 2. Get POI information 
- Compared Foursquare and Yelp place API result quality for venues located near bike stations using latitude and longitude data from citybik.es API call.
- The responses were then stored in a JSON file and parsed for the POI information. 
- Each call was stored and normalized in a dataframe
- All the normalized dataframes were then concatenated together to make one large df.
- 

### 3. Joined the dataframe and the Regression Model
- joined the dataframes and filtered for the POI of interest
- Made histplots to view relationships between distance and station capacity and distance between IDs.
- The relationships were then run through a linear regression model

## Results

The Yelp API provides more detailed information, such as reviews, ratings, and phone numbers, about each result compared to Foursquare. However, the Yelp results categorization system has discrepancies in how certain establishments are classified. Results for coffee and tea shops were provided when only "bars" were selected in the initial call. The other problem with Yelp is its call request limitations: 1. You can only make 300 calls per day, and 2. You cannot do multiple categories in a single request.

Foursquare has more value for our larger dataset due to the API: 1. having the ability to reselect multiple categories in a single request, 2. having a more robust category classification system that automatically pulls subcategory results that are relevent to the main POI category and 3. able to make larger calls in 1 day. These three features make the geospatial data in Foursquare more useful for statistically significant insights. 

The linear regression model comparing the minimum distance between a bike station and a park did not restrict the number of bikes available at the given station.

OLS Regression Results                            
==============================================================================
Dep. Variable:               capacity   R-squared:                       0.004
Model:                            OLS   Adj. R-squared:                  0.003
Method:                 Least Squares   F-statistic:                     5.960
Date:                Wed, 07 May 2025   Prob (F-statistic):             0.0147
Time:                        18:48:03   Log-Likelihood:                -5877.5
No. Observations:                1574   AIC:                         1.176e+04
Df Residuals:                    1572   BIC:                         1.177e+04
Df Model:                           1                                         
Covariance Type:            nonrobust                                         
==============================================================================
                 coef    std err          t      P>|t|      [0.025      0.975]
------------------------------------------------------------------------------
const         10.3169      0.492     20.985      0.000       9.353      11.281
distance       0.0037      0.001      2.441      0.015       0.001       0.007
==============================================================================
Omnibus:                     1125.829   Durbin-Watson:                   1.933
Prob(Omnibus):                  0.000   Jarque-Bera (JB):            18190.585
Skew:                           3.216   Prob(JB):                         0.00
Kurtosis:                      18.362   Cond. No.                         631.
==============================================================================

The second linear regression model tackled the relationship between the number of park IDs and the minimum distance to a bike station. This yielded a higher R-squared value of 0.09, but it is still not significant enough to warrent the financial decision of changing the bike capacity of each station. 

OLS Regression Results                            
==============================================================================
Dep. Variable:                 fsq_id   R-squared:                       0.090
Model:                            OLS   Adj. R-squared:                  0.089
Method:                 Least Squares   F-statistic:                     152.9
Date:                Sat, 10 May 2025   Prob (F-statistic):           1.46e-33
Time:                        15:29:12   Log-Likelihood:                -4403.0
No. Observations:                1552   AIC:                             8810.
Df Residuals:                    1550   BIC:                             8821.
Df Model:                           1                                         
Covariance Type:            nonrobust                                         
==============================================================================
                 coef    std err          t      P>|t|      [0.025      0.975]
------------------------------------------------------------------------------
const         12.7853      0.195     65.566      0.000      12.403      13.168
distance      -0.0063      0.001    -12.365      0.000      -0.007      -0.005
==============================================================================
Omnibus:                       52.854   Durbin-Watson:                   1.947
Prob(Omnibus):                  0.000   Jarque-Bera (JB):               57.430
Skew:                           0.462   Prob(JB):                     3.38e-13
Kurtosis:                       3.180   Cond. No.                         717.
==============================================================================


## Challenges 
The main challenge was devising a logic to simultaneously parse through the JSON file structures and normalize the records into tabular data for exploration analysis.

## Future Goals
An overlay of the Tokyo area with the station coordinates grouped on the city's 23 wards parameters would further refine the inquiry to which ward has a stronger relationship between its average number of parks and its average number of station bikes. This would help overcome the multiple individual observations that are causing the large and small data values to cancel each other out.