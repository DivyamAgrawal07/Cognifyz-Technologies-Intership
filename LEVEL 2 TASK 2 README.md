Identify the most common combinations of cuisines in the dataset.
Determine if certain cuisine combinations tend to have higher ratings.

import pandas
from itertools import combinations
from collections import Counter

# Load the CSV file into a DataFrame
data = pandas.read_csv('internship dataset.csv')

# Check the first few rows of the DataFrame to understand its structure
print(data.head())

# Handle any NaN values in the 'Cuisines' column
data['Cuisines'] = data['Cuisines'].fillna("")

# Create a list of lists where each inner list contains cuisines of a restaurant
cuisines_list = data['Cuisines'].str.split(', ')

# Count combinations of cuisines
combinations_count = Counter()
for cuisines in cuisines_list:
    if len(cuisines) > 1:  # Only consider restaurants with more than one cuisine
        for combo in combinations(sorted(cuisines), 2):  # Change `2` to `3` for triple combinations, etc.
            combinations_count[combo] += 1

# Get the most common combinations
most_common_combinations = combinations_count.most_common(10)  # Adjust `10` to show more or fewer combinations

print("Most common cuisine combinations:")
for combo, count in most_common_combinations:
    print(f"{', '.join(combo)}: {count} restaurants")

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

# Calculate average ratings for each cuisine combination
average_ratings_by_combination = {}
for combo, _ in most_common_combinations:
    combo_str = ', '.join(combo)
    subset_df = data[data['Cuisines'].apply(lambda x: all(cuisine in x.split(', ') for cuisine in combo))]
    if not subset_df.empty:
        average_rating = subset_df['Rating Value'].mean()
        average_ratings_by_combination[combo_str] = average_rating

# Print average ratings for each cuisine combination
print("\nAverage ratings for each cuisine combination:")
for combo_str, avg_rating in average_ratings_by_combination.items():
    print(f"{combo_str}: {avg_rating:.2f}")
