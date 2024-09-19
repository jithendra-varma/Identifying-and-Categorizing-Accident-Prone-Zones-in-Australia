# Data Preprocessing for Accident-Prone Zones Analysis

## Introduction

This project aims to identify accident-prone zones across Australia by analyzing historical road crash data from multiple states. The goal is to process and clean the data to enable clustering and further analysis, identifying patterns that can inform road safety measures. This document details the comprehensive steps taken to preprocess the datasets, including data cleaning, transformation, encoding, and aggregation.

## Data Collection and Loading

The dataset was collected from various sources, each corresponding to different Australian states. These datasets were merged into a single file named `Road_Crash_Data.csv`. The data includes multiple features such as crash severity, location, weather conditions, time of the accident, and more.

### Data Sources:
- **New South Wales**: Data sourced from [Transport for NSW](https://opendata.transport.nsw.gov.au/dataset/nsw-crash-data).
- **Victoria**: Data sourced from [Victoria State Government](https://discover.data.vic.gov.au/dataset/crash-stats-data-extract).
- **Queensland**: Data sourced from [Queensland Government](https://www.data.qld.gov.au/dataset/crash-data-from-queensland-roads).
- **South Australia**: Data sourced from [Government of South Australia](https://data.sa.gov.au/data/dataset/road-crash-data).
- **Western Australia**: Data sourced from [Main Roads Western Australia](https://portal-mainroads.opendata.arcgis.com/datasets/mainroads::crash-information-last-5-years/explore).

### Key Data Columns:
- **year**: Year in which the accident occurred.
- **month**: Month of the accident.
- **day**: Day of the week.
- **time**: Time of the accident.
- **location**: The specific location where the accident occurred.
- **light_cond**: The lighting condition at the time of the accident (e.g., Day, Night).
- **weather_cond**: Weather conditions during the accident (e.g., Raining, Not Raining).
- **speed_limit**: Speed limit at the crash location.
- **csef_severity**: Severity of the crash, categorized into various levels (e.g., Fatal, Serious Injury).
- **latitude** and **longitude**: Geospatial coordinates of the accident location.

## Data Cleaning

### Dropping Irrelevant Columns

To simplify the dataset and focus on relevant features, we removed columns that were unnecessary for analysis, such as `report_id`, which served as a unique identifier but was not needed for clustering or pattern recognition.

### Handling Mixed Data Types and Missing Values

The datasets contained mixed data types and some missing values. These issues were addressed by:
- Ensuring consistent data types across columns (e.g., converting all date and time fields to a standard format).
- Handling missing values through imputation or removal, depending on the significance of the missing data.

## Feature Engineering and Encoding

### Month and Day Encoding

#### Why Encode `month` and `day` Columns?

Both `month` and `day` are categorical variables representing temporal aspects of the data. Machine learning models typically require numerical inputs, so these categorical values were converted into numerical formats.

- **Month Encoding**: The `month` column was mapped from its string format (e.g., "January", "February") to numerical values (e.g., 1 for January, 2 for February).
- **Day Encoding**: The `day` column was transformed into a binary feature representing whether the day was a weekday or weekend, providing insight into accident patterns based on the day type.

### Encoding Time into One-Hour Intervals

#### Purpose

Time data can be complex to analyze at a granular level. By converting time into one-hour intervals, we simplify the dataset and enhance the ability to identify patterns related to specific times of day, such as rush hours or late-night periods.

- **Office Hours Encoding**: The time data was further categorized into "Office Hours" (9 AM to 6 PM) and "Non-Office Hours" to explore differences in accident frequencies during these periods.

## Categorical Feature Encoding

One-hot encoding was applied to several categorical features, including `loc_type` (location type), `light_cond` (lighting conditions), and `weather_cond` (weather conditions). This conversion allowed these categorical variables to be represented numerically, facilitating their use in clustering algorithms.

### Example Encoded Features:
- **loc_type_Intersection**: Indicates whether the accident occurred at an intersection.
- **light_cond_Day**: Indicates whether the accident occurred during daylight.
- **weather_cond_Raining**: Indicates whether the accident occurred during rain.

## Speed Limit Standardization

#### Rationale

Speed limits were represented by various values across the datasets. For consistency, similar speed limits were grouped together. For example, low-speed zones (e.g., 10 km/h, 20 km/h) were combined into a single category, and all speed limits were converted to integers.

## Aggregating Data by Location

### Latitude and Longitude Rounding

To aggregate accidents occurring in close proximity, the latitude and longitude values were rounded to three decimal places. This allowed us to group accidents that happened at nearly the same location.

### Location Aggregation

The data was aggregated by location to calculate summary statistics for each site, such as:
- **accident_count**: Total number of accidents at the location.
- **average_severity**: Average severity of accidents at the location.
- **is_weekday_mean**: Proportion of accidents occurring on weekdays.
- **is_office_hours_mean**: Proportion of accidents occurring during office hours.
- **weather_cond_mean**: Proportion of accidents under different weather conditions (e.g., raining).

### Cleaning and Standardizing Location Names

Location names were cleaned to ensure consistency. This involved converting all names to lowercase and replacing "and" with "&". Additionally, locations containing invalid entries like "nan" were removed.

## Final Data Preparation and Export

The cleaned and aggregated data was saved to a new file, `merged_locations.csv`, which includes all relevant features for further analysis and clustering.

### Final Output:
- **Total Accidents**: 156,694 accidents were included in the final dataset after cleaning and aggregation.
- **File Location**: The final aggregated data has been saved to `merged_locations.csv`.

## Conclusion

This preprocessing workflow meticulously cleaned and transformed the raw crash data into a structured format. By addressing issues like mixed data types, missing values, and inconsistent formatting, we ensured that the dataset is ready for clustering and analysis. These preprocessing steps are essential for producing reliable, insightful results in the subsequent analysis phases.
