# Financial Planning with APIs and Simulations
We will create two financial analysis tools by using a single Jupyter notebook:

Part 1: A financial planner for emergencies. The members will be able to use this tool to visualize their current savings. The members can then determine if they have enough reserves for an emergency fund.

Part 2: A financial planner for retirement. This tool will forecast the performance of their retirement portfolio in 30 years. To do this, the tool will make an [Alpaca API](https://alpaca.markets/docs/) call via the [Alpaca SDK](https://github.com/alpacahq/alpaca-trade-api-python/) to get historical price data for use in [Monte Carlo simulations](https://www.rdocumentation.org/packages/decisionSupport/versions/1.110/topics/mcSimulation).

We will use the information from the Monte Carlo simulation to analyse and visualize the portfolio.

## Technologies
Financial Planning with APIs and Simulations project leverages python 3.7 with the following packages:

[Pandas](https://github.com/pandas-dev/pandas "Pandas") 

[MCForecastTools](https://cdn.inst-fs-pdx-prod.inscloudgate.net/e0e08ad7-c5b3-43c1-8e7c-e7efc5f1f39c/MCForecastTools.py?token=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCIsImtpZCI6ImNkbiJ9.eyJyZXNvdXJjZSI6Ii9lMGUwOGFkNy1jNWIzLTQzYzEtOGU3Yy1lN2VmYzVmMWYzOWMvTUNGb3JlY2FzdFRvb2xzLnB5IiwidGVuYW50IjoiY2FudmFzIiwidXNlcl9pZCI6IjE1MDQyMDAwMDAwMDAxNjY3OSIsImlhdCI6MTY0NzgwNTcwMiwiZXhwIjoxNjQ3ODkyMTAyfQ.AFw4Zrh-g9L-bjcvOiNwTlG8AXpxX7mml1s1WvuToE2tPxnQ1OWTfyfYG0LnT8vXcSD469j1DdN2BRCQ5ACDUA&content_type=text%2Fx-python)

## Installation Guide

First install the following libraries and dependencies.

```
# conda
conda install pandas
pip install alpaca-trade-api
pip install python-dotenv
```

```
import os
import requests
import json
import pandas as pd
from dotenv import load_dotenv
import alpaca_trade_api as tradeapi
from MCForecastTools import MCSimulation
%matplotlib inline
```

## Usage

### Part 1: Create a Financial Planner for Emergencies
<br>

**Evaluate the Cryptocurrency Wallet by Using the Requests Library**
Determine the current value of a member’s cryptocurrency wallet. Use `requests.get` library to get the current price of Bitcoin (BTC) and Ethereum (ETH) and calculate total value of crypto portfolio.

**Evaluate the Stock and Bond Holdings by Using the Alpaca SDK**
Determine the current value of a member’s stock and bond holdings. Set the parameters `tickers`, `timeframe`, `start_date`, `end_date` and make an API call to Alpaca via the Alpaca SDK to get the current closing prices of the [S&P 500](https://en.wikipedia.org/wiki/S%26P_500 "S&P 500") and of the [AGG](https://www.ishares.com/us/products/239458/ishares-core-total-us-bond-market-etf).
Get the current closing prices for SPY and AGG by using the Alpaca `get_bars` function and calculate the value of the stock and bond portfolio.

**Evaluate the Emergency Fund**

`savings_df`

```
savings_df = pd.DataFrame(saving_data,
     index=["Crytpo","Stock/Bond"],
     columns = ["Amount"]
)
```

![Portfolio Composition](Images/Piechart.png)

### Part 2: Create a Financial Planner for Retirement
<br>

**Create the Monte Carlo Simulation**

```
MC_thirty_year = MCSimulation(
    portfolio_data = prices_df,
    weights = [.40, .60],
    num_simulation = 500,
    num_trading_days = 252 * 30
```

**Analyze the Retirement Portfolio Forecasts**

```
ci_lower_thirty_cumulative_return = MC_thirty_year_summary_statistics[8] * total_stock_bond_balance
ci_upper_thirty_cumulative_return = MC_thirty_year_summary_statistics[9] * total_stock_bond_balance
```
![30-year Monte Carlo simulation](Images/30yearplot.png)

**Forecast Cumulative Returns in 10 Years**

```
MC_ten_year_summary_statistics = MC_ten_year.summarize_cumulative_return()
```
![10-year Monte Carlo simulation](Images/10yearplot.png)

## Contributors

* Brought to you by Olga Koryachek.
* Email: olgakoryachek@live.com
* [LinkedIn](https://www.linkedin.com/in/olga-koryachek-a74b1877/?msgOverlay=true "LinkedIn")


---

## License

Licensed under the [MIT License](https://choosealicense.com/licenses/mit/)


