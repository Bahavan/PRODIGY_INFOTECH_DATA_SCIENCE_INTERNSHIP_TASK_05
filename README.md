# PRODIGY_INFOTECH_DATA_SCIENCE_INTERNSHIP_TASK_05

# Task-05: Traffic Accident Data Analysis

## Task Description
Analyze traffic accident data to identify patterns related to road conditions, weather, and time of day. Visualize accident hotspots and contributing factors.

## Dataset
You can access the **US Traffic Accident Analysis** dataset from Kaggle here:  
[US Traffic Accident EDA](https://www.kaggle.com/code/harshalbhamare/us-accident-eda)

## Instructions
1. **Download the dataset** from Kaggle.
2. **Load the dataset** using `pandas`.
3. **Data Preprocessing**:
   - Handle missing values.
   - Convert date-time columns to proper formats.
   - Filter relevant features like road conditions, weather, and time of the accident.
4. **Exploratory Data Analysis (EDA)**:
   - Identify accident frequency by location, time, and weather conditions.
   - Find accident-prone areas (hotspots) using geospatial data visualization.
5. **Data Visualization**:
   - Use heatmaps and scatter plots to display accident hotspots.
   - Create time-series plots for accident trends.
   - Analyze the correlation between accidents and factors like weather or time of day.

## Requirements
- Python 3.x
- Libraries:
  - `pandas`
  - `numpy`
  - `matplotlib`
  - `seaborn`
  - `folium` (for map visualization)
  - `geopandas`
  - `plotly`

## Example Code
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import folium
from folium.plugins import HeatMap

# Load dataset
df = pd.read_csv("us_accidents.csv")  # Replace with actual file name

# Convert date column to datetime format
df['Start_Time'] = pd.to_datetime(df['Start_Time'])

# Extract time-based features
df['Hour'] = df['Start_Time'].dt.hour
df['DayOfWeek'] = df['Start_Time'].dt.day_name()

# Visualizing accident trends over time
plt.figure(figsize=(10,5))
sns.histplot(df['Hour'], bins=24, kde=True)
plt.title("Accidents Distribution by Hour of Day")
plt.xlabel("Hour")
plt.ylabel("Number of Accidents")
plt.show()

# Heatmap of accident hotspots
m = folium.Map(location=[df['Start_Lat'].mean(), df['Start_Lng'].mean()], zoom_start=5)
heat_data = list(zip(df['Start_Lat'], df['Start_Lng']))
HeatMap(heat_data).add_to(m)
m.save("accident_hotspots.html")
