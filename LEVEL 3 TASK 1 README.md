Analyze the text reviews to identify the most common positive and negative keywords.
Calculate the average length of reviews and explore if there is a relationship between
review length and rating.


import pandas

from collections import Counter

# import re

# Load the CSV file into a DataFrame
data = pandas.read_csv('internship dataset.csv')

# Check the first few rows of the DataFrame to understand its structure
print(data.head())

# # Ensure the 'Reviews' and 'Rating text' columns are present
# if 'Reviews text' not in df.columns or 'Rating text' not in df.columns:
#     raise ValueError("The dataset must contain 'Reviews' and 'Rating text' columns.")

# import nltk

from nltk.corpus import stopwords

from nltk.tokenize import word_tokenize

# nltk.download('punkt')
# nltk.download('stopwords')

# Tokenize the reviews
data['Tokens'] = data['Reviews text'].apply(word_tokenize)

# Remove stopwords
stop_words = set(stopwords.words('english'))
data['Tokens'] = data['Tokens'].apply(lambda tokens: [word for word in tokens if word not in stop_words])

# Identify common words in positive and negative reviews
positive_reviews = data[data['Rating text'].isin(['Excellent', 'Very Good', 'Good'])]['Tokens']
negative_reviews = data[data['Rating text'].isin(['Poor', 'Average'])]['Tokens']

positive_words = [word for tokens in positive_reviews for word in tokens]
negative_words = [word for tokens in negative_reviews for word in tokens]

positive_word_counts = Counter(positive_words)
negative_word_counts = Counter(negative_words)

# Get the most common positive and negative words
common_positive_words = positive_word_counts.most_common(10)
common_negative_words = negative_word_counts.most_common(10)

print("Most common positive words:", common_positive_words)
print("Most common negative words:", common_negative_words)

# Assigning the length to reviews
review_length = {
     'Excellent': 1,
     'Very Good': 2,
     'Good': 1,
     'Average': 1,
     'Poor': 1,
     'Not Rated': 0
}
data['Review Length'] = data['Rating text'].map(review_length)

# Calculate the length of each review
data['Review Length'] = data['Reviews text'].apply(lambda x: len(x.split()))

# Calculate the average length of reviews
average_review_length = data['Review Length'].mean()
print("Average review length:", average_review_length)

import matplotlib.pyplot as plt

import seaborn as sns

# Map textual ratings to numerical values for comparison
rating_map = {
    'Excellent': 5,
    'Very Good': 4,
    'Good': 3,
    'Average': 2,
    'Poor': 1,
    'Not Rated': 0  # or any default value you prefer for unrated restaurants
}

data['Rating Value'] = data['Rating text'].map(rating_map)

# Plot the relationship between review length and rating
plt.figure(figsize=(10, 6))
sns.scatterplot(data=data, x='Review Length', y='Rating Value')
plt.title('Relationship between Review Length and Rating')
plt.xlabel('Review Length')
plt.ylabel('Rating Value')
plt.show()

# Calculate the correlation between review length and rating
correlation = data[['Review Length', 'Rating Value']].corr()
print("Correlation between review length and rating:")
print(correlation)
