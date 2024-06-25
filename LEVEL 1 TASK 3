Create a histogram or bar chart to visualize the distribution of price ranges among the restaurants.
Calculate the percentage of restaurants In each price range category.


import pandas

data = pandas.read_csv('internship dataset.csv')
data.info()

# extract the price range column
price_ranges = data['Price range']

# define categories (modify this according to your data structure)
price_categories = ['$', '$$', '$$$', '$$$$']

# count the occurrences of each price category
price_counts = price_ranges.value_counts()

# calculate the percentages
total_restaurants = len(price_ranges)
price_percentages = (price_counts / total_restaurants) * 100

# know visualizing by matplotlib

import matplotlib.pyplot as plt

# creating a bar chart

# plt.figure(figsize=(10, 6))
# price_counts.plot(kind='bar', color='skyblue')
# plt.title('Distribution of Price Ranges among Restauran ts')
# plt.xlabel('Price Range')
# plt.ylabel('Number of Restaurants')
# plt.xticks(rotation=0)
# plt.show()

# Display Percentage on the bar chart
plt.figure(figsize=(10, 6))
bars = plt.bar(price_counts.index, price_counts.values, color='skyblue')
# Annotate with percentages
for bar, percentage in zip(bars, price_percentages):
    yval = bar.get_height()
    plt.text(bar.get_x() + bar.get_width()/2, yval + 1, f'{percentage:.1f}%', ha='center', va='bottom')

plt.title('Distribution of Price Ranges among Restaurants')
plt.xlabel('Price Ranges')
plt.ylabel('Number of Restaurants')
plt.xticks(rotation=0)
plt.show()


