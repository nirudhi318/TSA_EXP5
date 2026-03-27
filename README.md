### Ex.No: 6 HOLT WINTERS METHOD

### date: 16/03/2026

### AIM:
To implement the Holt Winters Method Model using Python.

### ALGORITHM:
1. You import the necessary libraries
2. You load a CSV file containing daily sales data into a DataFrame, parse the 'date' column as
datetime, set it as index, and perform some initial data exploration
3. Resample it to a monthly frequency beginning of the month
4. You plot the time series data, and determine whether it has additive/multiplicative
trend/seasonality
5. Split test,train data,create a model using Holt-Winters method, train with train data and
Evaluate the model predictions against test data
6. Create teh final model and predict future data and plot it

### PROGRAM:
~~~

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.holtwinters import ExponentialSmoothing
from sklearn.preprocessing import MinMaxScaler
from sklearn.metrics import mean_squared_error
data = pd.read_csv('AirPassengers.csv', parse_dates=['Month'], index_col='Month')

print(data.head())


data_monthly = data.resample('MS').sum()


data_monthly.plot(title="Time Series Data")
plt.show()


scaler = MinMaxScaler()
scaled_data = pd.Series(
    scaler.fit_transform(data_monthly.values.reshape(-1, 1)).flatten(),
    index=data_monthly.index
)

scaled_data = scaled_data + 1


train_size = int(len(scaled_data) * 0.8)
train = scaled_data[:train_size]
test = scaled_data[train_size:]


model = ExponentialSmoothing(
    train,
    trend='add',
    seasonal='mul',
    seasonal_periods=12
).fit()

pred = model.forecast(len(test))


ax = train.plot()
pred.plot(ax=ax)
test.plot(ax=ax)
ax.legend(["Train", "Prediction", "Test"])
plt.show()


rmse = np.sqrt(mean_squared_error(test, pred))
print("RMSE:", rmse)


final_model = ExponentialSmoothing(
    scaled_data,
    trend='add',
    seasonal='mul',
    seasonal_periods=12
).fit()

future = final_model.forecast(12)

ax = scaled_data.plot()
future.plot(ax=ax)
ax.legend(["Data", "Future"])
plt.show()

````

### OUTPUT:

<img width="945" height="615" alt="Screenshot 2026-03-27 211503" src="https://github.com/user-attachments/assets/1e5f2fdb-1fd7-4d28-a677-056f1690742b" />

<img width="857" height="609" alt="Screenshot 2026-03-27 211512" src="https://github.com/user-attachments/assets/d7819f9d-b4b6-4ee6-8441-266678e59170" />

<img width="864" height="632" alt="Screenshot 2026-03-27 211519" src="https://github.com/user-attachments/assets/4d084276-520a-4fa9-963a-2da59cfae03a" />




### RESULT:
Thus the program run successfully based on the Holt Winters Method model.
