# DataScience_Activity3

# Air Quality Analysis in NYC 

## Overview

The goal is to analyze air quality data collected from low-cost sensors mounted on moving vehicles in New York City. Using the concepts learned in the chapters on Sampling and Empirical Distributions , Testing Hypotheses , and Estimation , statistical analysis was performed in order to estimate pollution levels, test hypotheses about differences in pollution across neighborhoods, and construct confidence intervals for key parameters. The analysis was conducted using Google Colab.

## Data used

Datasets used are:

- Air Quality Sensor Readings (NYC_PM.csv) :
Attributes: SensorID, time, temperature, humidity, pm25,
Focus attributes: temperature, humidity, pm1,pm25,pm10,
- City Polygons (nyc_polygon.geojson) :
Contains polygons representing neighborhoods or boroughs in NYC.
Used for spatially joining geographic information with air quality data.

## Usage

Libraries and modules used include:

```python
import pandas as pd
import geopandas as gpd
import numpy as np
import matplotlib.pyplot as plt

from datascience import *
%matplotlib inline
path_data = '../../../assets/data/'
import matplotlib.pyplot as plt
plt.style.use('fivethirtyeight')
import numpy as np
```

Key steps performed for data analysis:

1. Reading the CSV file containing PM sensor readings and Read the GeoJSON file containing neighborhood boundaries into a GeoDataFrame

```python
# Step 1: Read the CSV file containing PM10 sensor readings
pm10_data = pd.read_csv('https://raw.githubusercontent.com/IsamAljawarneh/datasets/master/data/NYC_PM.csv',index_col=False)

# Step 2: Read the GeoJSON file containing neighborhood boundaries into a GeoDataFrame
nyc_neighborhoods = gpd.read_file('https://raw.githubusercontent.com/IsamAljawarneh/datasets/master/data/nyc_polygon.geojson')
```

2. Converting the csv into a geodataframe and join it (sjoin) with the geojson, assign a coordinate reference system (CRS) the csv geodataframe which is identical to that of the geojson file, then perform the join, the result is a geodataframe, convert it to dataframe, and select pm10, neighborhood columns in a new dataframe

```python
pm10_gdf = gpd.GeoDataFrame(pm10_data, geometry=gpd.points_from_xy(pm10_data.longitude, pm10_data.latitude))
merged_data = gpd.sjoin(pm10_gdf, nyc_neighborhoods, how='inner', predicate='within')
```

3. Conversion of data from a pandas dataframes to numpy tables

Dataframes were frequently converted to numpy tables for table abstractions. For example:

```python
merged_table = Table().from_df(merged_data)
```

## Key Insights

- Comparison between sampling and empirical distributions of pm10 levels

- Estimation of the median pm10 value using the bootstrapping technique

- Testing hypotheses using confidence intervals

- Trends in air pollution (pm10) levels across neighborhoods

## Author

Nour Eddin Abdulsalam Alchmri
U24200614
