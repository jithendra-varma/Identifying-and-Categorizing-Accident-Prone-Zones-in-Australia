# Data Clustering Process for Identifying Accident-Prone Zones

## Introduction

In this section, we employ clustering techniques to identify accident-prone zones across various locations. The aim is to group locations with similar characteristics based on accident data and assign a risk level (Low, Mid, or High) to each zone. The clustering process uses KMeans clustering, followed by an analysis of the optimal number of clusters using the Elbow method and Silhouette Score. We also visualize the clusters on an interactive map and analyze the zone distribution through heatmaps and bar plots.

---

## Data Loading and Feature Selection

We start by loading a pre-processed dataset from the file `merged_locations.csv`, which contains aggregated accident data for each location. The `Lat_Long_Rounded` column provides the latitude and longitude for each location in a rounded format, which we use for geospatial visualizations later on. 

### Key Data Fields:
- **Latitude** and **Longitude**: Extracted from the `Lat_Long_Rounded` column for mapping purposes.
- **Accident Count**: The number of accidents that occurred in each location.

### Data Filtering:
We filter the data to include only locations where the accident count is greater than 1 to focus on areas with more significant accident activity.

---

## Feature Scaling

The features used for clustering are scaled using the `StandardScaler` from `sklearn`. This ensures that all features contribute equally to the clustering process. The scaling step is essential for KMeans, which relies on distance metrics and can be biased if features are not standardized.

---

## Elbow Method and Silhouette Score

To determine the optimal number of clusters, we use two techniques:

1. **Elbow Method**: This method involves running KMeans clustering for different values of `k` (number of clusters) and plotting the inertia (sum of squared distances from each point to its assigned cluster center). The point where the inertia curve begins to flatten (forming an elbow) suggests the optimal number of clusters.

2. **Silhouette Score**: This score measures how well each point fits within its assigned cluster. A higher silhouette score indicates better-defined clusters. We calculate the silhouette score for each value of `k` greater than 1.

### Plots:
- **Inertia vs. Number of Clusters**: This plot helps us visualize the Elbow Method.
- **Silhouette Score vs. Number of Clusters**: This plot helps determine the best value for `k` in terms of cluster separation.

---

## Clustering with KMeans

Based on the Elbow Method and Silhouette Score, we choose an optimal number of clusters, `k = 3`. KMeans clustering is then applied with this value of `k`, and each location is assigned to one of the three clusters.

### Cluster Ranking:
The accident count is used to rank the clusters:
- **Low Risk (1)**: Areas with the lowest average accident count.
- **Mid Risk (2)**: Areas with a moderate accident count.
- **High Risk (3)**: Areas with the highest accident count.

These rankings are mapped back into the dataset under the column `accident_prone_zone_rating`.

---

## Visualization of Clusters

### 1. **Interactive Map**:
We visualize the clusters on an interactive map using the `folium` library:
- **Low Risk Zones**: Displayed in blue with smaller circle markers.
- **Mid Risk Zones**: Displayed in orange with medium-sized markers.
- **High Risk Zones**: Displayed in red with the largest markers.

Each marker on the map shows the accident-prone rating (Low, Mid, or High) in a popup.

### 2. **Heatmap**:
We also create a heatmap layer that shows the density of accidents across all locations with more than one accident.

---

## Data Analysis and Visualization

### 1. **Bar Plot for Zone Distribution**:
We generate a bar plot that shows the number of locations categorized as Low, Mid, or High risk zones. This provides a quick visual of how the locations are distributed across the three clusters.

### 2. **Feature Analysis by Zone Rating**:
We further analyze how different features contribute to the classification of Low, Mid, and High-risk zones. The features considered include:
- **Average Severity**: The average severity of accidents in each zone.
- **Day/Night Conditions**: Whether most accidents occurred during the day or at night.
- **Weather Conditions**: Whether the accidents were influenced by raining or clear weather conditions.
- **Speed Limits**: Whether the majority of accidents occurred in areas with speed limits ≤ 60 km/h or higher than 60 km/h.

### Heatmap:
We plot a heatmap that compares the average values of these features across Low, Mid, and High-risk zones. This provides insight into the factors that influence accident risk in different areas.

---

## Results

### 1. **Cluster Assignments**:
Each location in the dataset is assigned a cluster (Low, Mid, or High risk) based on the number of accidents and associated features.

### 2. **Accident-Prone Zone Ratings**:
The final dataset includes a column `accident_prone_zone_rating`, which labels each location as Low, Mid, or High risk.

### 3. **Visual Insights**:
The interactive map and heatmaps provide a clear visual representation of where the most dangerous accident zones are located and what factors are contributing to the accident risk in each area.

---

## Conclusion

By applying KMeans clustering, we successfully categorized accident-prone zones into Low, Mid, and High-risk areas. The interactive map and heatmaps offer valuable insights into the spatial distribution of accidents and the factors contributing to accident severity in different regions. This process can aid traffic safety authorities in targeting high-risk areas for safety interventions.
