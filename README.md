# Stock-Market-Prediction
HCLTECH Stock Prediction 

#import libaries 
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from statsmodels.stats.outliers_influence import variance_inflation_factor

#import Dataset
df_hcl= pd.read_csv(r'E:\Handson Data Science\Share Martket Analysis\IT\HCLTECH.NS.csv', header=0, index_col='Date', 
                    parse_dates= True)
df_hcl.head()

df_hcl.tail(3)

#check description
df_hcl.describe()

#check shape
df_hcl.shape


import matplotlib.dates as mdates
import datetime

#visualization
fig,ax=plt.subplots(figsize=(10,5))
plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y'))
plt.gca().xaxis.set_major_locator(mdates.YearLocator())
plt.grid(True)

plt.plot(df_hcl.index, df_hcl['Adj Close'])
plt.title('HCLTECH Stock Market Data (2002-2021)')
plt.xlabel('Year')
plt.ylabel('Adjacent Close')
plt.xticks(rotation=90)
plt.show()

#will visualize monthly movement

hcl_18= df_hcl.loc[pd.Timestamp('2018-01-01'):pd.Timestamp('2018-12-31')]
plt.plot(hcl_18.index, hcl_18['Adj Close'])
plt.grid(True)
plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m'))
plt.gca().xaxis.set_major_locator(mdates.MonthLocator())
plt.title('HCLTECH (01-01-18 to 31-12-18)')
plt.xlabel('2018')
plt.ylabel('Adjacent Close')
plt.xticks(rotation=90)
plt.show()

#visualization in the duration of  in the year of 2020 to 2021
hcl_21= df_hcl.loc[pd.Timestamp('2020-01-01'):pd.Timestamp('2021-07-24')]
plt.plot(hcl_21.index, hcl_21['Adj Close'])
plt.grid(True)
plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m'))
plt.gca().xaxis.set_major_locator(mdates.MonthLocator())
plt.title('HCLTECH (01-01-20 to 24-07-21)')
plt.xlabel('2020-21')
plt.ylabel('Adjacent Close')
plt.xticks(rotation=90)
plt.show()

#Average value checking 
monthly_hcl= hcl_21.resample('4M').mean()
plt.scatter(monthly_hcl.index, monthly_hcl['Adj Close'])
plt.grid(True)
plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%Y-%m'))
plt.gca().xaxis.set_major_locator(mdates.MonthLocator())
plt.title('HCLTECH (01-01-21 to 24-07-21)')
plt.xlabel('2021')
plt.ylabel('Adjacent Close')
plt.xticks(rotation=90)
plt.show()
