# Life Expectancy vs Internet Usage & GDP per Capita Analysis

This project explores the relationship between life expectancy, internet usage percentage, and GDP per capita using World Bank data for the year 2019.

## Data Sources

All data from [World Bank Open Data](https://data.worldbank.org/):

| Indicator | Code | Description |
|-----------|------|-------------|
| Internet users (% of population) | `IT.NET.USER.ZS` | Percentage of individuals using the internet |
| Life expectancy at birth (years) | `SP.DYN.LE00.IN` | Average number of years a newborn is expected to live |
| GDP per capita (current US$) | `NY.GDP.PCAP.CD` | Gross domestic product divided by midyear population |

## Methodology

1. **Data Loading**: Load three World Bank CSV files (skipping 4 header rows)
2. **Data Cleaning**: 
   - Keep only Country Name, Country Code, and 2019 values
   - Merge datasets on country/country code (inner join, one-to-one)
   - Drop rows with missing values in any of the three variables
   - Filter out rows with GDP per capita ≤ 0
   - Create log-transformed GDP per capita (`log_gdp_per_capita = log10(gdp_per_capita)`) to handle skewness

## Key Findings

### Internet Usage vs Life Expectancy
- **Positive association**: Countries with higher internet usage percentages tend to have higher life expectancy
- Scatter plot shows a general upward trend

### GDP per Capita vs Life Expectancy
- **Positive association**: Higher GDP per capita correlates with higher life expectancy
- **Raw GDP per capita is heavily right-skewed** — most countries cluster at low values with a long tail of wealthy outliers
- **Log-transformed GDP per capita** shows a clearer linear relationship with life expectancy

### Confounding Variable
**GDP per capita** is a likely confounder explaining the internet–life expectancy relationship:
- Wealthier countries (high GDP) can afford both better healthcare (higher life expectancy) and better internet infrastructure (higher internet usage)
- The observed internet–life expectancy association may be partly or largely driven by underlying economic development

## Project Structure

```
ITusg/
├── data/                    # Raw World Bank CSV files
├── notebook/
│   └── Explore.ipynb        # Main analysis notebook
├── output/                  # Generated outputs (empty currently)
└── README.md                # This file
```

## Running the Analysis

```bash
# Install dependencies
pip install pandas matplotlib seaborn jupyter

# Launch notebook
cd notebook
jupyter notebook Explore.ipynb
```

## Exercise Reference

Based on OpenIntro Statistics textbook exercise:
> "Describe the relationship between life expectancy and percentage of internet users. Also state a possible confounding variable that might explain this relationship and describe its potential effect."

**Answer**: There is a positive association between internet usage and life expectancy. GDP per capita is a confounding variable — wealthier nations have both higher life expectancy (better healthcare, nutrition) and higher internet usage (better infrastructure), potentially explaining the observed correlation.