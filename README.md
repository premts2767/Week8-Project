# Nova Conglomerate: Complete Business Analysis & Operational Optimization Capstone Project

**Data Science Internship - Week 8 Capstone Project Submission**

---

## 1. Project Overview

Nova Conglomerate is a multi-sector enterprise operating across retail, telecommunications, and real estate markets. This project provides a comprehensive, end-to-end analytical assessment of Nova's three primary operating divisions. By analyzing transaction-level sales patterns, customer churn rates, and property valuations, this portfolio identifies optimizations to boost revenue, enhance customer retention, and refine real estate valuations.

### Business Problems & Objectives
1. **Nova Retail Division**:
   - *Problem*: Lack of structured insights regarding product margins, regional distributions, and how price elasticity impacts consumer volumes.
   - *Objective*: Identify core revenue drivers via Pareto (80/20) analysis, and model the price elasticity of demand to assess product pricing power.
2. **Nova Telecom Division**:
   - *Problem*: High subscriber churn impacting recurring monthly revenues.
   - *Objective*: Leverage statistical hypothesis testing (Chi-Square & T-Test) to isolate churn drivers, and deploy unsupervised clustering (K-Means) to identify high-risk customer segments.
3. **Nova Property Division**:
   - *Problem*: Property asset valuations are based on subjective comparisons rather than statistical coefficients.
   - *Objective*: Build an Ordinary Least Squares (OLS) Multiple Linear Regression model explaining house prices, and extract precise valuation multipliers for property size, room count, building age, and geographical location.

### Project Scope & KPIs
- **Scope**: Rigorous, reproducible analysis of three historical files: `sales_data.csv` (100 rows), `customer_churn.csv` (500 rows), and `house_prices.csv` (300 rows). Zero simulated or generated data was introduced.
- **Key Performance Indicators (KPIs)**:
  - *Retail*: Total Sales Revenue, Average Order Value (AOV), Sales Volume, Price Elasticity Coefficient.
  - *Telecom*: Baseline Churn Rate, Contract-specific Churn Risk, Customer Segment Churn Probability.
  - *Property*: Valuation Model R-squared ($R^2$), Bedroom Valuation Premium ($/room), Annual Property Depreciation Rate ($/year).

---

## 2. Setup & Installation Instructions

### Required Libraries
To execute the analysis notebook and compile the deliverables, you need Python 3.8+ and the following packages:
- `pandas` (Data loading and manipulation)
- `numpy` (Numerical operations)
- `matplotlib` & `seaborn` (Visual charts and styling)
- `scipy` (Hypothesis testing)
- `statsmodels` (OLS regressions)
- `scikit-learn` (Standard Scaling & K-Means clustering)
- `reportlab` (Programmatic PDF report generation)
- `python-pptx` (Programmatic PPTX presentation compilation)
- `openpyxl` (Excel engine dependency)

### Installation Steps
1. Clone or copy the project directory to your local system:
   ```bash
   cd c:\Users\ROG\Desktop\Documents\Internship\week8
   ```
2. Install all required dependencies from the provided `requirements.txt`:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the complete analysis in the Jupyter Notebook:
   ```bash
   jupyter notebook capstone_analysis.ipynb
   ```
4. (Optional) Recompile PDF and PowerPoint files using the generator scripts:
   ```bash
   python C:\Users\ROG\.gemini\antigravity-ide\brain\3dc780ab-8a67-4f42-9c6f-76520030d615\scratch\build_reports.py
   python C:\Users\ROG\.gemini\antigravity-ide\brain\3dc780ab-8a67-4f42-9c6f-76520030d615\scratch\build_presentation.py
   ```

---

## 3. Repository File Structure

```directory
week8/
├── sales_data.csv                    # Raw sales transaction dataset (100 rows)
├── customer_churn.csv                # Raw customer subscription dataset (500 rows)
├── house_prices.csv                  # Raw property valuation dataset (300 rows)
├── capstone_analysis.ipynb           # Primary executed analytical notebook
├── requirements.txt                  # List of Python library dependencies
├── README.md                         # Main project documentation (this file)
├── reports/
│   ├── technical_report.pdf          # Programmatically compiled technical PDF report
│   ├── executive_summary.pdf         # Programmatically compiled 2-page brief PDF report
│   └── assets/                       # High-resolution visual charts
│       ├── sales_product.png         # Revenue vs. Volume by product
│       ├── sales_region.png          # Geographic revenue contribution pie chart
│       ├── churn_contract.png        # Subscriber churn rate by contract length
│       ├── churn_segments.png        # Customer segmentation scatter plot
│       ├── house_regression.png      # Property valuation actual vs. predicted plot
│       └── house_boxplot.png         # Property price distribution boxplot
└── presentation/
    └── business_presentation.pptx    # Programmatically compiled slides presentation
```

---

## 4. Technical Details & Methods Used

### Statistical Hypothesis Testing (Telecom Churn)
1. **Chi-Square Test of Independence**:
   - *Goal*: Determine if Churn is independent of Contract Type (Month-to-month, One-year, Two-year).
   - *Test Formula*: $\chi^2 = \sum \frac{(O - E)^2}{E}$
   - *Finding*: Rejected the null hypothesis ($p = 9.59 \times 10^{-7}$). Month-to-month subscriptions have a significantly higher churn risk (20.59%).
