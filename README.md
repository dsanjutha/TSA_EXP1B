# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 25.10.2026

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load dataset
data = pd.read_csv("cars_dataset.csv")

# Remove spaces from column names
data.columns = data.columns.str.strip()

# Convert year and price to numeric
data['year'] = pd.to_numeric(data['year'], errors='coerce')
data['price'] = pd.to_numeric(data['price'], errors='coerce')

# Remove missing values
data = data.dropna(subset=['year', 'price'])

# Calculate average price for each year
yearly_data = data.groupby('year')['price'].mean().reset_index()
yearly_data = yearly_data.sort_values('year')

# Regular differencing
yearly_data['price_diff'] = yearly_data['price'].diff()

# Log transformation
yearly_data['price_log'] = np.log(yearly_data['price'])

# Log transformation and regular differencing
yearly_data['price_log_diff'] = yearly_data['price_log'].diff()

# Plot transformations
plt.figure(figsize=(14, 14))

plt.subplot(4, 1, 1)
plt.plot(yearly_data['year'], yearly_data['price'], marker='o')
plt.title('Original Data: Year vs Average Price')
plt.xlabel('Year')
plt.ylabel('Average Price')
plt.grid(True)

plt.subplot(4, 1, 2)
plt.plot(yearly_data['year'], yearly_data['price_diff'], marker='o')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Price Difference')
plt.grid(True)

plt.subplot(4, 1, 3)
plt.plot(yearly_data['year'], yearly_data['price_log'], marker='o')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log Price')
plt.grid(True)

plt.subplot(4, 1, 4)
plt.plot(yearly_data['year'], yearly_data['price_log_diff'], marker='o')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Log Price')
plt.grid(True)

plt.tight_layout()
plt.show()

# Overall view: Year vs Average Price
plt.figure(figsize=(12, 6))
plt.plot(yearly_data['year'], yearly_data['price'],
         marker='o', label='Average Car Price')

plt.xlabel('Year')
plt.ylabel('Average Price')
plt.title('Car Price Analysis: Year vs Average Price')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```


### OUTPUT:



<img width="1128" height="691" alt="ex1(b) output graph first" src="https://github.com/user-attachments/assets/43948fab-6d84-406c-b7c8-adf3536e25ea" />


<img width="1088" height="700" alt="ex1(b) output graph second" src="https://github.com/user-attachments/assets/c20a3506-3825-40ca-9e66-0caf85c47aaa" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
