# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 09/03/2026


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# 1. Load data and convert date
df = pd.read_csv('data.csv')
df['date'] = pd.to_datetime(df['date'])

# 2. Prepare daily series
daily_data = df.groupby('date')['price'].mean().asfreq('D').interpolate()

# 3. Perform Decomposition
result = seasonal_decompose(daily_data, model='additive', period=7)

# --- OUTPUT GENERATION ---
print("FIRST FIVE ROWS:")
print(df[['date', 'price']].head())

# Plotting
plt.figure(figsize=(10,4))
plt.plot(daily_data)
plt.title("PLOTTING THE DATA")
plt.show()

plt.figure(figsize=(10,4))
plt.plot(result.seasonal)
plt.title("SEASONAL PLOT REPRESENTATION")
plt.show()

plt.figure(figsize=(10,4))
plt.plot(result.trend)
plt.title("TREND PLOT REPRESENTATION")
plt.show()

result.plot()
plt.suptitle("OVERALL REPRESENTATION", fontsize=15)
plt.show()
```




### OUTPUT:
FIRST FIVE ROWS:
```
        date      price
0 2014-05-02   313000.0
1 2014-05-02  2384000.0
2 2014-05-02   342000.0
3 2014-05-02   420000.0
4 2014-05-02   550000.0
```

PLOTTING THE DATA:
<img width="826" height="374" alt="tas 5 1" src="https://github.com/user-attachments/assets/0213b14d-2213-4f42-a50a-3377b54bdf9c" />



SEASONAL PLOT REPRESENTATION :

<img width="860" height="374" alt="tas 5 2" src="https://github.com/user-attachments/assets/cb360fa0-42dd-4e78-b0c7-8a0508a38705" />



TREND PLOT REPRESENTATION :

<img width="873" height="374" alt="tas 5 3" src="https://github.com/user-attachments/assets/d7d9cfe1-77f0-4746-90e4-b93d1bc513e8" />


OVERAL REPRESENTATION:
<img width="987" height="593" alt="tas 5 4" src="https://github.com/user-attachments/assets/b5dce1f1-0a43-4e36-adf8-4f28853b5a29" />



### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
