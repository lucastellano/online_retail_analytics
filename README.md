# Online Retail Analytics

Exploratory analysis and customer segmentation on a transactional dataset from a UK-based online retailer (2009–2011).

## Objective

Answer key business questions from transactional data:
- How did revenue evolve over time?
- Which products and markets generate the most value?
- How can customers be segmented based on purchasing behavior?

## Dataset

**Source:** Online Retail II — UCI Machine Learning Repository via Kaggle

**Description:** Real transactional data from a UK-based online retailer between December 2009 and December 2011. Includes sales to both retail and wholesale customers, mainly across Europe.

| Column | Description |
|---|---|
| Invoice | Invoice number (prefix 'C' indicates cancellation) |
| StockCode | Product code |
| Description | Product name |
| Quantity | Quantity per transaction (negative = return) |
| InvoiceDate | Transaction date and time |
| Price | Unit price in British pounds (£) |
| Customer ID | Unique customer identifier |
| Country | Customer country |

## Technologies

- Python 3
- pandas
- numpy
- matplotlib
- seaborn
- Google Colab

## Project Structure

The analysis is organized in a single notebook with the following stages:

**1. Data Loading & Initial Exploration**
Loading the dataset, inspecting structure, data types, missing values, and descriptive statistics.

**2. Data Cleaning**
- Removal of cancellations (invoices with prefix 'C') and accounting adjustments (prefix 'A')
- Removal of rows with negative or zero Quantity or Price
- Conversion of InvoiceDate to datetime format
- Creation of Revenue column (Quantity × Price)
- Rows with null Customer ID are kept for general analysis and filtered only for RFM segmentation

**3. Business Metrics Analysis**
- Total revenue and monthly trend
- Top 10 products by revenue
- Top 10 countries by revenue (excluding the UK)

**4. Visualizations**
- Monthly revenue trend line (2009–2011)
- Bar chart: top 10 products by revenue
- Bar chart: top 10 countries by revenue

**5. RFM Segmentation**
Segmentation of 5,862 identified customers into five groups based on purchasing behavior: VIP, Loyal, New or Promising, At Risk, and Lost.

## Key Findings

- **Total revenue:** £20.9 million over two years
- **Clear seasonality:** October, November, and December concentrate revenue peaks in both years, with November 2011 as the record month (£1.5M) — strong dependency on the holiday season
- **Top product:** REGENCY CAKESTAND 3 TIER generated £344,563 over the period, nearly double the second-ranked product
- **Concentrated market:** The UK dominates sales. Among international markets, Ireland (EIRE) and the Netherlands lead with £640K and £550K respectively
- **Customer segmentation:**

| Segment | Customers | % |
|---|---|---|
| Lost | 2,043 | 35% |
| Loyal | 1,381 | 24% |
| At Risk | 888 | 15% |
| New or Promising | 888 | 15% |
| VIP | 662 | 11% |

The "At Risk" segment represents an immediate retention opportunity: customers with high historical frequency who recently stopped purchasing.

## How to Reproduce

1. Clone the repository
2. Download the dataset from Kaggle and place it in the root folder
3. Open the notebook in Google Colab or Jupyter
4. Run the cells in order

## Analytical Decisions

- **Exclusion of UK in country analysis:** The UK accounts for over 90% of transactions. It is excluded to better visualize the distribution across international markets.
- **RFM segmentation criteria:** Segments are defined primarily using R (Recency) and F (Frequency) scores. M (Monetary) is incorporated only for the VIP classification, where economic value is a key differentiator.
- **Null Customer IDs:** Represent 23% of the dataset (anonymous purchases). Kept for revenue and product analysis, excluded only for RFM segmentation where customer identification is required.
