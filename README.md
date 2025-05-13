# Final-Project-Statistical-Modelling-with-Python

## Project/Goals
The goal of this project was to see if there exists a correlation between social venues namely, parks, and the number of bikes available
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
- A refined request Foursquare request was made to for POI (parks, cafes, bars) 
- Each call was stored and normalized in a dataframe
- All the normalized dataframes were then concatenated together to make one large df.

### 3. Joined the dataframe and the Regression Model
- joined the dataframes and filtered for parks.
- Made histplots to view relationships between distance and station capacity and distance between number of locations with park ids.
- The relationships were then run through a linear regression model

## Results
The Yelp API provides more detailed information, such as reviews, ratings, and phone numbers, about each result compared to Foursquare. However, the Yelp results categorization system has discrepancies in how certain establishments are classified. Results for coffee and tea shops were provided when only "bars" were selected in the initial call. The other problem with Yelp is its call request limitations: 1. You can only make 300 calls per day, and 2. You cannot do multiple categories in a single request.

Foursquare has more value for our larger dataset due to the API: 1. having the ability to reselect multiple categories in a single request, 2. having a more robust category classification system that automatically pulls subcategory results that are relevent to the main POI category and 3. able to make larger calls in 1 day. These three features make the geospatial data in Foursquare more useful for statistically significant insights. 

The linear regression model comparing the minimum distance between a bike station and a parkgenerated a R-squared value of 0.004, a F-statistic of 5.960. Theses values show that park distance did not affect the number of bikes available at the given station.

The second linear regression model tackled the relationship between the number of park IDs and the minimum distance to a bike station. This yielded a higher R-squared value of 0.09, F-statistic of 152.9. Both models show that parks have little influence on bike stations. The current results don't warrent any financial decisions to change the current bike distribution network. 


## Challenges 
The main challenge was devising a logic to simultaneously parse through the JSON file structures and normalize the records into tabular data for exploration analysis.

## Future Goals
An overlay of the Tokyo area with the station coordinates grouped on the city's 23 wards parameters and allow for locality specific features that may play a more sigificant role in the bike station capacity distribution. 