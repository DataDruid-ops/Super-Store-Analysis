# Super Store Sales Analysis

## Project Overview
The **Super Store Sales Analysis** project aims to derive actionable business insights from retail sales data. This analysis covers sales trends, profitability, and regional performance to support strategic decision-making.

## Objectives
- Clean the dataset.
- Customer segmentation.
- Analyze total sales.
- Identify key sales trends and patterns.
- Examine region-wise sales performance.
- Provide data-driven recommendations for business growth.

## Dataset
- **Source:** Super Store Sales Dataset
- **Features:**
  - Order ID, Order Date, Ship Date
  - Customer ID, Customer Name, Segment, Country, Region
  - Product ID, Product Category, Sub-Category, Product Name
  - Sales, Profit, Discount, Quantity
  - 
## Methodology
1. **Data Cleaning & Preparation**
   - Handling missing values and duplicates.
   - Formatting date fields and standardizing categories.
2. **Exploratory Data Analysis (EDA)**
   - Univariate and bivariate analysis.
   - Trend identification for sales and profits.
3. **Advanced Analysis**
   - Predictive modeling for sales forecasting.
   - Customer segmentation for targeted marketing.
4. **Dashboard & Reporting**
   - Power BI dashboard with automated updates.
   - Dynamic KPIs for sales, profit margins, and regional performance.

## Key Insights
- Identification of best-performing products and regions.
- Impact of discounting strategies on profitability.
- Seasonal trends affecting sales volumes.
- Recommendations to optimize inventory and pricing.
- 
## Tools & Technologies
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df =pd. read_csv("train.csv")

df.head()

df.info()

null_count = df['Postal Code'].isnull().sum()
print(null_count)

df['Postal Code'].fillna(0, inplace=True)

df['Postal Code'] = df['Postal Code'].astype(int)

df.duplicated(keep=False).sum()

# types of customers

types_of_customers = df['Segment'].unique()
print(types_of_customers)

# number of customers in each segment

number_of_customers = df['Segment'].value_counts().reset_index()

number_of_customers = number_of_customers.rename(columns={'Segment' : 'Customer Type', 'count':'Total Customers'})

print(number_of_customers)

# plotting a pie chart

plt.pie(number_of_customers['Total Customers'], labels=number_of_customers['Customer Type'], autopct='%1.1f%%')

# set pie chart labels
plt.title('Distribution of Customers')

plt.show()
sales_per_category = df.groupby('Segment')['Sales'].sum().reset_index()

sales_per_category = sales_per_category.rename(columns={'Segment' : 'Customer Type', 'Sales':'Total Sales'})

print(sales_per_category)

# plotting a pie chart

plt.pie(sales_per_category['Total Sales'], labels=sales_per_category['Customer Type'], autopct='%1.1f%%')

# set pie chart labels
plt.title('Sales per Customer Category')

plt.show()

# bar graph
plt.bar(sales_per_category['Customer Type'], sales_per_category['Total Sales'])

# label
plt.title("Sales per Customer Category")
plt.xlabel("Customer Type")
plt.ylabel("Total Sales")

# the consumer segment is the most sold
# group data according to: Customer ID, Customer Name, Segemnt and Calculate frequency of their order

customer_order_freq = df.groupby(['Customer ID', 'Customer Name', 'Segment'])['Order ID'].count().reset_index()

# rename the order id column
customer_order_freq.rename(columns={'Order ID' : 'Total Orders'}, inplace=True)

# identify repeat customers
repeat_customers = customer_order_freq[customer_order_freq['Total Orders' ]>= 1]

# sort repeat  customer in descending order
sorted_repeat_customer = repeat_customers.sort_values(by = 'Total Orders', ascending=False)

print(sorted_repeat_customer.head(10).reset_index(drop=True))
```



## How to Use
1. **SQL Integration:** Ensure SQL Server is set up for data automation.
2. **Power BI Setup:** Load dataset and refresh connections.
3. **Analysis Execution:** Use provided scripts for deeper insights.

## Future Enhancements
- Implement real-time data updates.
- Develop predictive models for demand forecasting.
- Expand analysis to customer lifetime value (CLV).

## License
This project is open-source under the MIT License.

