# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_excel("Large_Yearly_Sales_Data_1900_2024.xlsx")

data.head()

data['Year'] = pd.to_datetime(data['Year'], format='%Y')
data.set_index('Year', inplace=True)

data['passengers_diff'] = data['Sales_Rate'] - data['Sales_Rate'].shift(1)

result = seasonal_decompose(data['Sales_Rate'], model='additive', period=12)
data['passengers_sea_diff'] = result.resid

data['passengers_log'] = np.log(data['Sales_Rate'])

data['passengers_log_diff'] = data['passengers_log'] - data['passengers_log'].shift(1)

result = seasonal_decompose(data['passengers_log_diff'].dropna(), model='additive', period=12)
data['passengers_log_seasonal_diff'] = result.resid


plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['Sales_Rate'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('Sales')

plt.subplot(6, 1, 2)
plt.plot(data['passengers_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Sales')

plt.subplot(6, 1, 3)
plt.plot(data['passengers_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally Adjusted Sales')

plt.subplot(6, 1, 4)
plt.plot(data['passengers_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(Sales)')

plt.subplot(6, 1, 5)
plt.plot(data['passengers_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff(Log(Sales))')

plt.subplot(6, 1, 6)
plt.plot(data['passengers_log_seasonal_diff'], label='Log Transformation and Seasonal Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(Sales)))')

plt.tight_layout()
plt.show()

data.plot(kind='line')
plt.show()
```


### OUTPUT:


REGULAR DIFFERENCING:
<img width="1650" height="262" alt="image" src="https://github.com/user-attachments/assets/46ee575b-2e6a-4e7b-8cd3-675b76e36724" />



SEASONAL ADJUSTMENT:
<img width="1638" height="269" alt="image" src="https://github.com/user-attachments/assets/531c00b8-e75c-44ec-a415-06526e76d694" />


LOG TRANSFORMATION:
<img width="1639" height="263" alt="image" src="https://github.com/user-attachments/assets/5fe63ad1-8984-4ee1-b273-75f6b3840335" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
