# Vendor-Performance-Analysis-Using-Python
Analyzed vendor sales and purchasing data using Python to evaluate sales performance, profitability, purchase trends, and vendor efficiency. Performed data cleaning, exploratory data analysis, statistical analysis, and visualization to identify top-performing vendors and business improvement opportunities.

📌 **1. Project Overview**

Vendor Performance Analysis is a data analytics project focused on evaluating vendor contributions to business revenue, profitability, purchasing, and inventory efficiency.

In retail and supply chain operations, selecting vendors based only on sales or purchase volume can lead to misleading decisions. A vendor may generate high sales but deliver lower profit, while another vendor may generate a high profit margin with comparatively lower sales. Similarly, excessive purchasing, slow-moving products, freight expenses, and excise taxes can affect overall business performance.

This project uses Python to examine vendor-level and product-level data, identify profitable and loss-making records, investigate relationships between financial and operational metrics, and develop actionable business recommendations.

The analysis also includes statistical testing and exploratory visualizations to understand how purchase value, sales revenue, gross profit, freight costs, excise tax, and stock turnover relate to vendor performance.

Project Domain: Retail and Supply Chain Analytics

⚠️ **2. Business Problem Statement**
   
The business needs a reliable way to evaluate vendor performance and understand which vendors and products contribute positively to profitability. Reviewing purchase and sales values alone does not provide a complete picture of financial performance or inventory efficiency.


1. Identify the vendors contributing the highest purchase value, sales revenue, and gross profit.
2. Identify underperforming vendors and products that generate losses.
3. Analyze the relationship between purchase prices, actual selling prices, sales revenue, and profitability.
4. Evaluate the relationship between freight costs, excise taxes, and gross profit.
5. Assess the impact of vendor brand count on profitability.
6. Compare purchase quantities with sales quantities to evaluate purchasing efficiency.
7. Examine the relationship between stock turnover and profit margin.
8. Compare profitability across order-size groups, freight-cost categories, and excise-tax categories.
9. Investigate vendors with substantial losses to identify potential performance issues.
10. Recommend strategies to improve vendor selection, control costs, and manage inventory effectively.


🎯 **3. Project Objectives**
   
- Analyse overall purchasing, sales, gross profit, and profit margin.
- Identify the highest- and lowest-performing vendors and products.
- Examine loss-making transactions and vendors with substantial losses.
- Evaluate relationships between prices, sales, purchases, quantities, and profit.
- Investigate freight costs, excise tax, and stock turnover.
- Examine numerical distributions, skewness, kurtosis, and potential outliers.
- Apply Winsorization to create capped versions of selected numerical variables.
- Use statistical tests to examine differences and associations within the data.
- Present the findings through Python visualizations and a Power BI dashboard.
- Recommend business actions supported by the analysis.
  
📁 **4. Dataset Information**

Dataset: Vendor Sales Summary

Source credited in the notebook: HUB of Analytics Education (HUBAE) — Bibitor, LLC dataset.

Repository: Vendor Performance Analysis Using Python

Dataset file: vendor_sales_summary.csv

The dataset contains vendor, product, pricing, purchasing, sales, tax, freight, profitability, and stock-turnover information. The time period covered by the dataset is not specified in the notebook.


The dataset contains vendor, product, pricing, purchasing, sales, tax, freight, profitability, and stock-turnover information. The time period covered by the dataset is not specified in the notebook.

### 📊 Dataset Size

| Processing Stage | Rows | Columns |
|---|---:|---:|
| Original Dataset | 10,692 | 18 |
| After Removing Two Unused Columns | 10,692 | 16 |
| After Removing Zero-Sales-Quantity Records | 10,514 | 16 |
| Final Prepared CSV Exported from the Notebook | 10,514 | 31 |

The final prepared dataset includes 10 capped numerical columns and five derived categorical columns in addition to the 16 retained original columns.

### 📋 Important Columns

