# FloodP rediction

---
### 1.0 Introduction

The purpose of this report is to forecast the next potential flood date in Lagos by analyzing historical precipitation data and applying statistical modeling methods. Accurately predicting floods is essential for reducing their adverse effects on lives and property of residents in Lagos state.

This data contains 7357 rows and  34 columns.

---
# 2.0 Data Collection and Preprocessing
## 2.1 Data sources
The following data set were collected:
Historical precipitation data from meteorological stations in Lagos from here
Flood occurrence data (dates of past floods) were gotten from social media platforms such as X(formerly Twitter)

## 2.2 Data preprocessing
### Missing values: 
Some of the variables in the data set have missing values in them. These were tackled using forward fill because they are continuous variables. Here are some of the variables which were filled using forward fill:
Temperature (temp, tempmax, tempmin)
Humidity
Wind Speed and Direction
Cloud Cover
Visibility
Sea Level pressure
Dew 
Cumulative precipitation
 The means of these attributes were calculated and used to fill the null values using the .fillna() method as shown below.

tempmin_mean = lagos['tempmin'].mean()
tempmin_mean
#### Fill the empty cells in the 'tempmin' column
lagos['tempmin'] = lagos['tempmin'].fillna(tempmin_mean)
Convert date column to proper date format: The date format was changed from “MM/DD/YYYY” format to “DD/MM/YYYY using pandas, making the days of the week to appear first.
#### Convert the datetime column to a proper datetime format
lagos['datetime'] = pd.to_datetime(lagos['datetime'], dayfirst=True, errors='coerce')

  ### 2.3 Define flood threshold
The flood threshold was defined so as to be 200 mm in 7 days so as to identify potential flood locations.
This was done Using the lagos['cumulative_precip'] column, which represents the cumulative precipitation data over time, the script calculates whether the cumulative precipitation meets or exceeds the defined flood threshold of 200 mm.

The column shown in a new boolean column is_flood in the lagos dataset. Each entry in this column is True if the cumulative precipitation at that time point equals or exceeds 200 mm, indicating a potential flood event; otherwise, it is False.

#### Define flood threshold (example: 200 mm in 7 days)
flood_threshold = 200
lagos['is_flood'] = lagos['cumulative_precip'] >= flood_threshold


---
## 3.0  Exploratory Data Analysis (EDA)
  ### 3.1 Precipitation analysis
  
The link graph shows precipitation over the years from 2002 till 2024. Over the years, the threshold exceeded 200 mm which showed the potential occurrence of flood in Lagos state over these years. The threshold was exceeded first around 2005-2006, and then again around 2012 with a precipitation of 300 mm. 

  ### 3.2 Historical flood analysis

The above chart is a histogram which shows the flood occurrence. It shows that floods mostly occurred in the year 2023. These years experience precipitation above 200 mm. The earlier years had lower precipitation than recent years.

  ### 3.3 Seasonal variation

The figure above illustrates the average precipitation by month. The average precipitation by month is more in the month of June (6), then May (5), and lastly, July(7). 

---
## 4.0  Model selection

	 ### 4.1 Feature selection:
Some of the features selected from this data set include: 
Temp max
Temp min
Feels like max
Feels like min
Dew
Humidity
Wind speed
Wind direction
Sea Level pressure
Cloudcover
Cumulative precipitation

#### Feature selection
features = lagos[['cumulative_precip','tempmax', 'tempmin','feelslikemax',
       'feelslikemin','dew', 'humidity','windspeed', 'winddir','sealevelpressure', 'cloudcover']].shift(1).dropna()
target = lagos['flood occurrence'][1:]
	
### 4.2 Model training

Here, the machine learning model to be used here is logistics regression. This is because the prediction for this instance involves a “yes” or “no” prediction. 

The model.score was used to check for its accuracy after fighting the variables into the model. It shows that the model has a 99.39% accuracy which is very good as 80% is the common threshold for many.

---
## 5.0 Prediction and Justification

There is no flood expected in the near future because the recent weather data shows that the amount of rain and other weather conditions are not severe enough to cause flooding. This means the rainfall and other factors like humidity and wind are within normal ranges, so a flood is unlikely to happen soon.

--- 
## 6.0 Conclusion
The logistic regression model uses historical weather data to predict the likelihood of a flood on the next day. This prediction helps in making informed decisions about flood preparedness and response. Regular updates and model improvements, along with continuous monitoring of weather conditions, are essential to enhance the accuracy and reliability of flood predictions.

---
# The End




