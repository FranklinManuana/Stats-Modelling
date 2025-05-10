# Final-Project-Statistical-Modelling-with-Python

## Project/Goals
The goal of this project was to see if there exists a correlation between specific social venues and the number of bikes available
in the surrounding bike stations.

## Process
### 1. Get bike station information 
Part 1.
- Obtained the list of all the bike stations for tokyo using the citybik.es API.
- Multiple networks were are used in tokyo, therefore used the docomo network.
- Made API call, converted response and stored JSON file for exploration.
- Parsed through JSON file to locate station information.
- Convert desired station information into dataframe while creating key column.

### 2.Get POI information 
- Obtained searched for venues surroundingt the docomo bike stations using their geospatial coordinates( latitude and longitude).
- A multiple API calls were done to obtain to figure out which venues are around each station 
- The responses were then stored in a JSON file and parsed for the venue information. 
- Each call was stored was normalized and stored in a dataframe
- all the normalized dataframes were then concatenated together to make one large df.
- 

### 3. Joined dataframe and Regression Model
- joined the dataframes and filtered for POI of interest
- Made histplots to view relationships between distance and station capacity and distance between id.
- The relationships were then ran through a linear regression model

## Results

The yelp API provides has more detailed information such as reviews, ratings,phone numbers about each result compared to foursquare. However, the yelp results categorization system has discrepancies in how certain establishments are classified. Results for coffee and tea shops were provided when only "bars" were selected in the initial call. The other problem with yelp is in its call request limitations: 1.only able to make 300 per day 2. unable to do multiple categories in a single request.

Foursquare has more value for our larger dataset due to the API: 1. having the ability to reselect multiple categories in a single request, 2. having a more robust category classification system that automatically pulls subcategory results that are relevent to the main POI category and 3. able to make larger calls in 1 day. These 3 features make the geospacial data in foursquare more useful for statistically significant insights. 

The linear regression model between the minimum distance between a bike station and a park had no barring on the number of bikes available at the given station. 

The second linear regression model tackled the relationship between the nubmer of park ids and the minimum distance to a bike station. This yielded a higher R-squared value of 0.09 however still not enough to be statistically signficant. 


## Challenges 
The main challenge was devising a logic to simulatineously parse through the JSON file structures and normalize the records into tabular data for exploration analysis.

## Future Goals
An overlay of the tokyo area with the station coordinates to grouped on the city's 23 wards parimeters. This wouldfurther refine the inquiry to which ward has a stronger relationship between it's average number of parks average number of station bikes. This would help overcome the  multiple individual observations that is causing the large and small data values from canceling each other out.