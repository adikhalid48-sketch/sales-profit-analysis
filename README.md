# Sales vs Profit Analysis: US Retail 2019-2020

An exploratory data analysis (Python) and an interactive Power BI dashboard on a US retail orders dataset.

**The main finding:** sales grew 77% from 2019 to 2020, but profit only grew 14%. The business sold much more and kept very little of it. This project finds where the profit went.

## Dashboard

**Page 1: Overview.** KPIs, sales vs profit by month, margin by category and year, plus slicers for Year, Region, Category and Odd Profit.

![Overview page](Dashboard/overview.png)

**Page 2: Where We Lose Money.** Profit by sub-category, profit by state, return rate by region and the top returning customers.

![Where We Lose Money page](Dashboard/where-we-lose-money.png)

> In Power BI Desktop, hold **Ctrl** and click to use the page buttons.

## Dataset

- `Data/sales_data.csv`: 5,901 order lines (rows), 3,003 unique orders and 773 customers, from January 2019 to December 2020.
- Columns include order and ship dates, ship mode, customer, segment, city, state, region, category, sub-category, sales, quantity, profit, returns and payment mode.
- There is **no cost or discount column**, so the analysis shows *what* happened but can't prove *why*.

## Tools

Python (pandas, matplotlib, seaborn) in Jupyter, and Power BI Desktop (DAX measures, slicers, conditional formatting).

## Questions I asked

1. Which regions, categories and states make money, and which lose it?
2. Sales grew a lot from 2019 to 2020. Did profit grow with it?
3. Where do returns come from?
4. Is the data clean enough to trust?

## Key findings

1. **Sales grew, profit didn't.** Sales went from about 565K (2019) to 1.0M (2020), but profit only went from about 82K to 93K. Margin fell from 14.5% to 9.3%.
2. **Office Supplies drove the growth** (175K to 469K), but its margin dropped from 20.0% to 8.5%. Binders, Art and Paper fell the most.
3. **Technology is the most profitable** (about 19% margin). **Furniture is weak** (about 2%). Tables lose money overall (-9.3%) and in every region. Supplies also lose money.
4. **Loss-making states:** Texas, Illinois, Ohio, Pennsylvania and Colorado. The top profit comes from California, New York and Washington.
5. **Central has the lowest margin** (8.0%), driven by Furnishings, Bookcases and Binders. West has the best (13.0%).
6. **Returns are concentrated.** 4.9% of rows and 3.5% of orders (104 of 3,003) are returned. West is the outlier (7.3% of orders), and it comes from a few customers: the top 12 returners account for 31% of returned rows. Shipping time, order size and profit have no link with returns.
7. **Ship Mode, Segment and Payment Mode are flat.** They show no big differences in sales, margin or returns.
8. **Data quirks.** 14 rows have profit greater than sales, which can't happen in a normal sale. They inflate the Copiers margin (71.6% drops to 40.5% without them) and the overall margin (11.2% vs 9.4%). They are flagged, not deleted.

## Data cleaning

- Dropped two empty columns (`ind1`, `ind2`).
- Returns: filled blanks with 0, so 0 means not returned and 1 means returned.
- Converted order and ship dates to real dates (month/day/year).
- Flagged the 14 rows where profit is greater than sales in an `Odd Profit` column, so they can be hidden in the dashboard.
- Kept the 19% Profit outliers, since they look like real orders. Kept the 108 rows that lose more than their sales, since that is possible with discounts or high costs.

## How rows, orders and returns are counted

A **row** is one product line, and an **order** can have several rows. When an order is returned, all its rows are marked returned. So the return rate is shown at the **order level** in the dashboard (returned orders ÷ orders). The notebook shows both the row-level and order-level numbers.

## Suggestions from the analysis

These come from the numbers above. They would need cost and discount data to confirm.

- Review pricing and discounts on Tables, Supplies and Bookcases.
- Look into why Office Supplies margin fell in 2020 (Binders, Art, Paper), and why Central's Furniture loses money.
- Follow up with the few customers behind most returns, mostly in California and Washington.
- Check the 14 odd-profit rows with whoever owns the data.

## Limitations

- No cost or discount data, so causes can't be confirmed.
- Only two years of data, so the 2019-2020 trend may not continue.
- Small cities show extreme margins because of very small samples.

## Files

```
├── Notebook/sales_analysis.ipynb          # EDA notebook (cleaning, analysis, findings)
├── Dashboard/sales_profit_dashboard.pbix  # Power BI dashboard + screenshots
└── Data/sales_data.csv                    # dataset
```

## Run it yourself

1. Install the libraries: `pip install pandas numpy matplotlib seaborn jupyter`
2. Change the file path in the data-loading cell of the notebook to where `Data/sales_data.csv` is on your computer.
3. Open `Notebook/sales_analysis.ipynb` and run all cells.
