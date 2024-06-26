Plot the locations of restaurants on a map using longitude and latitude
coordinates. Identify any patterns or clusters of restaurants in specific areas.

import pandas as pd
import folium
from folium.plugins import MarkerCluster

# Load the CSV file into a DataFrame
df = pd.read_csv('internship dataset.csv')

# Check the first few rows of the DataFrame to understand its structure
print(df.head())

# Ensure the 'Longitude' and 'Latitude' columns are present
if 'Longitude' not in df.columns or 'Latitude' not in df.columns:
    raise ValueError("The dataset must contain 'Longitude' and 'Latitude' columns.")

# Create a map centered around an average location
map_center = [df['Latitude'].mean(), df['Longitude'].mean()]
mymap = folium.Map(location=map_center, zoom_start=12)

# Add a marker cluster to the map
marker_cluster = MarkerCluster().add_to(mymap)

# Add points to the marker cluster
for idx, row in df.iterrows():
    if pd.notna(row['Latitude']) and pd.notna(row['Longitude']):
        folium.Marker(
            location=[row['Latitude'], row['Longitude']],
            popup=row['Cuisines']
        ).add_to(marker_cluster)

# Save the map to an HTML file
mymap.save('restaurants_map.html')

# Display the map in a Jupyter Notebook (if you're using one)
#mymap  # Uncomment this line if using Jupyter Notebook
