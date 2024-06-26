Plot the locations of restaurants on a map using longitude and latitude
coordinates. Identify any patterns or clusters of restaurants in specific areas.

import pandas
import folium
from folium.plugins import MarkerCluster

# Load the CSV file into a DataFrame
data= pandas.read_csv('internship dataset.csv')

# Check the first few rows of the DataFrame to understand its structure
print(data.head())

# Ensure the 'Longitude' and 'Latitude' columns are present
if 'Longitude' not in data.columns or 'Latitude' not in data.columns:
    raise ValueError("The dataset must contain 'Longitude' and 'Latitude' columns.")

# Create a map centered around an average location
map_center = [data['Latitude'].mean(), data['Longitude'].mean()]
mymap = folium.Map(location=map_center, zoom_start=12)

# Add a marker cluster to the map
marker_cluster = MarkerCluster().add_to(mymap)

# Add points to the marker cluster
for idx, row in data.iterrows():
    if pandas.notna(row['Latitude']) and pandas.notna(row['Longitude']):
        folium.Marker(
            location=[row['Latitude'], row['Longitude']],
            popup=row['Cuisines']
        ).add_to(marker_cluster)

# Save the map to an HTML file
mymap.save('restaurants_map.html')

# Display the map in a Jupyter Notebook (if you're using one)
#mymap  # Uncomment this line if using Jupyter Notebook
