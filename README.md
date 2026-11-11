# Do Strong Financial Fundamentals Lead to Higher Stock Returns?

**An empirical analysis of S&P 500 companies using Python, pandas, and regression modeling.**

This project tests a common investing assumption: that companies with strong fundamentals (profitable, liquid, and low in debt) also make strong stocks. Using several years of financial statement data and historical stock prices, I analyze price movements, market trends, and volatility, and build regression models to measure how much fundamentals actually explain stock performance.

**Author:** Ruba Abdelgalil<br>
**Notebook:** [`Ruba_Abdelgalil_Independent_Project.ipynb`](Ruba_Abdelgalil_Independent_Project.ipynb)

---

## Key Findings

- **Fundamentals explain very little of stock returns.** Most of the variation comes from how the overall market performed in a given year.
- **Same-year relationships are counterintuitive.** Companies with higher profit margins had *lower* returns, while more liquid companies performed slightly better.
- **Fundamentals don't predict next year's returns.** The only consistent effect was firm size: larger companies earned lower returns in both the same and the following year.
- **Conclusion:** markets appear to price in public accounting information quickly, leaving investors little edge from it.

## Skills Demonstrated

| Area | Details |
|------|---------|
| **Data wrangling** | Merging price and financial statement datasets, computing annual returns, building financial ratios |
| **Data cleaning** | Split-adjusted prices, missing-value handling, winsorizing outliers at the 1st/99th percentiles |
| **Exploratory analysis** | Summary statistics, correlation matrices, scatter plots |
| **Statistical modeling** | OLS regression with year fixed effects, clustered standard errors, VIF multicollinearity checks |
| **Research design** | Model comparison (R-squared), out-of-sample timing test, standardized effect sizes |
| **Communication** | Clear written interpretation of results for a non-technical audience |

## Data

- **Source:** [NYSE dataset on Kaggle](https://www.kaggle.com/datasets/dgawlik/nyse), downloaded programmatically with `kagglehub`
- **`fundamentals.csv`:** annual financial statements for S&P 500 companies
- **`prices-split-adjusted.csv`:** daily stock prices adjusted for stock splits, so a 2-for-1 split doesn't appear as a 50% loss

## Methodology

1. **Annual returns:** calculated from each company's last closing price of each year, then matched to the same fiscal year's financial statements.
2. **Variables:**
   - *Profitability:* after-tax ROE, profit margin, gross margin
   - *Liquidity:* current ratio
   - *Leverage:* long-term debt / total assets
   - *Firm size:* log of total assets
3. **Outliers:** each variable winsorized at the 1st and 99th percentiles.
4. **Exploratory analysis:** distributions, correlations, and visual checks before modeling.
5. **Regression:** OLS of annual returns on the six fundamentals, with year controls to absorb market-wide movements.
6. **Diagnostics:** variance inflation factors and standard errors clustered by company.
7. **Explanatory power:** compared against a year-controls-only model to isolate what fundamentals add.
8. **Predictive test:** used this year's fundamentals to predict *next* year's returns, since annual reports are published after the fiscal year ends.
9. **Effect sizes:** standardized coefficients to compare which factors matter most.

## Tools

Python · pandas · NumPy · Matplotlib · Seaborn · statsmodels · Jupyter · kagglehub

## How to Run

```bash
git clone https://github.com/rabdelgalil/financial-stock-analysis.git
cd financial-stock-analysis
pip install pandas numpy matplotlib seaborn statsmodels kagglehub jupyter
jupyter notebook Ruba_Abdelgalil_Independent_Project.ipynb
```

Run all cells. The dataset downloads automatically through `kagglehub` (a Kaggle API token may be required).
