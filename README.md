# London Bike Rides Analysis
## Project Overview
This is a Python and Tableau project analyzing london bike analysis. This project aims to provide valuable insights into the seasonal fluctuations of bike rides in London.
The dataset used in this project can be found in Kaggle.

You can interact with the dashboard in tableau public [here](https://public.tableau.com/views/LondonBikeRidesDashboard-1/Dashboard1?:language=en-GB&publish=yes&:display_count=n&:origin=viz_share_link)

![Dashboard](https://github.com/PhilipSada/london-bike-rides-analysis/assets/55988995/b21412b7-867e-44a0-a9a1-e32123731517)



## Data Gathering, Exploration and Manipulation
```python
import pandas as pd
import kaggle
import zipfile
```
```python
#downloading dataset from kaggle using the Kaggle API
!kaggle datasets download -d hmavrodiev/london-bike-sharing-dataset
```
```python
# extracting the file from the downloaded zip file
zipfile_name = 'london-bike-sharing-dataset.zip'
with zipfile.ZipFile(zipfile_name, 'r') as file:
    file.extractall()
```
```python
# reading in the csv file as a pandas dataframe
bikes = pd.read_csv("london_merged.csv")
```
```python
# exploring the data
bikes.info()
```
```python
# counting the unique values in the weather_code column
bikes.weather_code.value_counts()
```
```python
# counting the unique values in the weather_code column
bikes.weather_code.value_counts()
```
```python
# count the unique values in the season column
bikes.season.value_counts()
```
```python
# identifying the column names needed for the analysis
new_cols_dict = {
    'timestamp':'time',
    'cnt':'count', 
    't1':'temp_real_C',
    't2':'temp_feels_like_C',
    'hum':'humidity_percent',
    'wind_speed':'wind_speed_kph',
    'weather_code':'weather',
    'is_holiday':'is_holiday',
    'is_weekend':'is_weekend',
    'season':'season'
}

# renaming the columns to the column names listed in the dictionary above
bikes.rename(new_cols_dict, axis=1, inplace=True)
```

```python
# making the humdity values more understandable by changing it to percentage (i.e. a value between 0 and 1)
bikes.humidity_percent = bikes.humidity_percent / 100
```

```python
# creating a weather dictionary so that we can map the integers to the actual written values making it more readable
weather_dict = {
    '1.0':'Clear',
    '2.0':'Scattered clouds',
    '3.0':'Broken clouds',
    '4.0':'Cloudy',
    '7.0':'Rain',
    '10.0':'Rain with thunderstorm',
    '26.0':'Snowfall'
}

# changing the weather column data type to string
bikes.weather = bikes.weather.astype('str')
# mapping the values to the actual written weathers
bikes.weather = bikes.weather.map(weather_dict)

# creating a season dictionary so that the integers 0-3 can be mapped to the actual written values, making it more readable
season_dict = {
    '0.0':'spring',
    '1.0':'summer',
    '2.0':'autumn',
    '3.0':'winter'
}

# changing the seasons column data type to string
bikes.season = bikes.season.astype('str')
# mapping the values 0-3 to the actual written seasons
bikes.season = bikes.season.map(season_dict)
```

```python
# checking the dataframe to see the modified data
bikes.head()
```

```python
# writing the final dataframe to an excel file which would be used for the tableau visualization
bikes.to_excel('london_bikes_final.xlsx', sheet_name='Data')
```

## Data Analysis and Visualization
Tableau was used for the data analysis and visualization. 

![Dashboard](https://github.com/PhilipSada/london-bike-rides-analysis/assets/55988995/b21412b7-867e-44a0-a9a1-e32123731517)

![Dashboard](https://github.com/PhilipSada/london-bike-rides-analysis/assets/55988995/df8e1e6a-e2a3-418e-8d8e-7ff10a3b334b)

![Dashboard](https://github.com/PhilipSada/london-bike-rides-analysis/assets/55988995/ee23f28b-2f0f-415c-a8dd-777d6b13b6eb)

![Dashboard](https://github.com/PhilipSada/london-bike-rides-analysis/assets/55988995/91c1c777-8b2b-4f4a-b73e-6f7cc763c890)

![Dashboard](https://github.com/PhilipSada/london-bike-rides-analysis/assets/55988995/55c2f3b3-0f63-4bc8-a957-ef34ddd7895a)

The following are some of the key findings:

### a. Peak Activity Months:
The analysis highlighted August of both 2015 and 2016 as the periods with the highest bike ride activities, as indicated by the moving average figures. This suggests a seasonal trend where biking activities surge during the summer months, possibly due to more favorable weather conditions.

### b. Low Activity Periods:
Conversely, the months of January and early February in 2016, as well as January 2017, witnessed significantly lower average bike rides. This decline might be attributed to winter weather conditions, reduced outdoor activities, or potential operational challenges faced by bike rental services during the colder months.

## Recommendations
Based on the analysis provided, the following are recommended to bike rental companies in London:
### a. Seasonal Campaigns:
Promotional Events: Organize special biking events and promotions during peak months to capitalize on the high activity periods. Special events can attract tourists and locals alike, boosting bike ride numbers.
Winter Campaigns: Implement targeted marketing campaigns and discounts during the winter months to encourage biking, despite the weather challenges. Offering winter-specific incentives can attract resilient riders.
### b. Infrastructure Enhancements:
Winter-Friendly Bikes: Introduce winter-specific bikes equipped for colder weather, such as wider tires for better traction. This can make biking a more viable option during the colder months, increasing overall ridership.
Maintenance Emphasis: Ensure bikes are in optimal condition during high-demand periods. Regular maintenance checks become crucial during peak months to prevent service disruptions.
### c. User Engagement:
Customer Feedback: Engage with customers to understand their preferences and challenges during different seasons. Feedback surveys can provide valuable insights into areas needing improvement, allowing for tailored strategies.
Seasonal User Incentives: Offer loyalty rewards and incentives to regular users during both high and low activity periods. Discounts during low seasons can encourage consistent usage despite reduced overall bike rides.
### d. Collaborations and Events:
Tourism Collaborations: Partner with tourism agencies to promote biking as a part of the tourist experience during the peak months. Collaborative efforts can attract tourists, enhancing overall bike ride numbers.
Community Engagement: Organize community events and biking initiatives to engage locals. This fosters a sense of community and promotes biking as a healthy, sustainable transportation option year-round.
