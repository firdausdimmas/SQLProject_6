# Analyze International Debt Statistics

### Project Overview

![dollar](https://github.com/user-attachments/assets/1b92c27b-b4f9-487e-ab18-ce4ac0300ad8)

This project analyzes international debt data collected by The World Bank, focusing on the debt owed by developing countries across various categories. The objective of this project is to uncover key insights about the debt situation among these nations, including identifying the largest debtors, understanding debt distribution by category, and recognizing overall debt trends. Through this analysis, we aim to provide a clearer understanding of how debt supports economic development in developing countries and offer valuable insights for stakeholders and policymakers.

### Data Sources

Below is a description of the table worked with:

<h4><code>international_debt</code> table</h4>

<table>
  <thead>
    <tr>
      <th>Column</th>
      <th>Definition</th>
      <th>Data Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>country_name</code></td>
      <td>Name of the country</td>
      <td><code>varchar</code></td>
    </tr>
    <tr>
      <td><code>country_code</code></td>
      <td>Code representing the country</td>
      <td><code>varchar</code></td>
    </tr>
    <tr>
      <td><code>indicator_name</code></td>
      <td>Description of the debt indicator</td>
      <td><code>varchar</code></td>
    </tr>
    <tr>
      <td><code>indicator_code</code></td>
      <td>Code representing the debt indicator</td>
      <td><code>varchar</code></td>
    </tr>
    <tr>
      <td><code>debt</code></td>
      <td>Value of the debt indicator for the given country (in current US dollars)</td>
      <td><code>float</code></td>
    </tr>
  </tbody>
</table>

### Exploratory Data Analysis

EDA involved exploring the international debt table to answer key questions, such as:
- What is the number of distinct countries present in the database?
- What country has the highest amount of debt?
- What country has the lowest amount of repayments?

### Data Analysis

Including some interesting code/features worked with

```sql
-- num_distinct_countries 
SELECT COUNT(DISTINCT country_name) as total_distinct_countries
FROM international_debt;
```

```sql
-- highest_debt_country 
SELECT country_name,
       SUM(debt) as total_debt
FROM international_debt
GROUP BY country_name
ORDER BY total_debt DESC
LIMIT 1;
```

```sql
-- lowest_principal_repayment 
SELECT country_name,
       indicator_name,
       MIN(debt) as lowest_repayment
FROM international_debt
WHERE indicator_code = 'DT.AMT.DLXF.CD'
GROUP BY country_name, indicator_name
ORDER BY lowest_repayment ASC
LIMIT 1;
```

### Results/Findings

The analysis results are summarized as follows:
- There are 124 distinct developing countries recorded in the international debt dataset.
- The country with the highest total debt is China, with a total debt amounting to approximately $285 billion USD.
- The country with the lowest principal repayments (indicator: DT.AMT.DLXF.CD) is Timor Leste, with repayments as low as $825,000 USD.

### Recommendations

Based on the analysis, we recommend the following actions:
- The World Bank should prioritize support for countries with critical needs and lower debt burdens to promote balanced global development.
- Regularly monitor debt sustainability in such high-borrowing nations to avoid long-term financial strain, both domestically and globally.
- Continued support low-repayment countries through flexible repayment terms, grants, or technical assistance.
