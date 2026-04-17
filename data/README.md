# Dataset

The raw data file (`data.csv`) is not tracked in this repository.

## About the Dataset

| Property | Value |
|---|---|
| Rows | 2,240 customers |
| Columns | 29 features |
| Target | `Response` (binary: accepted/rejected campaign) |
| Positive rate | 14.9% (imbalanced) |

## Columns

| Column | Description |
|---|---|
| `ID` | Customer identifier |
| `Year_Birth` | Year of birth |
| `Education` | Education level |
| `Marital_Status` | Marital status |
| `Income` | Annual household income |
| `Kidhome` | Number of kids at home |
| `Teenhome` | Number of teenagers at home |
| `Dt_Customer` | Date of enrollment |
| `Recency` | Days since last purchase |
| `MntWines` | Spent on wine (last 2 years) |
| `MntFruits` | Spent on fruits (last 2 years) |
| `MntMeatProducts` | Spent on meat (last 2 years) |
| `MntFishProducts` | Spent on fish (last 2 years) |
| `MntSweetProducts` | Spent on sweets (last 2 years) |
| `MntGoldProds` | Spent on gold products (last 2 years) |
| `NumDealsPurchases` | Purchases with discount |
| `NumWebPurchases` | Web purchases |
| `NumCatalogPurchases` | Catalog purchases |
| `NumStorePurchases` | In-store purchases |
| `NumWebVisitsMonth` | Web visits per month |
| `AcceptedCmp1–5` | Whether accepted campaigns 1–5 |
| `Response` | **Target** — accepted last campaign |
| `Complain` | Filed a complaint in last 2 years |
| `Z_CostContact` | Fixed cost column (dropped) |
| `Z_Revenue` | Fixed revenue column (dropped) |

## Engineered Features (created in notebook)

| Feature | Description |
|---|---|
| `Age` | 2024 − Year_Birth |
| `Days_Customer` | Days since enrollment |
| `TotalMnt` | Sum of all product spending |
| `TotalPurchases` | Sum of all purchase channels |
| `TotalAccepted` | Sum of all accepted campaigns (1–5) |
| `TotalDependents` | Kidhome + Teenhome |

## How to Obtain

This dataset is from a public iFood data science case study. You can find it on:

- [Kaggle — iFood Data Analyst Case](https://www.kaggle.com/datasets/jackdaoud/marketing-data)

After downloading, rename the file to `data.csv` and place it in this `data/` folder.
