# Cognifyz-Technologies-Intership

Determine the top three most common cuisines in the dataset and Calculate the percentage of 
restaurants that serve each of the top cuisines.

import pandas

data = pandas.read_csv('internship dataset.csv')
data.info()
data.head(1)

cuisine_counts = data['Cuisines'].str.split(', ').explode().value_counts()
top_three_cuisines = cuisine_counts.head(3)
print(top_three_cuisines)

total_restaurants = data.shape[0]
top_three_cuisine_percentages = (top_three_cuisines / total_restaurants) * 100
print(top_three_cuisine_percentages)
