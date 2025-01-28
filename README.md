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














