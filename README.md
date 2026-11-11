# Do Companies with Stronger Financial Fundamentals Generate Higher Stock Returns?

An independent financial analysis project in Python that examines stock market data, analyzes historical price movements, and explores trends in financial markets. Using data analysis, visualization, and regression techniques, it investigates market behavior and volatility, and tests whether "good" companies (profitable, liquid, low debt) actually make good stocks.

**Author:** Ruba Abdelgalil

## Overview

A common assumption in investing is that companies with strong fundamentals should also deliver strong stock returns. This project puts that idea to the test using financial statements and historical stock prices for S&P 500 companies, asking whether profitability, liquidity, leverage, and firm size are related to annual stock returns.

## Key Findings

- **Fundamentals explain very little.** Most of the variation in stock returns comes from how the overall market performed in a given year.
- **Same-year effects are mixed.** Companies with higher profit margins actually had lower returns, while companies with more liquidity did slightly better.
- **Little predictive power.** None of those relationships held when predicting the *next* year's returns. The only consistent result was size: larger companies earned lower returns in both the same year and the following year.
- **Takeaway:** markets appear to price in public accounting information quickly, so it offers investors little edge.

## Data

- **Source:** [NYSE dataset on Kaggle](https://www.kaggle.com/datasets/dgawlik/nyse) (downloaded with `kagglehub`)
- **Files used:**
  - `fundamentals.csv`: annual financial statement data for S&P 500 companies
  - `prices-split-adjusted.csv`: daily stock prices adjusted for stock splits (so a 2-for-1 split doesn't look like a 50% loss)

## Methodology

1. **Data preparation:** Calculated annual returns from each company's last closing price of the year and matched them to the same fiscal year's financial statements.
2. **Variable construction:**
   - *Profitability:* after-tax ROE, profit margin, gross margin
   - *Liquidity:* current ratio
   - *Leverage:* long-term debt / total assets
   - *Size:* log of total assets
3. **Outlier handling:** Winsorized each variable at the 1st and 99th percentiles.
4. **Exploratory data analysis:** Summary statistics, correlation matrix, and scatter plots.
5. **Regression modeling:** OLS regression of annual returns on the six fundamentals, with year controls to account for market-wide movements.
6. **Model diagnostics:** Variance inflation factors (VIFs) to check multicollinearity, and standard errors clustered by company.
7. **Explanatory power:** Compared the full model's R-squared against a year-controls-only model to isolate what fundamentals add.
8. **Predictive test:** Re-ran the model using fundamentals to predict *next* year's returns, since annual reports are released after the fiscal year ends.
9. **Effect sizes:** Compared standardized coefficients to see which factors matter most.

## Tools & Libraries

- Python
- pandas, NumPy
- Matplotlib, Seaborn
- statsmodels
- kagglehub

## Repository Structure

| File | Description |
|------|-------------|
| `Ruba_Abdelgalil_Independent_Project.ipynb` | Main notebook with the full analysis, commentary, and findings |
| `Project.ipynb` | Earlier working version of the analysis |
| `README.md` | Project overview |

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/rabdelgalil/financial-stock-analysis.git
   cd financial-stock-analysis
   ```
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn statsmodels kagglehub jupyter
   ```
3. Open the notebook:
   ```bash
   jupyter notebook Ruba_Abdelgalil_Independent_Project.ipynb
   ```
4. Run all cells. The dataset downloads automatically through `kagglehub` (a Kaggle account/API token may be required).
