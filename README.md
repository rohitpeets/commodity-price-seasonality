# Maize & Wheat Price Seasonality

Does buying grain in a certain month and selling later actually pay? I tested it on 12 years of world prices (2014–2025) and added India's MSP history for context.

I worked grain procurement in Punjab, and in 2025 I bought maize in June–July and sold it to starch, beer and ethanol plants. This checks whether that kind of margin comes from timing or from the trade itself.

## Results

| | Maize | Wheat |
|---|---|---|
| Cheapest month | Aug | Sep |
| Most expensive month | May | May |
| Seasonal swing | 12.4% | 15.0% |
| Best window (after 1%/month carry) | Buy Aug, sell May: +6.2% avg | Buy Sep, sell May: +7.1% avg |
| Best window, median / years profitable | -3.6% / 5 of 12 | +3.6% / 6 of 12 |
| Buy Jun–Jul, sell 1–3 months later | -7.8% avg, 1 of 12 years profitable | -7.5% avg, 2 of 12 |
| Out-of-sample (pick on 2014–19, test 2020–25) | +3.5% | +0.7% |
| MSP growth 2014-15 to 2025-26 | 5.66%/yr | 5.12%/yr |

- Prices usually bottom in late summer and peak in May, but the pattern is loose.
- The best window looks good on average because of a few big years (maize 2020: +94.7%). In a normal year it's small or negative.
- Buying maize in June–July and holding lost money in 11 of 12 years. Margin in that window comes from grading lots and selling to the right processor, not from price moves.
- Paddy MSP grew 5.17%/yr. In dollars, maize MSP sat above the world price in 10 of 12 seasons.

## Method

1. Seasonal index: each month's price ÷ that year's average, averaged across years.
2. Every buy month × holding period of 1–11 months (132 windows per crop). Net return = gross return − carry × months held.
3. Carry cost is an assumption (1%/month). The Sensitivity sheet runs 0–2%.
4. Out-of-sample test to check the edge isn't just fit to the data.

## Data

- World prices: IMF via FRED, [PMAIZMTUSDM](https://fred.stlouisfed.org/series/PMAIZMTUSDM) and [PWHEAMTUSDM](https://fred.stlouisfed.org/series/PWHEAMTUSDM), USD/ton, monthly.
- India MSP: Ministry of Agriculture (DES) MSP table, checked against Lok Sabha answers and PIB releases.
- INR/USD: Federal Reserve, [AEXINUS](https://fred.stlouisfed.org/series/AEXINUS).
- Full list with retrieval dates in `data/sources.csv`.

## Limits

- World benchmark prices, not Punjab mandi prices. I couldn't get a clean official monthly mandi series.
- 12 years is short and a few years drive the averages.
- Carry cost is assumed. Transaction costs and storage losses aren't modeled.

## Files

- `Commodity_Seasonality_Analysis.xlsx` – the model, all live formulas. Change carry cost or year range on `Buy_Sell_Windows` and everything updates.
- `commodity_seasonality.ipynb` – Python version, same numbers.
- `Summary.pdf` – 2-page summary.
- `data/` – raw CSVs and sources.

```bash
pip install pandas numpy matplotlib jupyter
jupyter nbconvert --to notebook --execute --inplace commodity_seasonality.ipynb
```
