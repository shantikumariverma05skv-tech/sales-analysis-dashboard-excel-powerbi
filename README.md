
# Superstore Sales Analysis Dashboard (Excel & Power BI)



## Business Objective
To analyze sales performance across regions, categories, and products to support data-driven business decisions.

## Dataset


**Superstore Sales Dataset** containing:

- Order ID
- Product Name
- Category
- Region
- Sales, Quantity, Profit
- Order Date

- Source: Public Superstore dataset (Kaggle)
- 
## Tools & Skills Used
- **Tools:** Excel (Pivot Tables, Aggregations, Trend Analysis), Power BI (Dashboard Design, Data Modeling, Visual Analytics)
- **Skills:** Business Analysis, Data Visualization, Sales Performance Analysis

## Business Questions Addressed

- Which regions generate the highest sales and which need improvement?
- What are the monthly sales trends and seasonal patterns?
- Which products contribute most to total revenue?
- Which product categories generate the highest profit?

## Key KPIs
- Total Sales
- Total Orders
- Sales by Region
- Sales by Category

## Analysis & Insights


<img width="884" height="502" alt="sales_dashboard_preview" src="https://github.com/user-attachments/assets/433ac7bc-d1e2-4e8a-b94f-b51555c474fc" />


### 1. Sales by Region
#### Excel Pivot Table:



```text
Rows: Region
Values: Sum of Sales
Sort by: Sum of Sales (Descending)
```

#### Power BI DAX:

```DAX
TotalSales = SUM('Superstore'[Sales])
```

#### Insight:

- West region is the top revenue contributor.
- South region underperforms → opportunity for targeted marketing campaigns.

---

### 2. Top Products Analysis

<img width="1198" height="466" alt="e2" src="https://github.com/user-attachments/assets/26052427-9ce6-4ea8-8b56-04511e40f97c" />


#### Excel Pivot Table:
```text

Rows: Product Name
Values: Sum of Sales
Sort by: Sum of Sales (Descending)
Filter: Top 5 Products

```

#### Power BI DAX:

```DAX
TopProducts = 
TOPN(5, SUMMARIZE('Superstore', 'Superstore'[Product Name], "TotalSales", SUM('Superstore'[Sales])), [TotalSales], DESC)
```

#### Insight:

- Small group of products drives majority of revenue → focus on inventory optimization and promotions.

---

### 3 Monthly Sales Trend

<img width="395" height="686" alt="e3" src="https://github.com/user-attachments/assets/eff86a61-910e-4e5b-bb57-4860e7aa771e" />
<img width="407" height="686" alt="e4" src="https://github.com/user-attachments/assets/b3634a0c-9cbf-417e-b319-48cb2bc735b0" />



#### Excel Pivot Table:
```text
Rows: Month(Order Date)
Values: Sum of Sales
Chart: Line chart
```

#### Power BI DAX:

```DAX
MonthlySales = 
SUMMARIZE('Superstore', 
          FORMAT('Superstore'[Order Date], "YYYY-MM"), 
          "TotalSales", SUM('Superstore'[Sales]))

```

#### Insight:

- Sales peak in Q1–Q2 → seasonal promotions can maximize revenue.

---

### 4 Category-wise Profit Analysis
#### Excel Pivot Table:
```text
Rows: Category
Values: Sum of Profit
Sort by: Sum of Profit (Descending)
```

#### Power BI DAX:
```DAX

CategoryProfit = SUMMARIZE('Superstore', 'Superstore'[Category], "TotalProfit", SUM('Superstore'[Profit]))

```

#### Insight:

- Technology category generates the highest profit.
- Office Supplies and Furniture contribute less → consider focusing promotions on high-profit categories.

  
## Key Business Insights Summary

- West region is the top revenue contributor.
- Strong seasonal sales trends in Q1–Q2.
- Top products contribute most of total sales.
- Technology category drives highest profitability.

## Conclusion

The Superstore Sales Analysis highlights actionable opportunities for business growth:

- Focus on underperforming regions (South) for marketing campaigns.
- Promote top-performing products and categories.
- Leverage seasonal trends for stock and promotion planning.

  ### Next Steps / Recommendations
- Increase marketing in South region
- Promote top 5 products and Technology category
- Plan Q1–Q2 seasonal campaign

### Business Impact:
Enables stakeholders to optimize sales strategy, improve revenue performance, and make data-driven decisions.

## Python Code for Reproducibility
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
df = pd.read_excel("Superstore_Sales.xlsx")

# 1. Sales by Region
region_sales = df.groupby('Region')['Sales'].sum().sort_values(ascending=False)
region_sales.plot(kind='bar', title='Sales by Region')
plt.show()

# 2. Top 5 Products
top_products = df.groupby('Product Name')['Sales'].sum().sort_values(ascending=False).head(5)
top_products.plot(kind='bar', title='Top 5 Products')
plt.show()

# 3. Monthly Sales Trend
df['Order Month'] = pd.to_datetime(df['Order Date']).dt.to_period('M')
monthly_sales = df.groupby('Order Month')['Sales'].sum()
monthly_sales.plot(kind='line', title='Monthly Sales Trend')
plt.show()

# 4. Category-wise Profit
category_profit = df.groupby('Category')['Profit'].sum()
category_profit.plot(kind='bar', title='Profit by Category')
plt.show()
```

## Author & Contact

**Author:** Shanti Kumari Verma  
**GitHub:** [https://github.com/shantikumariverma05skv-tech](https://github.com/shantikumariverma05skv-tech)  
**LinkedIn:** [https://www.linkedin.com/in/shantikumariverma05skv-tech](https://www.linkedin.com/in/shantikumariverma05skv-tech)  
**Role Simulated:** Data Analyst / Business Analyst