| Column | Description |
|---|---|
| `VendorNumber` | Vendor identification number |
| `VendorName` | Vendor or supplier name |
| `Brand` | Brand identification number |
| `Description` | Product description |
| `PurchasePrice` | Unit purchase price |
| `ActualPrice` | Actual selling price per unit |
| `Volume` | Product volume or package size |
| `TotalPurchaseQuantity` | Total purchased quantity |
| `TotalPurchaseDollars` | Total purchase expenditure |
| `TotalSalesQuantity` | Total sales quantity |
| `TotalSalesDollars` | Total sales revenue |
| `TotalExciseTax` | Total excise tax |
| `FreightCost` | Freight or transportation cost |
| `GrossProfit` | Gross profit recorded in the dataset |
| `ProfitMargin` | Profit margin recorded in the dataset |
| `StockTurnover` | Stock turnover measure recorded in the dataset |

The original TotalSalesPrice and SalesToPurchaseRatio columns were removed during preprocessing because they were not retained for the subsequent analysis.

🛠️ **5. Technology Stack**

Programming language: Python
Libraries used:
- Pandas: Data loading, cleaning, transformation, grouping, and aggregation.
- NumPy: Numerical operations and derived categories.
- Matplotlib: Data visualization.
- Seaborn: Statistical plots and exploratory data analysis.
- SciPy: Statistical hypothesis testing and Winsorization.
- Plotly: Interactive visualizations.
- Power BI: Dashboard development and business reporting.
  
🧹 **6. Data Cleaning and Preprocessing**

Data preparation was performed before the detailed exploratory analysis.

Step 1: Initial data inspection
The notebook examined the dataset's shape, columns, data types, summary statistics, duplicate records, missing values, and unique values.

The initial review also identified differences between mean and median values and unusually high maximum values in several numerical variables, suggesting skewed distributions.

Step 2: Data type conversion
The Volume and TotalSalesQuantity columns were converted to integer data types to support the intended analysis.

Step 3: Remove unused columns
The following columns were removed:
- TotalSalesPrice
- SalesToPurchaseRatio
This reduced the analytical dataset from 18 to 16 columns.

Step 4: Remove zero-sales-quantity records
The notebook identified and removed rows where TotalSalesQuantity was equal to zero.
- Original records: 10,692
- Records removed: 178
- Records remaining: 10,514
This filtering step was used to focus the subsequent analysis on records with positive sales quantities. It is a business-rule-based filtering step, not statistical outlier removal.

Step 5: Outlier detection
Box plots, histograms, skewness, and kurtosis were examined to understand the distributions of selected numerical variables.

The analysis found that many financial and quantity variables were strongly right-skewed and contained extreme observations. However, large values were not automatically considered errors because they may represent genuine differences in vendor purchase and sales volumes.

Step 6: Winsorization
Winsorization was applied using 5% lower-tail and 5% upper-tail limits to create capped versions of the following ten columns:

PurchasePrice, ActualPrice, TotalPurchaseQuantity, TotalSalesQuantity, TotalPurchaseDollars, TotalSalesDollars, TotalExciseTax, StockTurnover, GrossProfit, and ProfitMargin.

The new columns use the _winsor suffix, preserving the original values.

This technique reduces the influence of extreme values in the capped variables. It does not delete additional rows, and it does not guarantee that every distribution becomes normally distributed.

Data quality consideration: The initial exploratory analysis flagged negative-infinity values in ProfitMargin. These values should be explicitly audited and handled if the workflow is extended, rather than assuming that every non-finite value has been corrected by outlier treatment.

⚙️ **7. Feature Engineering and Business Categories**
   
The project created five additional categorical features to support comparisons and visualization.
Derived feature	Classification used in the notebook
OrderSize	Based on Volume: VerySmall, Small, Medium, Large
ExciseTaxCategory	LowTax, MediumTax, HighTax
FreightCostCategory	VeryLowFreight, LowFreight, MediumFreight, HighFreight
StockTurnoverCategory	Low_Turnover, Balanced_Turnover, High_Turnover
ProfitCategory	Loss, VeryLowProfit, LowProfit, MediumProfit, HighProfit

The classification rules are detailed below.

OrderSize: Created from Volume using the bins [1, 1000, 5000, 10000, 25000] and labels VerySmall, Small, Medium, and Large.

ExciseTaxCategory: Created using TotalExciseTax bins of 0–500, 500–5,000, and 5,000–10,000.

FreightCostCategory: Created using FreightCost bins of 0–1,000, 1,000–10,000, 10,000–100,000, and 100,000–300,000.

