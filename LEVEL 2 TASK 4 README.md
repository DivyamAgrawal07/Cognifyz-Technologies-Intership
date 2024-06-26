Identify if there are any restaurant chains present in the dataset.
Analyze the ratings and popularity of different restaurant chains.

import pandas

# Load the CSV file into a DataFrame
data = pandas.read_csv('internship dataset.csv')

# Check the first few rows of the DataFrame to understand its structure
print(data.head())

# Identify restaurant chains by counting the occurrences of each restaurant name
restaurant_counts = data['Restaurant Name'].value_counts()
chains = restaurant_counts[restaurant_counts > 1]

print("Restaurant chains:")
print(chains)

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

# Calculate average ratings for each restaurant chain
chain_ratings = data[data['Restaurant Name'].isin(chains.index)].groupby('Restaurant Name')['Rating Value'].mean()

print("\nAverage ratings of restaurant chains:")
print(chain_ratings)

# Calculate the number of locations for each restaurant chain (popularity)
chain_popularity = data[data['Restaurant Name'].isin(chains.index)].groupby('Restaurant Name').size()

print("\nPopularity of restaurant chains (number of locations):")
print(chain_popularity)

# Combine ratings and popularity into a single DataFrame
chain_analysis = pd.DataFrame({
    'Average Rating': chain_ratings,
    'Number of Locations': chain_popularity
})

print("\nAnalysis of restaurant chains:")
print(chain_analysis)

# Sort by number of locations and then by average rating for better analysis
chain_analysis_sorted = chain_analysis.sort_values(by=['Number of Locations', 'Average Rating'], ascending=[False, False])

print("\nSorted analysis of restaurant chains:")
print(chain_analysis_sorted)
