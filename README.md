
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Load and Prepare Data
df = pd.read_csv('sales_data.csv')
df['Sale_Date'] = pd.to_datetime(df['Sale_Date'])
df['Month'] = df['Sale_Date'].dt.to_period('M').astype(str)

# 2. Key Metrics
total_sales = df['Sales_Amount'].sum()
top_rep = df.groupby('Sales_Rep')['Sales_Amount'].sum().idxmax()
print(f"Total Revenue: ${total_sales:,.2f}")
print(f"Top Performer: {top_rep}")

# 3. Monthly Sales Trend
monthly_sales = df.groupby('Month')['Sales_Amount'].sum()
plt.figure(figsize=(10, 5))
monthly_sales.plot(kind='line', marker='o', color='b')
plt.title('Monthly Sales Trend')
plt.ylabel('Revenue')
plt.grid(True)
plt.show()

# 4. Sales by Category
plt.figure(figsize=(8, 5))
sns.barplot(data=df, x='Product_Category', y='Sales_Amount', estimator=sum, ci=None)
plt.title('Revenue by Category')
plt.show()

# 5. Relationship Analysis (Heatmap)
plt.figure(figsize=(8, 6))
sns.heatmap(df.corr(), annot=True, cmap='RdBu')
plt.title('Metric Correlations')
plt.show()