StockTurnoverCategory: Based on the recorded StockTurnover value:
- Below 1: Low_Turnover
- Equal to 1: Balanced_Turnover
- Above 1: High_Turnover
ProfitCategory: Based on GrossProfit:
- At or below zero: Loss
- Above zero to 10,000: VeryLowProfit
- Above 10,000 to 20,000: LowProfit
- Above 20,000 to 50,000: MediumProfit
- Above 50,000: HighProfit
Important interpretation note: In this notebook, OrderSize is based on product Volume, not TotalPurchaseQuantity. It should therefore be interpreted as a volume-based category rather than a measure of the number of units in an order.

🧮 **8. Important Business Formulas**
   
The following formulas explain the key measures used in the analysis. Where the notebook uses a field already supplied by the dataset, this is distinguished from a newly calculated metric.

### 8.1 Total Purchase Amount
$$
\text{Total Purchases}=\sum \text{TotalPurchaseDollars}
$$

Measures the total expenditure recorded for purchasing products.
### 8.2 Total Sales Revenue

$$
\text{Total Sales} = \sum \text{TotalSalesDollars}
$$

Measures the total sales revenue recorded in the dataset.

### 8.3 Gross Profit

$$
\text{Total Gross Profit} = \sum \text{GrossProfit}
$$

The notebook aggregates the supplied `GrossProfit` field. It does not independently recompute the accounting formula used to construct that source field.

### 8.4 Overall Profit Margin

$$
\text{Profit Margin} =
\frac{\sum \text{GrossProfit}}
{\sum \text{TotalSalesDollars}} \times 100
$$

This is the overall margin calculated using aggregate gross profit divided by aggregate sales. It is not the simple average of each row's profit margin.

### 8.5 Vendor-Level Profit Margin

$$
\text{Vendor Margin} =
\frac{\text{Vendor Gross Profit}}
{\text{Vendor Sales Revenue}} \times 100
$$

This allows vendors to be compared based on the proportion of their sales revenue represented by gross profit.

### 8.6 Positive Profit, Loss, and Net Profit

Positive profit is calculated by summing positive `GrossProfit` values.

Loss is calculated by summing negative `GrossProfit` values; it remains negative when presented as a signed amount.

$$
\text{Net Profit} =
\text{Positive Profit} + \text{Negative Loss}
$$

### 8.7 Correlation

The Pearson correlation coefficient is used to examine linear relationships between numerical variables.

A positive coefficient indicates that two variables tend to increase together. A negative coefficient indicates an inverse relationship. Correlation alone does not establish causation.

8.8 Statistical significance

The analysis uses a significance threshold of \(0.05\).
- \(p<0.05\): evidence of a statistically significant difference or association under the test assumptions.
- \(p\geq0.05\): insufficient evidence to reject the null hypothesis.
The interpretation also depends on whether the groups, assumptions, and test design are appropriate for the business question.

🔍 **9. Exploratory Data Analysis** 

Exploratory analysis was conducted to understand financial performance, product behavior, vendor contributions, and inventory efficiency.
Overall financial analysis
Purchase expenditure, sales revenue, gross profit, and profit margin were aggregated to understand overall business performance.
Vendor-level analysis
Vendors were grouped by name to compare total purchases, sales, gross profit, and profit margin. The analysis identified major contributors as well as vendors requiring loss investigation.
Product-level analysis
Products were assessed using their descriptions, sales values, gross profit, and profit margins to identify high-performing and underperforming products.
Brand analysis
The analysis explored relationships between the number of brands associated with vendors and their financial performance. It examined whether vendors with greater brand counts consistently generated higher profits.
Cost and inventory analysis
Purchase prices, actual prices, freight costs, excise taxes, order-size categories, and stock-turnover categories were analysed in relation to gross profit and profit margin.
Distribution and correlation analysis
Histograms, box plots, summary statistics, skewness, kurtosis, and correlation analysis were used to understand the spread of the data, identify extreme observations, and evaluate relationships between numerical variables.

📈 **10. Statistical Analysis** 

Three hypothesis tests and a confidence interval were included in the notebook.
Method	Purpose	Recorded result
Independent-samples t-test	Compare gross-profit values for positive-profit and negative-profit records	\(t \approx 31.75\), \(p \approx 2.23\times10^{-211}\)
One-way ANOVA	Compare average gross profit across four freight-cost categories	\(F \approx 92.75\), \(p \approx 3.04\times10^{-59}\)
Chi-square test of independence	Examine association between stock-turnover category and binary profit/loss category	\(\chi^2 \approx 1603.28\), 2 degrees of freedom, \(p<0.001\)
95% confidence interval	Estimate the population mean gross profit using a normal approximation	Approximately $8,004–$8,567

