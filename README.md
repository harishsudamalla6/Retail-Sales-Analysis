# Retail-Sales-Analysis
#Analysng the Retail Product Sales
#Exexute the Code in Jupyter Notebook

pip show pandas
………………………………………………………………………………………………................
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
sns.set(style='whitegrid’)
%matplotlib inline
……………………………………………………………………………………………………........
df = pd.read_csv(r'C:\Users\DELL 5480\Downloads\retail_sales_dataset.csv’)
df.head()
…………………………………………………………………………………………………………
df.info()
df.isnull().sum()
…………………………........................................................................................................................
df['Date'] = pd.to_datetime(df['Date'], errors='coerce’)
df['Month'] = df['Date'].dt.to_period('M’)
df['Year'] = df['Date'].dt.year
df.head()
……………………………....................................................................................................................
print("Total Revenue: ₹", df['Total Amount'].sum())
print("Total Orders:", len(df))
print("Unique Customers:", df['Customer ID'].nunique())
print("Product Categories:", df['Product Category'].nunique())
……………………………....................................................................................................................
monthly_sales = df.groupby('Month')['Total Amount'].sum().reset_index()
monthly_sales['Month'] = monthly_sales['Month'].astype(str)
plt.figure(figsize=(10, 5))
sns.lineplot(data=monthly_sales, x='Month', y='Total Amount', marker='o’)
plt.title('Monthly Revenue Trend’)
plt.xlabel("Month")
plt.ylabel("Total Revenue (₹)")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
………………………………................................................................................................................
category_sales = df.groupby('Product Category')['Total Amount'].sum().sort_values()
plt.figure(figsize=(8, 5))
category_sales.plot(kind='barh', color='lightgreen’)
plt.title("Revenue by Product Category")
plt.xlabel("Revenue (₹)")
plt.tight_layout()
plt.show()
……………………………………………………………………………………………………………………………………………………………….
top_customers = df.groupby('Customer ID')['TotalAmount'].sum().sort_values(ascending=False).head(10)
plt.figure(figsize=(8, 4))
top_customers.plot(kind='bar', color='tomato’)
plt.title("Top 10 Customers by Revenue")
plt.xlabel("Customer ID")
plt.ylabel("Revenue (₹)")
plt.tight_layout()
plt.show()

