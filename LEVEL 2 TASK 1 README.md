Analyze the distribution of aggregate ratings and determine the most common rating range.
Calculate the average number of votes received by restaurants.


import pandas

# Load the CSV file into a DataFrame
data = pandas.read_csv('internship dataset.csv')

# Check the first few rows of the DataFrame to understand its structure
print("First few rows of the DataFrame:")
print(data.head())

# Define a mapping from text ratings to numeric values
rating_map = {
    'Excellent': 5,
    'Very Good': 4,
    'Good': 3,
    'Average': 2,
    'Poor': 1,
    'Not Rated': 0
}

# Map the text ratings to numeric values
data['Numeric_Rating'] = data['Rating text'].map(rating_map)

# Analyze the distribution of aggregate ratings
rating_distribution = data['Rating text'].value_counts().sort_index()

# Determine the most common rating range
bins = [0, 1, 2, 3, 4, 5, 6]
labels = ['Not Rated', 'Poor', 'Average', 'Good', 'Very Good', 'Excellent']
data['Rating_Range'] = pandas.cut(data['Numeric_Rating'], bins=bins, labels=labels, include_lowest=True)

# print("\nRating Ranges after binning:")
# print(data['Rating_Range'].value_counts())

most_common_rating_range = data['Rating_Range'].value_counts().idxmax()

print("\nRating Distribution:")
print(rating_distribution)

print(f"\nThe most common rating range is {most_common_rating_range}.")

# Calculate the average number of votes received by restaurants
average_votes = data['Votes'].mean()

print(f"\nThe average number of votes received by restaurants is {average_votes:.2f}.")

