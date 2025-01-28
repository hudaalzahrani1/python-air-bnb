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


























