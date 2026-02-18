# Weather Analytics Dashboard

Real-time Power BI dashboard with live API integration for Norwegian weather data. Automated data refresh with no manual updates required.

## Overview

Dynamic weather analytics system connected directly to external weather API, displaying 7-day forecasts for six Norwegian cities: Oslo, Bergen, Stavanger, Trondheim, Arendal, and Molde.

## Architecture

```
Weather API --> Power Query (M) --> Data Model --> DAX Measures --> Visualizations
     |               |                  |              |                |
  Live JSON      Transform &        Star Schema    Temperature      Cards, Gauges,
   Endpoint      Parse Data         Modeling       Wind, Rain       Charts, Maps
```

## Technical Implementation

### 1. API Integration

Direct connection to external Weather API via custom Power Query functions. Data refreshes automatically without manual intervention.

```m
// Power Query API call pattern
let
    Source = Json.Document(Web.Contents(apiUrl & city & apiKey)),
    // Transform nested JSON structure
in
    Result
```

### 2. Data Processing (Power Query M)

- JSON parsing and flattening
- Multi-city data handling
- Variable extraction and type conversion
- Scalable architecture for additional cities

### 3. Data Model

**Dimensions:**
- Cities (city_id, name, latitude, longitude)
- Calendar (date, day_name, week, month)

**Facts:**
- Weather Data (city_id, date, temperature, humidity, pressure, wind_speed, precipitation_chance, air_quality)
- Forecasts (city_id, forecast_date, predicted_temp, predicted_conditions)

### 4. DAX Measures

Custom calculations for weather analytics:

```dax
// Temperature analysis
Avg Temperature = AVERAGE(Weather[temperature])
Temp Change = [Current Temp] - [Previous Day Temp]
Max Temperature = MAX(Weather[temperature])
Min Temperature = MIN(Weather[temperature])

// Wind analysis
Avg Wind Speed = AVERAGE(Weather[wind_speed])
Max Wind Gust = MAX(Weather[wind_gust])

// Precipitation
Rain Probability = AVERAGE(Weather[precipitation_chance])
Total Precipitation = SUM(Weather[precipitation_mm])

// Air Quality
AQI Index = AVERAGE(Weather[air_quality_index])
```

## Dashboard Components

### KPI Cards
- Current Temperature
- Humidity Level
- Atmospheric Pressure

### Gauges
- Wind Speed (with thresholds)
- Air Quality Index (color-coded)

### Charts
- Line Chart: Temperature trend over 7 days
- Bar Chart: Precipitation probability by day
- Comparison: Cross-city temperature analysis

### Filters
- City selector
- Date range
- Metric type

## Cities Covered

| City | Region |
|------|--------|
| Oslo | Eastern Norway |
| Bergen | Western Norway |
| Stavanger | Southwestern Norway |
| Trondheim | Central Norway |
| Arendal | Southern Norway |
| Molde | Northwestern Norway |

## Features

**Real-Time Data:**
- Live API connection
- Automatic refresh on schedule
- No manual data updates required

**Scalability:**
- Easily add new cities
- Configurable API parameters
- Modular query structure

**Analytics:**
- Temperature trend analysis
- Air quality monitoring
- Wind speed tracking
- Precipitation forecasting
- Cross-city comparison

## Use Cases

- **Transportation:** Route planning based on weather conditions
- **Energy Management:** Demand forecasting based on temperature
- **Emergency Preparedness:** Severe weather monitoring
- **Event Planning:** Outdoor activity scheduling
- **Agriculture:** Precipitation and temperature tracking

## Technical Stack

| Component | Technology |
|-----------|------------|
| Visualization | Power BI Desktop |
| Data Extraction | Power Query (M Language) |
| API | External Weather API |
| Calculations | DAX |
| Data Format | JSON |

## Configuration

To use this dashboard:

1. Obtain API key from weather data provider
2. Update API key parameter in Power Query
3. Configure refresh schedule in Power BI Service
4. Add/remove cities as needed

## Data Refresh

- Scheduled refresh via Power BI Service
- On-demand refresh available
- API rate limits respected

## Author

Kesara Rathnasiri
