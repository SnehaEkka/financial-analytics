# Identifying Financial Risk: Z-Score Analysis of Company Data

This project analyzes a panel of company financial data to assess organizational financial health using Altman's Z-score model. The workflow mirrors industry-standard risk analytics and statistical modeling procedures. Below is an overview of the methodology and key results, structured for maximum clarity and reproducibility for both academic and practical audiences.

## **Tools Used** 
- Python (pandas, numpy, statsmodels)
- WRDS Compustat data

## Dataset Overview

- **Source:** Compustat financial statement data (assign1-fix.csv)
- **Sample:** 4,143 companies for fiscal year 2022
- **Key Variables:**
  - Current Assets (act), Total Assets (at)
  - EBIT (ebit), Current Liabilities (lct), Total Liabilities (lt)
  - Retained Earnings (re), Sales (sale)
  - Market Value of Equity (mve), Sector (gsector), Stock price (prcc_c)
- Data includes identifiers such as GVKEY, ticker symbol, and company name.
- Financial figures are in millions of USD.

## Method & Analysis

### **Data Cleaning and Preprocessing**

- **Data Integration:** Financial data for 4,143 companies (2022, multiple industries) were combined into a single DataFrame.
- **Outlier Treatment:** Key ratio variables used in Z-score calculation were winsorized at the 1st and 99th percentiles, ensuring extreme outlier effects do not distort results.
- **Transformation:** Because firm size (measured as sales and assets) is highly skewed, the natural logarithm of the "at" (total assets) and "sale" (total sales) variables was computed to normalize these distributions.

### **Z-Score Calculation**

The Altman's Z-Score formula, specialized for non-manufacturing firms, was calculated as:

$$Z = 1.2A + 1.4B + 3.3C + 0.6D + 1.0E$$

Where:
- $$A = \frac{\text{working capital}}{\text{total assets}} = \frac{\text{act} - \text{lct}}{\text{at}}$$
- $$B = \frac{\text{retained earnings}}{\text{total assets}} = \frac{\text{re}}{\text{at}}$$
- $$C = \frac{\text{EBIT}}{\text{total assets}} = \frac{\text{ebit}}{\text{at}}$$
- $$D = \frac{\text{market value of equity}}{\text{total liabilities}} = \frac{\text{mve}}{\text{lt}}$$
- $$E = \frac{\text{sales}}{\text{total assets}} = \frac{\text{sale}}{\text{at}}$$

A higher Z-Score signals greater financial stability and lower bankruptcy risk.

### **Descriptive Statistics and Zone Classification**

- **Overall Sample (All Sectors):**
  - The mean Z-Score is slightly below zero, indicating a non-trivial share of companies facing financial challenges.
  - The data display a wide dispersion—some companies show strong financial health with high Z-Scores, while others are in severe distress.

- **Industry Analysis:**
  - For each GICS sector, descriptive metrics (mean, median, min, max, std) for Z-Score and log(assets) were computed.
  - Patterns emerged, such as negative average Z-Scores in health care and limited variability but lower Z-Scores in utilities, likely reflecting industry-specific risk structures.
  
- **Zone Classification:**
  - Companies are classified as "Safe Zone" (Z > 2.99), "Grey Zone" (1.81 < Z < 2.99), or "Distress Zone" (Z < 1.81).
  - The percentage of companies in each zone was reported, revealing the proportion of firms at risk of bankruptcy versus those with solid financial footing.

### **Most Distressed Companies**

- The 10 companies with the lowest Z-Scores were identified, along with their names and industry sector codes.
- These firms uniformly fell into the "Distress Zone," with extremely negative Z-Scores, suggesting imminent or ongoing financial distress. This highlights the method's sharpness for flagging outliers deserving more scrutiny.

### **Regression Analysis: Size and Financial Health**

- **Model:** A linear regression (OLS) was run:  
  $$\text{Z-Score} = \beta_0 + \beta_1 \cdot \log(\text{sale}) + \epsilon$$
- **Results:**
  - The coefficient on log(sale) was positive and statistically significant, suggesting that, on average, larger companies (by sales) tend to have healthier Z-Scores.
  - The model’s R² was moderate (about 13–14%), indicating a statistically significant but not overwhelming explanatory power. Size matters, but other factors clearly drive financial health.
  - Key statistical outputs (coefficient estimate, t-statistic, p-value, R², Adj-R²) were reported and interpreted.
- **Interpretation:** A one-unit increase in log(sales) (i.e., sales increasing by ~2.7x) is associated with an increase in the Z-Score, improving predicted financial health. However, the relationship is not deterministic—company health is influenced by many factors beyond scale.

### **Key Insights and Discussion**

- **Heterogeneity:** Considerable dispersion exists in company financial health, both within and across sectors.
- **Risk Concentration:** A non-trivial proportion of companies fall into the "Distress Zone," consistent with a period of macroeconomic uncertainty or industry-specific shocks.
- **Predictors of Health:** Company size is a meaningful but incomplete predictor of financial health. Results advocate for multi-factorial models and sector-specific analytical approaches.
- **Sector Interpretation:** Recognition of variable sector characteristics is crucial—direct Z-Score comparisons across industries require careful contextualization.

### **Conclusion**

This analysis provides a rigorous, replicable framework for using classic financial risk models (Altman Z-Score) with modern data science tools. It offers actionable insights for credit analysts, investors, and regulators, as well as a practical template for further research or coursework.

## Business Impact & Interpretation

- This analysis offers a practical tool for investors, creditors, and company management to identify firms at risk of financial distress.
- The Z-Score provides a clear numeric risk indicator to prioritize monitoring and intervention efforts.
- Regression results inform stakeholders that company size, as reflected in sales, is a valuable predictor of financial stability.
- The findings support strategic decisions in lending, investment, and corporate risk management by linking company fundamentals to bankruptcy risk.

## Learning & Takeaways

- Gained experience in financial ratio construction and advanced data cleaning techniques such as winsorization to handle outliers.
- Strengthened understanding of the Altman Z-Score as a predictive tool for financial distress.
- Developed skills in regression modeling to explore the impact of size on financial risk.
- Learned to translate quantitative outputs into actionable business interpretations.

## Project Details

- **Completed:** February 2024
- **Course:** BA870 Financial Analytics, Boston University MSBA
- **Team:**
  - Gunjan Sharma
  - Sneha Ekka

*This README summarizes the analysis pipeline, major findings, and the significance of results, helping future users understand the scope and impact of Z-Score analytics on corporate financial risk assessment.*
