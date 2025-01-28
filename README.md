# Insights-from-a-real-air-bnb-data-set
https://insideairbnb.com/get-the-data/#:~:text=New%20York%20City-,calendar.csv.gz,-Detailed%20Calendar%20Data 
#### I have done all the calculations based on data from New York
![image](https://github.com/user-attachments/assets/c681a4b0-2b57-4900-a73e-f2fc106dfb64)

# 🧑‍💻 Let’s bring in the calendar file
```python
import pandas as pd
calendar = pd.read_csv('/Users/hudasaleh/Downloads/calendar.csv.gz')
```
![image](https://github.com/user-attachments/assets/73ba9bde-0aa9-41e1-954b-09766bb81711)

# Questions you may wish to explore regarding the provided data.
##### Let`s dive into exciting insights!

```python
calendar.available.value_counts()
```
![image](https://github.com/user-attachments/assets/a55fbdaf-14f4-4b1b-aa07-a900f4f92ae3)

# Purpose: Compute the percentage of available (t) and unavailable (f) dates.

* Explanation:
* value_counts(normalize=True) gives proportions.
* Multiplying by 100 converts the proportions into percentages

```python
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
![image](https://github.com/user-attachments/assets/0813d6ad-3915-417c-9cb6-bd319e22d2d8)

# Identify the busiest day! 🚩
##### Hint: We will be counting the most unavailable days (given by f)
```python
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
![image](https://github.com/user-attachments/assets/3ef9cf70-c3e7-4f5e-8c2d-8d8ccc8bda67)

# Create a bar graph to visualize the percentage of room availability.
```python
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['green', 'red'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```
![image](https://github.com/user-attachments/assets/d210d397-cdb6-4e96-b038-006d998ee765)

# Visualize the day with the highest activity.
``` python
busiest_dates.head(10).plot(kind='bar', color='orange')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
![image](https://github.com/user-attachments/assets/d933442f-deda-4da1-994d-c594b76c0ed7)


# 📄 Download listings dataset of New York from
https://insideairbnb.com/get-the-data/#:~:text=New%20York%20City-,listings.csv,-Summary%20information%20and
``` python
import pandas as pd
listings = pd.read_csv('/Users/hudasaleh/Downloads/listings.csv')
```
![image](https://github.com/user-attachments/assets/24962c28-e026-4def-b294-8770251f102a)

``` python
listings.columns
```
![image](https://github.com/user-attachments/assets/a5793ed6-b614-416b-9d1c-42e649ef614b)

# ✅ The room type and price are provided separately.

##### Let`s Combine and visualize them
``` python
import matplotlib.pyplot as plt
price_by_room = listings.groupby('room_type')['price'].mean()
print(price_by_room)

# Plot price by room type
price_by_room.plot(kind='bar', color='cyan')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')

plt.show()
```
![image](https://github.com/user-attachments/assets/c5f57425-0646-43f8-86c3-8083165f4d47)

# ✅ Identify the top 10 neighborhoods with the highest number of listings.
``` python
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='lightcoral')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```
![image](https://github.com/user-attachments/assets/1f9ae16d-6f26-4116-a293-99fb2b47390a)

# ✅ Geographical Distribution of Listings (Price Colored)
''' python 
import matplotlib.pyplot as plt
import seaborn as sns
```
``` python
plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
![image](https://github.com/user-attachments/assets/c8a6e207-decd-4d6a-adb9-eb144adfc4b6)

# Let us see the listings on a real map
* Hotter Areas (Red/Yellow): High Density: The areas that appear in red or yellow (the "hot" colors) indicate higher density or concentration of listings. This means there are more listings in these areas. Popular Locations: These regions might be more popular or in high demand. It could be near tourist attractions, popular neighborhoods, or central areas in New York where people tend to stay more often. Colder Areas (Green/Blue):
* Low Density: Areas with blue or green (the "cold" colors) indicate a lower concentration of listings. These regions have fewer listings available. Less Popular Locations: These areas might be less popular or further from key attractions. If you're looking at pricing or other factors, lower density could imply less competition in these regions, which might indicate more affordable areas or less tourist traffic.Density Patterns:
* Clustered Areas: If you notice clusters of heatmap intensity, they represent hotspots. These might correspond to high-traffic areas like tourist attractions, business districts, or entertainment hubs in New York. Spread-Out Listings: If the heatmap shows a more uniform distribution, it could suggest that listings are more evenly spread across the region, which may reflect a more balanced demand for rentals across different areas of New York.
```python

import folium
from folium.plugins import HeatMap
import pandas as pd


NewYork_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around New York 
m = folium.Map(location=[40.71072729805865, -74.01045684567059], zoom_start=10)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in NewYork_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('NewYork _heatmap.html')

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m
```
![image](https://github.com/user-attachments/assets/b58696e6-75f8-42ac-9746-177b3e2df0a5)

# 🚨 How do I find location for my city?
* Type your city name on google maps
* Right click
* The firt button
![image](https://github.com/user-attachments/assets/de1c29bc-763d-4b9e-b114-e42ef04889c9)


# How many listings have a price above $200?
```python
listings_above_200 = listings[listings['price'] > 200].shape[0]
print("Number of listings with a price above $200:", listings_above_200)
```
![image](https://github.com/user-attachments/assets/5cb11000-7c88-41c6-9b23-aaf51f5e2290)

# What is the most common room type in Manhattan?

``` python
most_common_room_type_manhattan = listings[listings['neighbourhood_group'] == 'Manhattan']['room_type'].mode()[0]

print("The most common room type in Manhattan is:", most_common_room_type_manhattan)
```
![image](https://github.com/user-attachments/assets/900e0787-77d1-477b-8687-9895bd1a99f8)







