Interpretation
The ANOVA result indicates that average gross profit differs across the four freight-cost categories under the test assumptions. It does not, by itself, identify which pairs of categories differ or prove that freight costs cause the difference.

The chi-square result indicates an association between stock-turnover category and profit/loss category. It does not establish causation.

The t-test compares groups created from positive versus negative gross-profit values. Since the groups are defined by the sign of the outcome being compared, the significant result is expected and should not be interpreted as evidence explaining why certain records become loss-making.

These tests provide supporting analysis; the business recommendations should also consider the underlying vendor, product, cost, and inventory data.

💡 **11. Key Findings**

The following findings are recorded in the notebook.
Overall business performance
The analysis reported approximately:
Metric	Result
Total purchase expenditure	$202.66 million
Total sales revenue	$289.32 million
Total gross profit (net of recorded losses)	$87.115 million
Positive-profit records, summed	$88.78 million
Negative-profit records, summed as a loss	-$1.66 million
Overall profit margin	30.11%

Sales revenue was higher than purchase expenditure, and the aggregated gross profit was positive. However, the presence of negative-profit records shows that performance was not uniform across all vendors and products.
Vendor performance
- Diageo North America Inc., Martignetti Companies, and Jim Beam Brands Company were among the leading vendors by purchase and sales value.
- Martignetti Companies, Diageo North America Inc., and Constellation Brands Inc. were the leading vendors by total gross profit.
- Flavor Essence Inc., Capstone International, and Silver Mountain Ciders were identified as the top vendors by profit margin in the notebook.
- A set of 12 vendors was identified for further investigation because of substantial losses. Vineyard Brands LLC, Black Cove Beverages, and Uncorked were among the vendors highlighted.
High sales contribution and high profit margin are different performance measures. Vendor rankings should therefore consider more than one metric.
Product and brand performance
- Jack Daniel’s No. 7 Black, Grand Marnier, and Bacardi Superior Rum were identified among the leading products by sales.
- The notebook identified several products for investigation among the lowest-performing or negative-performing sales/profit records, including Bayou Satsuma Rum Liqueur and Havana Club variants.
- Brand-count analysis did not establish that supplying the largest number of brands automatically results in the highest gross profit.
- Both product-level profitability and vendor-level contribution should be considered when reviewing brand performance.
Purchase and sales relationships
The correlation analysis reported strong positive relationships between:
- Purchase quantity and sales quantity: approximately 0.994.
- Purchase amount and sales amount: approximately 0.989.
- Sales amount and gross profit: approximately 0.957.
- Purchase amount and gross profit: approximately 0.908.
These relationships indicate that larger purchases and sales generally occurred alongside higher gross profit in this dataset. They do not imply that increasing purchases will always increase profit, particularly where products generate losses or move slowly.
Costs and inventory efficiency
- Freight cost showed a weak positive relationship with gross profit, approximately 0.180.
- Excise tax showed a stronger positive relationship with gross profit, approximately 0.769.
- Stock turnover showed a positive relationship with profit margin, approximately 0.600.
- Stock turnover had almost no linear relationship with gross profit, approximately -0.033.
The medium freight-cost category had the highest number of records and the highest total gross profit, but also the highest recorded losses. Low-turnover records contributed the highest total gross profit, largely in a context where that category contained more records. High-turnover records had a slightly higher average profit per order according to the notebook's interpretation.

These findings illustrate why totals, averages, and margins should be examined together.

✅ **12. Business Recommendations**

Based on the analysis, the following actions are recommended.

Review loss-making vendors and products. Investigate the 12 vendors highlighted in the notebook and examine their purchase costs, sales revenue, freight costs, pricing, and profit margins before making supplier decisions.

Evaluate vendors using multiple metrics. Consider total sales, gross profit, profit margin, purchase expenditure, and loss exposure. A vendor with high sales is not necessarily the most profitable vendor.

Improve purchasing decisions. Compare purchase quantities with actual sales quantities and avoid buying more than demand justifies. High purchase values should be assessed against expected sales and inventory requirements.

