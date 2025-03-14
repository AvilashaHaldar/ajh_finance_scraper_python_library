Hello! This is a Python library for scraping various forms of public finance data in the USA. The code is shown in this [GitHub repository](https://github.com/AvilashaHaldar/ajh_finance_scraper_python_library). Currently, this library can:

1. Scrape forward 1 and 3 month SOFR curves

This can be done by doing:

```
from financedatascraperonline import InterestRatesScrapedData
forward_SOFR_curves_df, allowed_SOFR_lengths_months = InterestRatesScrapedData.InterestRatesScrapedData().get_scraped_SOFR_curves()
```

forward_SOFR_curves_df is a Pandas DataFrame containing the 1-month and 3-month forward SOFR rates for the next 10 years. allowed_SOFR_lengths_months is a NumPy array containg the allowed month lengths for the SOFR curves (currently only 1 and 3). We scrape the data from [Pensford](https://www.pensford.com/resources/forward-curve).

2. Getting daily closing stock prices for the past 3 years

```
from financedatascraperonline import HistoricalDailyStockPricesAPI
closing_prices_df = HistoricalDailyStockPricesAPI.HistoricalDailyStockPricesAPI().get_historical_prices_df(ticker_symbol)
```

closing_prices_df is a Pandas DataFrame of daily closing prices over the past 3 years containing the columns [Close, Log_Close, Daily_Returns, Annualized_Hist_Volatility, Annualized_Mean_Daily_Return]. Volatility and mean are rolling values calculated over a 252-day period. (We assume 252 business days in a year.)

3. Compute a few key statistics from the past day

```
from financedatascraperonline import HistoricalDailyStockPricesAPI
mu, sigma, latest_price = HistoricalDailyStockPricesAPI.HistoricalDailyStockPricesAPI().get_main_stats_from_hist_prices(ticker_symbol)
```

mu is the annualized mean daily log return of the last business day calculated for the last 252 days, sigma is the annualized standard deviation of daily log returns over the last 252 days, and latest_price is the last closing price.

4. Scrape US treasury bill rates

```
from financedatascraperonline import InterestRatesScrapedData
treasury_bill_rates_df = InterestRatesScrapedData.InterestRatesScrapedData().get_scraped_treasury_bill_rates()
```

Here, we scrape US treasury bill rates from the (US Treasury website)[https://home.treasury.gov/resource-center/data-chart-center/interest-rates/TextView?type=daily_treasury_bill_rates&field_tdr_date_value=2025] and return the rates in a Pandas DataFrame.