2. **Two-Sample Independent T-Test**:
   - *Goal*: Compare average Monthly Charges of churned vs. active customers.
   - *Finding*: Rejected the null hypothesis ($p = 0.0101$). Churned customers pay significantly higher monthly charges ($129.77 mean vs. $111.72 active), indicating cost-sensitivity churn.

### Customer Segmentation (K-Means Clustering)
- **Features Used**: `Tenure` (months) and `MonthlyCharges` ($).
- **Preprocessing**: Scaled features using `StandardScaler` to achieve zero mean and unit variance.
- **Clustering Algorithm**: $K$-Means clustering ($K=3$) to profile subscribers:
  - **Cluster 0 ("Stable Low-Cost")**: High tenure, low monthly cost, 0.0% churn.
  - **Cluster 1 ("High Risk / New")**: Low tenure, high monthly cost, 28.65% churn. *Primary tactical retention group.*
  - **Cluster 2 ("Premium High-Value")**: High tenure, high monthly cost, 0.0% churn. Highly loyal premium tier.

### Multiple Linear Regression (Property Valuations)
- **Features Used**: `Area` (sq ft), `Bedrooms` (count), `Bathrooms` (count), `Age` (years), `Location` (Rural, Suburb, City Center), `Property_Type` (Apartment, House, Villa).
- **Categorical Encoding**: Dummy one-hot encoding (dropped first column to prevent multicollinearity).
- **Valuation Equation**:
  $$\text{Price} = 8.13\text{M} + 7615 \times \text{Area} + 1.67\text{M} \times \text{Bedrooms} + 645,500 \times \text{Bathrooms} - 83,790 \times \text{Age} - 16.54\text{M} \times \text{Rural} - 8.35\text{M} \times \text{Suburb}$$
- **Model Quality**: Adjusted $R^2 = 0.954$, indicating 95.4% of the valuation variance is captured.

---

## 5. Visual Documentation (Generated Charts)

These high-resolution visual charts are saved dynamically to `reports/assets/` and integrated into the primary Jupyter Notebook and compiled reports:

### Figure 1: Product Performance & Regional Sales Contribution
- **Product Performance** (`sales_product.png`): Displays total revenue (bar chart, left y-axis) vs. quantity sold (line plot, right y-axis). Shows Laptops commanding top revenue.
- **Regional Sales** (`sales_region.png`): Pie chart depicting geographical revenue splits. North and South regions represent the top revenue hubs (62.4% cumulatively).

### Figure 2: Telecom Customer Churn Drivers & Segment Profile
- **Churn by Contract** (`churn_contract.png`): Highlights the contrast in churn rate between Month-to-month contracts (20.6%) and multi-year tiers.
- **K-Means Scatter Plot** (`churn_segments.png`): Maps subscriber groups along Monthly Charges (y-axis) vs. Tenure (x-axis), with data points styled by churn status. Isolates K-Means Cluster 1 as the high-risk segment.

### Figure 3: Property Pricing Dynamics
- **Pricing Distribution** (`house_boxplot.png`): Grouped boxplot of housing prices broken down by location (Rural, Suburb, City Center) and property type (Apartment, House, Villa).
- **Valuation Regression Model** (`house_regression.png`): Scatters actual prices against model predicted prices, overlaid with the regression fit line and a 45-degree reference line to illustrate residual fit.

---

## 6. Testing Evidence & Result Verification

The analysis results have been successfully cross-verified across all output formats (Jupyter Notebook cells, PDF reports, and PPTX presentation slides):

### Model and Analysis Validation Table
| Analysis Metric | Notebook Computed Value | Technical PDF Value | PPTX Slides Value | Status |
| :--- | :--- | :--- | :--- | :--- |
| **Sales Revenue** | Laptops: \$3,889,210 | Laptops: \$3,889,210 | Laptops: \$3,889,210 | Verified & Matches |
| **Price Elasticity p-value** | 0.937 (Inelastic) | 0.937 (Inelastic) | 0.937 (Inelastic) | Verified & Matches |
| **Telecom Churn Rate** | 10.60% | 10.60% | 10.60% | Verified & Matches |
| **Chi-Square p-value** | $9.59 \times 10^{-7}$ | $9.59 \times 10^{-7}$ | $9.59 \times 10^{-7}$ (p < 0.001) | Verified & Matches |
| **T-Test p-value** | 0.0101 | 0.0101 | 0.0101 | Verified & Matches |
| **Cluster 1 Churn Rate** | 28.65% | 28.65% | 28.65% | Verified & Matches |
| **Property Model $R^2$** | 95.5% (Adj: 95.4%) | 95.5% (Adj: 95.4%) | 95.4% (Adjusted) | Verified & Matches |
| **Bedroom Coefficient** | \$1,670,000 | \$1,670,000 | \$1.67M | Verified & Matches |
| **Rural Location Coefficient**| -\$16,540,000 | -\$16,540,000 | -\$16.54M | Verified & Matches |

All calculations compile deterministically and are submission-ready.
