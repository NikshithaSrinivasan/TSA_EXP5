# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 11.05.2026


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
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Step 1: Load the dataset
data = pd.read_csv('/content/sales.csv')

# Step 2: Convert date column to datetime
data['order_date'] = pd.to_datetime(data['order_date'])

# Step 3: Set date column as index
data.set_index('order_date', inplace=True)

# Step 4: Sort data by date
data = data.sort_index()

# Step 5: Resample revenue data monthly
monthly_sales = data['revenue'].resample('ME').sum()

# Step 6: Remove missing values
monthly_sales = monthly_sales.dropna()

# Step 7: Perform seasonal decomposition
decomposition = seasonal_decompose(
    monthly_sales,
    model='additive',
    period=12
)

# Step 8: Plot the decomposition
plt.figure(figsize=(10, 12))

# Original Data
plt.subplot(411)
plt.plot(monthly_sales, label='Monthly Revenue')
plt.legend(loc='upper left')
plt.title('Monthly Revenue')

# Trend Plot
plt.subplot(412)
plt.plot(decomposition.trend, label='Trend', color='orange')
plt.legend(loc='upper left')
plt.title('Trend Plot')

# Seasonal Plot
plt.subplot(413)
plt.plot(decomposition.seasonal, label='Seasonal', color='green')
plt.legend(loc='upper left')
plt.title('Seasonality Plot')

# Residual Plot
plt.subplot(414)
plt.plot(decomposition.resid, label='Residual', color='red')
plt.legend(loc='upper left')
plt.title('Residual Plot')

plt.tight_layout()
plt.show()
```
### OUTPUT:

PLOTTING THE DATA:
<img width="739" height="220" alt="image" src="https://github.com/user-attachments/assets/176047f9-beac-4833-8483-f1bef1d78268" />


SEASONAL PLOT REPRESENTATION :
<img width="746" height="215" alt="image" src="https://github.com/user-attachments/assets/713c7532-041e-44ce-ac32-665e9bc6bca0" />

TREND PLOT REPRESENTATION :
<img width="746" height="235" alt="image" src="https://github.com/user-attachments/assets/682e6cec-86b7-4dc0-8c50-62d8155a02b3" />


RESIDUAL REPRESENTATION:
<img width="745" height="229" alt="Screenshot 2026-05-11 084547" src="https://github.com/user-attachments/assets/1b0c5dbc-68b0-4e26-8b26-e6c519a803f0" />



### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
