# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)

### Name: GOKUL S
### Reg.No: 212224240044
### Date: 3.11.2026


### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.

### SOFTWARE REQUIRED:
1. Google Colab /
2. Jupiter Notebook

### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```py
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# Load dataset
df = pd.read_csv('Indian_Climate_Dataset_2024_2025.csv')
df['Date'] = pd.to_datetime(df['Date'])

# Pick one city and one column (change these if you want)
city = df['City'].unique()[0]
column = 'Temperature_Avg (°C)'

city_df = df[df['City'] == city].sort_values('Date')
data = np.array(city_df[column].dropna())   # must be a numpy array for slicing math

N = len(data)
lags = range(35)
autocorr_values = []
mean_data = np.mean(data)
variance_data = np.var(data)
normalized_data = (data - mean_data) / np.sqrt(variance_data)

# Go through lag components one-by-one
for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum((data[:-lag] - mean_data) * (data[lag:] - mean_data)) / N
        autocorr_values.append(auto_cov / variance_data)  # Normalize by variance

# Display the graph
plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)
plt.title(f'Autocorrelation of {column} - {city}')
plt.xlabel('Lag (days)')
plt.ylabel('Autocorrelation')
plt.grid(True)
plt.show()
```

### OUTPUT:

<img width="846" height="547" alt="download" src="https://github.com/user-attachments/assets/fc7437e3-8bd8-4e8d-b593-b0e8ab55de52" />

### RESULT:

Thus we have successfully implemented the auto correlation function in python.
