Identify the restaurants with the highest and lowest number of votes. 
Analyze if there is a correlation between the number of votes and the rating of a restaurant.


import pandas

# Load the CSV file
data = pandas.read_csv('internship dataset.csv')

# Check the first few rows of the Dataset
print(data.head())

# Check the 'Votes' and 'Rating text' columns are present
if 'Votes' not in data.columns or 'Rating text' not in data.columns:
    raise ValueError("The dataset must contain 'Votes' and 'Rating text' columns.")

# Identify the restaurant with the highest number of votes
restaurant_highest_votes = data.loc[data['Votes'].idxmax()]
print("Restaurant with the highest number of votes:")
print(restaurant_highest_votes)

# Identify the restaurant with the lowest number of votes
restaurant_lowest_votes = data.loc[data['Votes'].idxmin()]
print("\nRestaurant with the lowest number of votes:")
print(restaurant_lowest_votes)

import matplotlib.pyplot as plt
import seaborn as sns

# Assuming `Rating` is in text form, map it to numerical values for comparison
rating_map = {
    'Excellent': 5,
    'Very Good': 4,
    'Good': 3,
    'Average': 2,
    'Poor': 1,
    'Not Rated': 0  # or any default value you prefer for unrated restaurants
}

data['Rating Value'] = data['Rating text'].map(rating_map)

# Ploting the relationship between number of votes and rating
plt.figure(figsize=(10, 6))
sns.scatterplot(data=data, x='Votes', y='Rating Value')
plt.title('Relationship between Number of Votes and Rating')
plt.xlabel('Number of Votes')
plt.ylabel('Rating Value')
plt.show()

# Calculate the correlation between number of votes and rating
correlation = data[['Votes', 'Rating Value']].corr()
print("\nCorrelation between number of votes and rating:")
print(correlation)

