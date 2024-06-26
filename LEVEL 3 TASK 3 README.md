Analyze if there is a relationship between the price range and the availability of online
delivery and table booking. Determine if higher-priced restaurants are more 
likely to offer these services.


import pandas

# Load the CSV file into a DataFrame
data = pandas.read_csv('internship dataset.csv')

# Check the first few rows of the DataFrame to understand its structure
print(data.head())

# Ensure the necessary columns are present
required_columns = ['Price range', 'Has Online delivery', 'Has Table booking']
for column in required_columns:
    if column not in data.columns:
        raise ValueError(f"The dataset must contain '{column}' column.")

# Convert 'Has Online delivery' to a binary variable (1 for 'Yes', 0 for 'No')
data['Has Online delivery'] = data['Has Online delivery'].apply(lambda x: 1 if x == 'Yes' else 0)

# Calculate the percentage of restaurants offering online delivery in each price range
online_delivery_by_price_range = data.groupby('Price range')['Has Online delivery'].mean() * 100

print("Percentage of restaurants offering online delivery by price range:")
print(online_delivery_by_price_range)

# Convert 'Has Table booking' to a binary variable (1 for 'Yes', 0 for 'No')
data['Has Table booking'] = data['Has Table booking'].apply(lambda x: 1 if x == 'Yes' else 0)

# Calculate the percentage of restaurants offering table booking in each price range
table_booking_by_price_range = data.groupby('Price range')['Has Table booking'].mean() * 100

print("\nPercentage of restaurants offering table booking by price range:")
print(table_booking_by_price_range)

import matplotlib.pyplot as plt
import seaborn as sns

# Plot the percentage of restaurants offering online delivery by price range
plt.figure(figsize=(10, 5))
sns.barplot(x=online_delivery_by_price_range.index, y=online_delivery_by_price_range.values)
plt.title('Percentage of Restaurants Offering Online Delivery by Price Range')
plt.xlabel('Price Range')
plt.ylabel('Percentage')
plt.show()

# Plot the percentage of restaurants offering table booking by price range
plt.figure(figsize=(10, 5))
sns.barplot(x=table_booking_by_price_range.index, y=table_booking_by_price_range.values)
plt.title('Percentage of Restaurants Offering Table Booking by Price Range')
plt.xlabel('Price Range')
plt.ylabel('Percentage')
plt.show()
