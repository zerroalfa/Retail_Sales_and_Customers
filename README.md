# Retail_Sales_and_Customers
this is my 8th project with Quantum Analytics

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Recommendations](#recommendations)

### Project Overview
---

**Project Overview: Retail Sales and Customer Demographics Analysis**  

This project aims to explore and analyze retail sales and customer demographics using a synthetic dataset that captures key attributes of a dynamic retail environment. The dataset serves as an excellent resource for understanding sales trends, customer behavior, and the influence of demographic factors on purchasing patterns. The ultimate goal is to derive actionable insights that can optimize retail strategies and enhance customer engagement.  

### Objectives:  
1. **Sales Trend Analysis**: Identify patterns in sales over time, including seasonal trends and peak periods.  
2. **Customer Demographic Insights**: Analyze customer purchasing behavior based on demographic factors such as age and gender.  
3. **Product Preferences**: Understand the popularity of different product categories and their contribution to overall sales.  
4. **Purchase Volume and Spending**: Explore transaction volumes and spending habits to identify high-value customers and products.  
5. **Customer Segmentation**: Segment customers based on demographics and purchasing behavior to support targeted marketing efforts.  
6. **Revenue Optimization**: Derive insights to improve pricing strategies and optimize product offerings.  

### Key Areas of Analysis:  
1. **Temporal Sales Analysis**:  
   - Track sales trends by day, month, and year to identify peak periods.  
   - Analyze the impact of time (e.g., holidays or weekends) on purchasing behavior.  

2. **Demographic-Based Analysis**:  
   - Investigate gender-based differences in purchasing patterns.  
   - Explore age group preferences for various product categories and spending habits.  

3. **Product Category Analysis**:  
   - Determine the most popular product categories.  
   - Evaluate average spending and quantities purchased per category.  

4. **Transaction-Level Insights**:  
   - Analyze high-value transactions to understand customer preferences and motivations.  
   - Examine purchase frequency and volume across different customer segments.  

5. **Customer Lifetime Value (CLV)**:  
   - Estimate customer value based on spending patterns and transaction frequency.  
   - Identify loyal customers and explore strategies to enhance retention.  

### Potential Use Cases:  
1. **Marketing Strategies**: Develop targeted campaigns based on customer demographics and product preferences.  
2. **Inventory Management**: Align stock levels with demand patterns identified through sales trends.  
3. **Pricing Optimization**: Adjust pricing strategies based on insights into customer spending behavior and product popularity.  
4. **Customer Relationship Management**: Enhance customer satisfaction by tailoring offerings to segmented groups.  
5. **Revenue Growth**: Identify high-performing products and customer groups to focus efforts on growth areas.  

This project will provide a comprehensive understanding of retail sales and customer demographics, enabling businesses to enhance their operational efficiency, tailor their marketing efforts, and improve overall customer satisfaction.

![Dashboard]![8 Retail Sales and Customers](https://github.com/user-attachments/assets/13a942e4-cdbc-4fbc-b285-fcff7af956eb)



### Data Sources

Retail Sales dataset: The primary dataset used for this analysis is the "retail-sales-dataset-csv.csv" file, containing detailed information about Retail Sales.

### Tools

- Excel - Data Cleaning
  - [Download here](https://microsoft.com)
- SQL Server - Data Analysis
- PowerBI - Creating reports


### Data Cleaning/Preparation

In the initial data preparation phase, we performed the following tasks:
1. Data loading and inspection.
2. Handling missing values.
3. Data cleaning and formatting.

### Exploratory Data Analysis

EDA involved exploring the sales data to answer key questions, such as:

- What is the overall sales trend?
- Which products are top sellers?
- What are the peak sales periods?

### Data Analysis

Include some interesting code/features worked with

**Customer Age and Gender Influence on Purchasing Behavior**
```sql
SELECT 
    Gender, 
    CASE 
        WHEN Age < 25 THEN 'Under 25'
        WHEN Age BETWEEN 25 AND 34 THEN '25-34'
        WHEN Age BETWEEN 35 AND 44 THEN '35-44'
        WHEN Age BETWEEN 45 AND 54 THEN '45-54'
        ELSE '55 and above'
    END AS Age_Group, 
    COUNT(*) AS Total_Transactions,
    SUM(Total_Amount) AS Total_Spent
FROM 
    retail_sales_data
GROUP BY 
    Gender, Age_Group
ORDER BY 
    Gender, Age_Group;
```

**Relationship Between Age, Spending, and Product Preference**
```sql
SELECT 
    CASE 
        WHEN Age < 25 THEN 'Under 25'
        WHEN Age BETWEEN 25 AND 34 THEN '25-34'
        WHEN Age BETWEEN 35 AND 44 THEN '35-44'
        WHEN Age BETWEEN 45 AND 54 THEN '45-54'
        ELSE '55 and above'
    END AS Age_Group, 
    Product_Category, 
    COUNT(*) AS Total_Transactions,
    SUM(Total_Amount) AS Total_Spent
FROM 
    retail_sales_data
GROUP BY 
    Age_Group, Product_Category
ORDER BY 
    Age_Group, Total_Spent DESC;
```

**Patterns in Sales Across Different Time Periods**
```sql
SELECT 
    DATE_FORMAT(Date, '%Y-%m') AS Sale_Month, 
    COUNT(*) AS Total_Transactions,
    SUM(Total_Amount) AS Total_Spent
FROM 
    retail_sales_data
GROUP BY 
    Sale_Month
ORDER BY 
    Sale_Month;
```

**Product Category with the Highest Appeal**
```sql
SELECT 
    Product_Category, 
    COUNT(*) AS Total_Transactions,
    SUM(Total_Amount) AS Total_Spent
FROM 
    retail_sales_data
GROUP BY 
    Product_Category
ORDER BY 
    Total_Spent DESC
LIMIT 1;
```

**Adaptation of Shopping Habits During Seasonal Trends**
```sql
SELECT 
    MONTH(Date) AS Sale_Month, 
    COUNT(*) AS Total_Transactions,
    SUM(Total_Amount) AS Total_Spent
FROM 
    retail_sales_data
GROUP BY 
    Sale_Month
ORDER BY 
    Sale_Month;
```

**Distinct Purchasing Behaviors Based on the Number of Items Bought**
```sql
SELECT 
    Quantity, 
    COUNT(*) AS Total_Transactions,
    SUM(Total_Amount) AS Total_Spent
FROM 
    retail_sales_data
GROUP BY 
    Quantity
ORDER BY 
    Quantity;
```

**Total Sales Amount, Average Customer Age, Male Sales, Female Sales, Total Transactions, and Total Quantity Sold**
```sql
SELECT 
    SUM(Total_Amount) AS Total_Sales_Amount,
    AVG(Age) AS Average_Customer_Age,
    SUM(CASE WHEN Gender = 'Male' THEN Total_Amount ELSE 0 END) AS Male_Sales,
    SUM(CASE WHEN Gender = 'Female' THEN Total_Amount ELSE 0 END) AS Female_Sales,
    COUNT(*) AS Total_Transactions,
    SUM(Quantity) AS Total_Quantity_Sold
FROM 
    retail_sales_data;
```

### Results/Findings

The analysis results are summarized as follows:

**Customer Age and Gender Influence on Purchasing Behavior:**

Younger customers (under 25) tend to make fewer transactions but spend significantly when they do, particularly on electronics and beauty products.
Males generally spend more than females, especially in the electronics category, while females show higher engagement in clothing and beauty.

**Relationship Between Age, Spending, and Product Preference:**

The 25-34 age group exhibits a strong preference for clothing, contributing to higher spending in this category.
Older customers (45 and above) tend to prefer electronics and beauty products, with notable spending patterns during specific months.

**Patterns in Sales Across Different Time Periods:**

Sales peak during holiday seasons (e.g., November and December), indicating a strong seasonal trend.
Monthly sales data shows fluctuations, with significant increases in spending during back-to-school and holiday periods.

**Product Category with the Highest Appeal:**

Clothing emerged as the most popular category, followed closely by electronics and beauty products, indicating diverse consumer interests.

**Adaptation of Shopping Habits During Seasonal Trends:**

Customers adapt their purchasing habits based on seasonal trends, with a noticeable shift towards gift-related purchases during the holiday months.

**Distinct Purchasing Behaviors Based on the Number of Items Bought:**

Customers purchasing in larger quantities (3 or more items) tend to spend significantly more, particularly in clothing and electronics.

**Total Sales Amounts and Customer Demographics:**

The total sales amount is substantial, with a balanced average customer age indicating a diverse customer base.
Male sales outpace female sales in total amount spent, but female customers have higher transaction counts.

### Recommendations

Based on the analysis, we recommend the following actions:

**Targeted Marketing Campaigns:**

Develop marketing strategies tailored to younger demographics, emphasizing high-value products in electronics and beauty.
Create campaigns focused on clothing during peak shopping seasons to capitalize on the high engagement in this category.

**Seasonal Promotions:**

Implement seasonal promotions and discounts during peak shopping months to attract more customers and increase sales volume.

**Product Bundling:**

Consider bundling popular products (e.g., clothing with accessories) to encourage larger purchases, especially aimed at customers who typically buy multiple items.

**Customer Engagement Strategies:**

Enhance customer engagement through loyalty programs that reward repeat purchases, particularly for categories with high transaction counts like clothing.

**Data-Driven Insights:**

Continuously monitor sales data to refine marketing strategies and product offerings based on emerging trends and customer preferences.


### Limitations

**Sample Size and Scope:**

The dataset may not fully represent the entire customer base, leading to potential biases in understanding purchasing behavior.

**Temporal Factors:**

External factors such as economic conditions, competitor actions, and market trends could influence purchasing behavior but may not be reflected in the dataset.

**Data Accuracy:**

The accuracy of self-reported data (if applicable) could impact the reliability of findings, particularly in demographic reporting.

**Limited Product Categories:**

The analysis is limited to the categories present in the dataset, which may not encompass the full range of customer interests and behaviors.

**Static Analysis:**

The findings are based on historical data and may not account for future changes in consumer behavior or market dynamics.

This structured overview provides a comprehensive understanding of the insights derived from the retail sales analysis, along with actionable recommendations and a candid acknowledgment of the study's limitations.
### References

`column_1`

**bold**

*italic*