Investigate slow-moving products. Use product sales quantity and stock-turnover measures to identify items that may require closer inventory monitoring. Review demand before increasing future orders.

Review freight and excise-tax costs. Compare costs against the sales and profit generated by relevant products and vendors. Investigate unusually costly records rather than assuming every high-cost record is inefficient.

Monitor product pricing. Compare purchase prices and selling prices alongside gross profit and profit margin. Positive revenue alone is not sufficient evidence of a healthy contribution.

Monitor vendors over time. Maintain a dashboard that enables the business to track purchase expenditure, sales, gross profit, margins, stock movement, and loss-making records as new data becomes available.

⚖️ **13. Limitations**
    
- The dataset's reporting period is not specified in the notebook.
- The analysis is descriptive and diagnostic; it does not establish that one variable causes another.
- The zero-sales-quantity filter removes 178 records from the original dataset. Unsold purchased products could be operationally important, so those records should be reviewed separately if inventory risk is a priority.
- Winsorization creates capped versions of numerical columns and can affect the distribution of extreme values. The original columns are preserved in the notebook.
- The OrderSize feature is based on Volume, so the category should not be interpreted as a classification of order quantity.
- The initial analysis flagged non-finite profit-margin values. Further data-quality checks are recommended before relying on all margin calculations and statistical summaries.
- The confidence interval uses a normal approximation and should be interpreted cautiously because the gross-profit distribution is skewed.
- The statistical tests depend on their assumptions; significant p-values alone do not establish business causation.
  
🚀 **14. Future Enhancements**
  
- Develop a predictive model to flag potentially loss-making vendors and forecast vendor profitability.
- Compare suitable models using cross-validation and relevant metrics such as precision, recall, F1-score, and ROC-AUC.
- Introduce vendor segmentation using purchase value, sales performance, profit contribution, and profit margin.
- Improve the Power BI dashboard with interactive vendor rankings, product-level loss analysis, purchase/sales comparisons, and inventory indicators.
- Develop interactive Plotly visualizations to support deeper data exploration.
- Automate data preparation, reporting, and dashboard refreshes to support regular monitoring.
- Strengthen validation of non-finite values and evaluate the effect of outlier treatment on reported metrics.

🏁 **15. Conclusion**
  
The Vendor Performance Analysis project demonstrates how Python can be used to evaluate vendor contributions, product performance, profitability, costs, and inventory efficiency in a retail and supply chain setting.

The analysis found that purchase quantity, sales quantity, sales revenue, and gross profit were strongly related in the dataset. However, higher sales and purchases did not guarantee stronger profit margins, and a number of vendors and products required further investigation because of recorded losses.

Stock turnover was positively related to profit margin, while freight cost had a weak relationship with gross profit. The results also showed that vendor performance cannot be judged solely by sales revenue or the number of brands supplied.

The findings support a more comprehensive approach to vendor management: monitor gross profit and profit margin together, investigate loss-making products and vendors, control purchasing and logistics costs, and align inventory decisions with sales demand.

Overall, the project applies exploratory data analysis, data cleaning, feature engineering, statistical analysis, and visualization to convert vendor sales data into actionable business insights


## 👩‍💻 Author

**Shanthini M**  
Aspiring Data Analyst  
Skills: Python | Pandas | NumPy | Matplotlib | Seaborn | SciPy | Exploratory Data Analysis | Statistical Analysis | Data Visualization | Power BI

## 📄 License

This project is developed for educational purposes to demonstrate practical skills in data analysis, statistical techniques, data visualization, and business intelligence.

## 🙏 Acknowledgments

I would like to thank:

- **Entri Elevate Course Support** for providing guidance, learning resources, and support throughout this project.
- **Python Documentation** for valuable references and support in understanding Python and its libraries.
- **Pandas and NumPy Documentation** for guidance on data manipulation, preprocessing, and numerical analysis.
- **Matplotlib, Seaborn Documentation and PowerBI** for helping create visualizations and explore data patterns.
- **SciPy Documentation** for references on statistical analysis and hypothesis testing.
- **Google Colab** for providing an interactive environment to execute Python code and analyze data.
- **Microsoft Power BI** for enabling the creation of interactive dashboards and visual reports.

