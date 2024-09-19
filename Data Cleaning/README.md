# Data Cleaning Process for Identifying and Categorizing Accident-Prone Zones in Australia

## Introduction

This project focuses on identifying and categorizing accident-prone zones across various Australian states by analyzing historical crash data. The datasets used were collected from open government sources, covering the states of New South Wales (NSW), Queensland (QLD), Victoria (VIC), Western Australia (WA), and South Australia (SA). This `.md` file outlines the data cleaning and preparation steps applied to each state's dataset, ensuring consistency across the combined dataset used for analysis.

---

## Data Sources

Below are the datasets collected for each state:

- **New South Wales (NSW)**: [NSW Crash Data 2018-2022](https://opendata.transport.nsw.gov.au/dataset/nsw-crash-data) – Crash records, including crash time, date, location, and severity, from 2018 to 2022.
  
- **Queensland (QLD)**: [Crash Data from Queensland Roads](https://www.data.qld.gov.au/dataset/crash-data-from-queensland-roads) – A dataset that includes details about crashes across Queensland from 2019 to 2022.

- **Victoria (VIC)**: [Victoria Road Crash Data](https://discover.data.vic.gov.au/dataset/victoria-road-crash-data) – A GeoJSON dataset with detailed crash data, including road types, accident severity, and location information.

- **Western Australia (WA)**: [Crash Information (Last 5 Years)](https://portal-mainroads.opendata.arcgis.com/datasets/mainroads::crash-information-last-5-years/explore) and [Legal Speed Limits](https://portal-mainroads.opendata.arcgis.com/datasets/mainroads::legal-speed-limits/about) – Data on crashes, road conditions, and speed limits.

- **South Australia (SA)**: [SA Road Crash Data 2019-2023](https://data.sa.gov.au/data/dataset/road-crash-data), [Road Crashes GeoJSON](https://data.sa.gov.au/data/dataset/road-crashes/resource/78d24425-6c14-426e-8895-d414c2a12521), and [SA Roads Data](https://data.sa.gov.au/data/dataset/roads/resource/e0c742b7-0762-48f3-8d4f-27a877d98baa) – Crash data across South Australia from 2019 to 2023, including crash locations, severity, and road infrastructure.

---

## Data Cleaning Process

### New South Wales (NSW)

1. **Data Loading**:
   - The dataset was loaded from the NSW Road Crash Data Excel file.

2. **Filtering**:
   - We filtered the data to include only records from 2019 to 2022.
   - Rows with unknown crash times were removed.

3. **Date and Time Standardization**:
   - A new column `crash_date_time` was created using the crash date and two-hour intervals to standardize crash time across records.
   - The `day`, `month`, and `year` columns were extracted from the crash date.

4. **Geospatial Processing**:
   - The `stats_area` column was created to categorize regions into City, Metropolitan, and Country zones using the `Conurbation 1` field.
   
5. **Location and Lighting Conditions**:
   - The `loc_type` (Intersection or Midblock) and `location` columns were derived based on crash details.
   - Lighting conditions were standardized into "Day" or "Night," and rows with unknown values were removed.

6. **Weather Conditions**:
   - Weather conditions were categorized into "Raining" or "Not Raining."
   - Unknown values were removed.

7. **Severity**:
   - The crash severity was classified into four levels: Fatal, Serious Injury, Minor Injury, and Property Damage Only (PDO).

---

### Queensland (QLD)

1. **Data Loading**:
   - The crash data was loaded from a CSV file obtained from Queensland Government.

2. **Date and Time Processing**:
   - Crash year, month, day, and time were extracted from the relevant fields and standardized.

3. **Geospatial Processing**:
   - The `stats_area` column was derived from the `Loc_ABS_Remoteness` field to categorize regions into City, Metropolitan, or Country.

4. **Location and Lighting Conditions**:
   - The `loc_type` and `location` columns were created from road and intersection data.
   - The lighting conditions were mapped to "Day" or "Night" based on crash time.

5. **Weather Conditions**:
   - Weather conditions were standardized, and rows with unknown values were removed.

6. **Severity**:
   - Crash severity levels were mapped into four categories.

---

### Victoria (VIC)

For Victoria, I used two datasets to compile the final crash data:
1. **[Victoria Road Crash Data](https://discover.data.vic.gov.au/dataset/victoria-road-crash-data)**: This GeoJSON dataset provided the main crash data, including road names, severity, and crash location.
   
2. **[ACCIDENT_LOCATION](https://discover.data.vic.gov.au/dataset/victoria-road-crash-data/resource/ACCIDENT_LOCATION.csv)** and **[ATMOSPHERIC_COND](https://discover.data.vic.gov.au/dataset/victoria-road-crash-data/resource/ATMOSPHERIC_COND.csv)**: These datasets provided additional details about accident locations and weather conditions.

#### Data Cleaning Steps:

1. **Data Loading and Merging**:
   - The crash data was loaded from the GeoJSON file, and accident location and atmospheric conditions datasets were merged using the `ACCIDENT_NO` field.

2. **Date and Time Standardization**:
   - I created `year`, `month`, `day`, and `time` columns from the accident date and time fields.
   - Data was filtered to include records from 2019 to 2022.

3. **Geospatial Processing**:
   - The `stats_area` column was derived from the `DEG_URBAN_NAME` field to categorize regions as City, Metropolitan, or Country.

4. **Location and Speed Limits**:
   - The `location` and `loc_type` columns were created from road and intersection data.
   - Speed limits were cleaned by removing non-numeric characters and converting values to integers.

5. **Weather and Lighting Conditions**:
   - Weather conditions were standardized based on the `ATMOSPH_COND_DESC` field, and unknown values were removed.
   - Lighting conditions were standardized into "Day" and "Night."

6. **Severity**:
   - Crash severity was classified into four categories: Fatal, Serious Injury, Minor Injury, and PDO.

7. **Final Data Cleanup**:
   - The final cleaned dataset was saved as `Final_VIC.csv`.

---

### South Australia (SA)

In South Australia, I utilized three datasets to compile the final crash data for analysis:
1. **[SA Road Crash Data 2019-2023](https://data.sa.gov.au/data/dataset/road-crash-data)**: This dataset provided the primary crash data, including crash date, time, severity, and general location.
   
2. **[Road Crashes GeoJSON](https://data.sa.gov.au/data/dataset/road-crashes/resource/78d24425-6c14-426e-8895-d414c2a12521)**: This dataset contained detailed geospatial information (latitude and longitude) for crash locations. 

3. **[SA Roads Data](https://data.sa.gov.au/data/dataset/roads/resource/e0c742b7-0762-48f3-8d4f-27a877d98baa)**: This dataset provided additional road infrastructure details, such as road names and intersections, which were crucial for categorizing crash locations.

#### Data Cleaning Steps:

1. **Data Loading**:
   - I loaded the main crash dataset from CSV and the geospatial data from the Road Crashes GeoJSON file.

2. **Merging Data**:
   - I merged the crash dataset with the GeoJSON file on the common `UNIQUE_LOC` column to extract latitude and longitude information.
   - I further merged the resulting data with the SA Roads dataset to include road names and specific intersection details.

3. **Date and Time Processing**:
   - Crash date and time were standardized to create `year`, `month`, `day`, and `time` columns.
   - Data was filtered to include only records from 2019 to 2022.

4. **Geospatial Processing**:
   - Latitude and longitude were extracted from the `geometry` column.
   - The `stats_area` column was created by classifying regions as City, Metropolitan, or Country based on the crash location.

5. **Location and Lighting Conditions**:
   - The `location` and `loc_type` columns were derived from road and intersection details using the merged datasets.
   - Lighting conditions were standardized into "Day" and "Night."

6. **Weather and Speed Limits**:
   - Weather conditions were standardized, and unknown values were removed.
   - Speed limits were extracted from the SA Roads dataset and cleaned for consistency.

7. **Final Data Cleanup**:
   - I removed rows with missing `latitude`, `longitude`, and `lga` values to ensure complete and accurate records.
   - The final dataset was saved as `Final_SA.csv`.

---

### Western Australia (WA)

1. **Data Loading and Merging**:
   - Crash data was loaded from the WA crash dataset, and speed limits were merged using the `ROAD_NO` field.

2. **Date and Time Standardization**:
   - Crash date and time were parsed to create year, month, day, and time columns.
   - Data was filtered to include records from 2019 to 2022.

3. **Geospatial Processing**:
   - The `stats_area` column categorized regions based on the `RA_NAME` field, mapping them into City, Metropolitan, or Country zones.

4. **Location and Lighting Conditions**:
   - The `location` and `loc_type` columns were derived from crash data, and lighting conditions were standardized into "Day" and "Night."

5. **Weather Conditions**:
   - Weather data was fetched using the Meteostat API, which provided daily weather information based on latitude and longitude coordinates for each crash.
   - A parallelized fetching mechanism was implemented for efficiency, with fallback mechanisms for missing data.

6. **Severity**:
   - Crash severity levels were mapped into four categories: Fatal, Serious Injury, Minor Injury, and PDO.

7. **Final Data Cleanup**:
   - The final dataset was saved as `Final_WA.csv`.

---

## Combining Datasets

Once the individual datasets for each state were cleaned and standardized, the following steps were taken:

1. **Standardization of Column Names**:
   - Column names were made consistent across datasets by converting them to lowercase, replacing spaces with underscores, and ensuring uniformity.

2. **Concatenation**:
   - The datasets from all five states were concatenated into a single dataset for Australia-wide analysis.

3. **Final Data Cleanup**:
   - Any remaining blank or irrelevant columns were removed, and the final dataset was saved for further analysis.

4. **Final Dataset**:
   - The final cleaned dataset was saved as `Road_Crash_Data.csv`, which includes fields such as `report_id`, `year`, `month`, `day`, `time`, `state`, `stats_area`, `location`, `loc_type`, `latitude`, `longitude`, `speed_limit`, `light_cond`, `weather_cond`, and `csef_severity`.

---

## Conclusion

The data cleaning process involved multiple stages of standardization, merging, and feature extraction to ensure consistency across datasets from different states. The final dataset is ready for further geospatial analysis and machine learning tasks to identify accident-prone zones across Australia.
