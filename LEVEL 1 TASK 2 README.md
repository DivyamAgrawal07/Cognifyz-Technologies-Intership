Identify the city with the highest number of restaurants in the dataset. Calculate the average rating for
restaurants in each city. Determine the city with the highest average rating.

import numpy 

import pandas

data = pandas.read_csv('internship dataset.csv')
data.info()
data.head(1)

city_counts = data['City'].value_counts()

top_cities = city_counts.head(10)
print(top_cities)


average_rating_per_restaurant = data.groupby('Restaurant Name')['Aggregate rating'].mean()
print(average_rating_per_restaurant.head())

