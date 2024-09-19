# Accident-Prone Zones in Australia: Data Analysis and Classification

## Introduction

This project aims to identify and classify accident-prone zones across various states in Australia, using historical road crash data. The primary objective is to develop predictive models that can classify zones as `Low`, `Mid`, or `High` risk based on several factors, including accident frequency, severity, environmental conditions, and road characteristics.

## Data Collection

### Overview of Data Sources

The datasets used in this project were collected from multiple sources, representing road crash data from the five most populous states in Australia:

- **New South Wales (NSW):** Dataset obtained from [Transport for NSW Open Data](https://opendata.transport.nsw.gov.au/dataset/nsw-crash-data)
- **Queensland (QLD):** Dataset obtained from [Queensland Government Open Data](https://www.data.qld.gov.au/dataset/crash-data-from-queensland-roads)
- **South Australia (SA):** Dataset obtained from [Data SA](https://data.sa.gov.au/data/dataset/road-crash-data)
- **Victoria (VIC):** Dataset obtained from [Victoria Government Open Data](https://discover.data.vic.gov.au/dataset/victoria-road-crash-data)
- **Western Australia (WA):** Dataset obtained from [Main Roads Western Australia](https://portal-mainroads.opendata.arcgis.com/datasets/mainroads::crash-information-last-5-years/explore)

### Data Description

- **NSW Data:** Contains crash records from 2018 to 2022, with information on the date, time, location, severity, and environmental conditions.
- **QLD Data:** Covers crash data from 2019 to 2022, including geographical locations, road conditions, and crash severity.
- **SA Data:** Merges multiple datasets, including road crashes, geographical information, and road characteristics, spanning from 2019 to 2022.
- **VIC Data:** A combination of crash data and additional information on atmospheric conditions and road surfaces, covering the period from 2019 to 2022.
- **WA Data:** Provides detailed records of crashes from the last five years, including speed limits, crash types, and environmental factors.

## Data Cleaning and Preprocessing

### New South Wales (NSW)

- **Date and Time Conversion:** The crash date and time were standardized to ISO 8601 format and 24-hour time.
- **Geographical Classification:** Areas were categorized into `City`, `Metropolitan`, and `Country` based on conurbation data.
- **Location Type:** Classified as either `Intersection` or `Midblock` based on distance and road names.
- **Environmental Conditions:** Light and weather conditions were standardized, with unknown values removed.

### Queensland (QLD)

- **Date and Time Standardization:** Converted crash date and time to uniform formats, with missing values handled.
- **Geographical Classification:** Areas classified based on ABS remoteness categories.
- **Location Identification:** Roads were classified into `Intersection` or `Midblock`, and precise locations were determined using road names.
- **Environmental Conditions:** Light and weather conditions were cleaned and standardized, with unknown entries removed.

### South Australia (SA)

- **Multiple Dataset Integration:** Combined road crash data with geographical information from a GeoJSON file to obtain latitude and longitude.
- **Location Classification:** Location types were classified based on position types, and intersections were identified using road names.
- **Environmental and Speed Conditions:** Standardized light, weather, and speed limit data, ensuring consistency across records.

### Victoria (VIC)

- **Merging Multiple Datasets:** Combined crash data with atmospheric and road surface conditions, ensuring consistency in accident records.
- **Date and Time Processing:** Crash dates and times were standardized, and data was filtered to include records from 2019 to 2022.
- **Geographical and Location Data:** Areas were classified, and locations were identified using road names and intersection types.
- **Environmental and Speed Data:** Conditions were cleaned, standardized, and missing values were handled.

### Western Australia (WA)

- **Date and Time Conversion:** Crash dates and times were processed to ensure uniformity, with missing values handled appropriately.
- **Geographical and Speed Data:** Merged crash data with legal speed limits and geographical information to classify areas and set speed limits.
- **Location and Environmental Data:** Locations were identified and classified, and environmental conditions were cleaned and standardized.

## Data Merging and Standardization

After cleaning the individual datasets, they were merged into a single comprehensive dataset:

- **Standardized Column Names:** All column names were standardized to lowercase with underscores for consistency.
- **Combined Dataset:** The cleaned datasets from NSW, QLD, SA, VIC, and WA were merged into a unified dataset, ensuring compatibility across all fields.

## Data Clustering and Analysis

### Clustering of Accident-Prone Zones

- **Feature Selection:** Relevant features, such as accident count, severity, light conditions, and speed limits, were selected for clustering.
- **Scaling:** Features were scaled using standardization to ensure uniformity in clustering.
- **Elbow Method and Silhouette Score:** These methods were used to determine the optimal number of clusters, with `k=3` being selected.
- **K-Means Clustering:** Applied to classify accident-prone zones into `Low`, `Mid`, and `High` risk categories.

### Visualization

- **Cluster Visualization:** The clusters were visualized on an interactive map using Folium, with color coding for different risk levels.
- **Heatmap:** A heatmap was added to the map to represent accident density, providing a visual understanding of high-risk areas.

## Model Development and Evaluation

### Model Selection

Three machine learning models were developed to classify accident-prone zones:

- **Random Forest Classifier**
- **Support Vector Machine (SVM)**
- **Gradient Boosting Classifier**

### Model Training and Evaluation

- **Training and Testing Split:** The data was split into training and testing sets, with the training set used for model fitting and the test set reserved for evaluation.
- **Cross-Validation:** Models were evaluated using cross-validation to ensure robustness and prevent overfitting.
- **Metrics:** Models were assessed using accuracy, balanced accuracy, recall, precision, F1 score, and confusion matrices.

### Best Model Selection

The Gradient Boosting Classifier emerged as the best model, with the highest balanced accuracy, recall, and precision.

### Test Set Evaluation

The Gradient Boosting model was evaluated on the test set, achieving high performance, consistent with cross-validation results.

### Feature Importance Analysis

For the best model (Gradient Boosting), feature importance was analyzed to understand the most influential factors:

- **Accident Count:** The most critical feature.
- **Speed Limits:** Significant in determining accident-prone zones.
- **Environmental Conditions:** Played a role but were less influential than accident counts and speed limits.

## Conclusion

The project successfully developed a predictive model for classifying accident-prone zones in Australia. The Gradient Boosting Classifier was identified as the best-performing model, with high accuracy and reliability. The insights gained from feature importance analysis provide valuable information for policymakers to enhance road safety by targeting high-risk areas.
