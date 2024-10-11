# Amazon-sales-analysis
# A code for this dashboard
# Import necessary libraries
import pandas as pd
import matplotlib.pyplot as plt

# Load the sales data from CSV (replace 'sales_data.csv' with your actual filename)
data = pd.read_csv('sales_data.csv')

# Display the first few rows of the data
print(data.head())

# Basic Data Summary
print("Summary Statistics:")
print(data.describe())

# Checking for missing values
print("Missing Values:")
print(data.isnull().sum())

# Sales Analysis
# Assuming the dataset has columns like 'Date', 'Sales', 'Product', 'Region'
# Convert 'Date' column to datetime format
data['Date'] = pd.to_datetime(data['Date'])

# Create a new column for the year and month
data['Year'] = data['Date'].dt.year
data['Month'] = data['Date'].dt.month

# Total Sales Per Month
monthly_sales = data.groupby(['Year', 'Month'])['Sales'].sum().reset_index()

# Plot Monthly Sales
plt.figure(figsize=(10, 6))
plt.plot(monthly_sales['Month'], monthly_sales['Sales'], marker='o')
plt.title('Monthly Sales Over Time')
plt.xlabel('Month')
plt.ylabel('Total Sales')
plt.grid(True)
plt.show()

# Sales by Region
region_sales = data.groupby('Region')['Sales'].sum()

# Plot Sales by Region
region_sales.plot(kind='bar', figsize=(8, 5), color='skyblue')
plt.title('Sales by Region')
plt.xlabel('Region')
plt.ylabel('Total Sales')
plt.xticks(rotation=45)
plt.show()

# Sales by Product
product_sales = data.groupby('Product')['Sales'].sum()

# Plot Sales by Product
product_sales.plot(kind='bar', figsize=(8, 5), color='green')
plt.title('Sales by Product')
plt.xlabel('Product')
plt.ylabel('Total Sales')
plt.xticks(rotation=45)
plt.show()
