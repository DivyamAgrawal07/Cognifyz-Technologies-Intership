Determine the percentage of restaurants that offer online delivery.
Compare the average ratings of restaurants with and without online delivery.

import pandas

# load the csv file into a dataframe
data = pandas.read_csv('internship dataset.csv')

# check the first few row
print(data.head())

# determine the total no. of restaurants
total_restaurants = data.shape[0]

# determine the percentage of restaurants that offer online delivery
online_delivery_counts = data['Has Online delivery'].value_counts()
percentage_online_delivery = (online_delivery_counts['Yes'] / total_restaurants) * 100

print(f'Percentage of restaurants that offer online delivery: {percentage_online_delivery:.2f}%')

# convert text ratings to numeric values for comparison
rating_map = {
    'Excellent': 5,
    'Very Good': 4,
    'Good': 3,
    'Average': 2,
    'Poor': 1,
    'Not Rated': 0
}

data['Rating Value'] = data['Rating text'].map(rating_map)

# compare the average rating of restaurants with and without online delivery
average_rating_online = data[data['Has Online delivery'] == 'Yes']['Rating Value'].mean()
average_rating_no_online = data[data['Has Online delivery'] == 'No']['Rating Value'].mean()

print(f'Average rating of restaurants with online delivery: {average_rating_online:.2f}')
print(f'Average rating of restaurants without online delivery: {average_rating_no_online:.2f}')





