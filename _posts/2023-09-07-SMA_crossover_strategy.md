---
layout: post
title: "Backtesting a Crossover Moving Average Strategy Algorithm in the Forex Market."
author: "Mario H. Gonzalez-Sauri"
date: "2023-09-07"
keywords: finance, trading, forex
---



## Introduction

This post aims to explore the effectiveness of a straightforward Forex
market investment algorithm. Amidst numerous algorithmic possibilities,
I chose to embrace simplicity as a stepping stone before delving into
more complex strategies. Inspiration was drawn from Gurrib’s 2016 paper,
published on ‘Global Review of Accounting and Finance,’ available at
SSRN (<https://ssrn.com/abstract=2578302>). Gurrib’s study, which
benchmarked a crossover simple moving average strategy on daily S&P500
candles between 1993 and 2014, reported an impressive 24% return over
1593 investment days. Let’s embark on this journey to assess the
potential of a similar approach in the Forex market.

## Simple Moving Average(SMA) Basics

The simple moving average (SMA) is a method of forecasting that predicts
the next value in the series based on the mean of a set $q$ previous
values (lags). Obviously, the model will perform well if the series has
a tendency to revert to a mean value (stationary) well represented by
the number of selected previous or lag values in the model. In other
words, once we accounted for the correct number of lag values, the
errors $\epsilon$ in the model should be independent and identically
distributed (random).

$Y_t = \bar{Y}(Y_{t-1} + ... Y_{t-q}) + \epsilon$

## SMA Crossover Strategy

The SMA crossover strategy works by assuming that the series contains
short and long-run trends. The short-run trend follows the series
closely and reacts more rapidly to variations in the series in
comparison to the long-run trend. The core idea of the strategy is that
we can find market signals of buying or selling by monitoring the
intersections between the short and long-run trends in the series. If
the short-run trend intersects the long-run trend and moves upward the
value of the series is increasing (also called a golden cross), and
therefore the algorithm sends a buy signal. Conversely, if the short-run
trend intersects the long-run trend and moves downward the price
decreases (known as a dead cross), and it is time to sell.

To understand better the behavior of the algorithm I have created a
visualization that monitors the interaction between the USD.SEK series
that I downloaded from Interactive Brokers in candles of 30 seconds
(blue) and the short and long-run trends (red and green respectively)
that I have estimated using SMA.

![](https://github.com/Wario84/blog/raw/main/assets/imgs/USD.SEK_SMA_3.gif?raw=true)<!-- -->

``` python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import os
from matplotlib.animation import FuncAnimation
from IPython.display import display, clear_output

# change working directory

# Specify the target directory
new_directory = r'C:\Users\mglez\Documents\PHD\Semester 16\01092023_SMA_blog\material\dynamc_graph'

# Change the working directory
os.chdir(new_directory)

# Read the CSV file and extract the first column of the USD.SEK as y1
df = pd.read_csv('USDSEK_dur_5D_candle_30sec_2023-08-20_2023-08-24_CLOSE.csv')
y1 = df.iloc[301:, 1].values
# Loading the simple moving averages
y2 = df.iloc[301:, 2].values
y3 = df.iloc[301:, 3].values

# Create x data
n = len(y1)
x = np.arange(n)

# Initialize the plot
fig, ax = plt.subplots()
line1, = ax.plot(x, y1, label='USD.SEK', color='blue')
line2, = ax.plot(x, y2, label='SMA 5', color='red')
line3, = ax.plot(x, y3, label='SMA 300', color='green')
ax.set_title('SMA Crossover Strategy: USD.SEK')
ax.legend()

# Set the y-axis limits to display values between 10.5 and 11.5
ax.set_ylim(10.9, 11)

# Initialize text annotation
text = ax.text(0.1, 0.90, '', transform=ax.transAxes, fontsize=12, color='black')

# Number of values to display on the horizontal axis
num_values_to_display = 100

# Function to update the plot for each frame
def update(frame):
    x_data = x[max(0, frame - num_values_to_display):frame]
    line1.set_data(x_data, y1[max(0, frame - num_values_to_display):frame])
    line2.set_data(x_data, y2[max(0, frame - num_values_to_display):frame])
    line3.set_data(x_data, y3[max(0, frame - num_values_to_display):frame])
    
    # Calculate the x-axis limits dynamically based on the frame and num_values_to_display
    min_x = max(0, frame - num_values_to_display)
    max_x = frame
    ax.set_xlim(min_x, max_x)

    # Check if there are enough data points to calculate min and max
    if len(x_data) >= num_values_to_display:
        min_y = min(min(y1[max(0, frame - num_values_to_display):frame]), min(y2[max(0, frame - num_values_to_display):frame]), min(y3[max(0, frame - num_values_to_display):frame]))
        max_y = max(max(y1[max(0, frame - num_values_to_display):frame]), max(y2[max(0, frame - num_values_to_display):frame]), max(y3[max(0, frame - num_values_to_display):frame]))
        ax.set_ylim(min_y - 0.009, max_y + 0.009)
    
    if y2[frame] > y3[frame]:
        text.set_text('Buy')
        text.set_color('red')
    else:
        text.set_text('Sell')
        text.set_color('green')
    return line1, line2, line3, text

# Create the animation
ani = FuncAnimation(fig, update, frames=n, interval=300)  # Update every 3 seconds

# Display the animation in Jupyter Notebook
display(fig)

try:
    # Continuously update the animation
    for i in range(n):
        update(i)
        clear_output(wait=True)
        display(fig)
except KeyboardInterrupt:
    pass
```

## Requesting Data from Interactive Brokers

To request data from Interactive Brokers, you need a trading account and
to connect the API of the Trader Workstation to Python or R. If you are
using R, you need to install the `IBrokers` package before you attempt
to download the data. To teach how to download data from the API, can be
a tutorial in itself. But the key elements that you need are a
connection to the API, a contract with a correct symbol for the stock, a
duration and a candle size. In this example, I am creating a connection
that I call `tws`, then I am creating a contract with the
`twsContract()` with the correct symbol `USD.SEK` and finally I am
setting a duration of “5 D” (5 days) with candles of “30 sec”.

``` r
library('IBrokers')


#### ACCOUNT ####
tws = twsConnect(port=7496)
twsConnectionTime(tws)
ac <- reqAccountUpdates(tws)

#### CONTRACT ####
contract <- twsContract()
contract$symbol <- "USD"
contract$sectype <- "CASH"
contract$currency <- "SEK"
contract$exch <- "IDEALPRO"
contract$includeExpired = TRUE
is.twsContract(contract)


#### REQUEST HIST DATA ####

duration <- "5 D"
barSizeSetting <- "30 sec"

data <- reqHistoricalData(conn=tws, Contract=contract, duration=duration, barSize=barSizeSetting, whatToShow="MIDPOINT")
```

The setting that I am using on my Trader Workstation are the following:

![](https://github.com/Wario84/blog/raw/main/assets/imgs/00_set_up_API.gif?raw=true)<!-- -->

## Optimizing the SMA Crossover bands

A key requirement for the success of the algorithm is to identify which
set of bands (long and short-run) are better to predict changes in the
behavior of the series. We are interesting on benchmarking a series of
pair of bands so we can identify which combination is more profitable.
In other words, we are going to set the criteria of the highest balance
at the end of the testing period to select the pair of bands.

Probably there is fastest vectorized way to identify the intersections,
but to calculate the final profit I think it is only possible to do with
a loop. Because, the margins of profit/loss change in every transaction
and the accumulation of capital depends on this interactive process.

The range I selected for the SMA in the short run is from `5:100` and
`10:300`for the long run. In each iteration the algorithm will select
one pair of bands, fit the corresponding models, calculate benchmarks
and estimate the capital at the end of the period.

Similar to the study by Gurrib (2016), I assume that:

1.  The frequency of data is set initially to candles of 30 seconds.
2.  The effect of discounts, taxes and commissions are ignored.
3.  All orders occur immediately at market prices.  
4.  Limit and stop order options are not allowed at this stage.

``` r
perf_df <- data.frame(matrix(ncol = 13, nrow = 0))
colnames(perf_df) <-
  c(
    "n",
    "m",
    "capital",
    "num_trades",
    "trades_per_min",
    "numWinningTrades",
    "numLosingTrades",
    "mae_short",
    "mae_long",
    "rmse_short",
    "rmse_long",
    "corr_short",
    "corr_long"
  )

# Set commission rate
# commission_rate <- 0.00075
commission_rate <- 0

# Loop over n and m
for (n in 5:100) {
  for (m in 10:300) {
    # Calculate moving averages
    data$sma_short <- SMA(data$USD.SEK.Close, n = n)
    data$sma_long <- SMA(data$USD.SEK.Close, n = m)
    # data$sma_short[is.na(data$sma_short)] <- 0
    # data$sma_long[is.na(data$sma_long)] <- 0
    
    # Mean Absolute Error (MAE)
    mae_short <- mean(abs(data$sma_short - data$USD.SEK.Close),na.rm = TRUE)
    mae_long <- mean(abs(data$sma_long - data$USD.SEK.Close), na.rm = TRUE)
    
    # Root Mean Squared Error (RMSE)
    rmse_short <-
      sqrt(mean(sum(data$sma_short - data$USD.SEK.Close, na.rm = T) ^ 2))
    rmse_long <- sqrt(mean(sum(data$sma_long - data$USD.SEK.Close, na.rm = TRUE) ^ 2))
    
    # Correlation Coefficient
    corr_short <- cor(data$sma_short, data$USD.SEK.Close, use = "complete.obs")
    corr_long <- cor(data$sma_long, data$USD.SEK.Close, use = "complete.obs")
    
    
    # Initialize variables
    init_capital = 2000
    capital = 2000
    pos = 0
    numTrades = 0
    numWinningTrades = 0
    numLosingTrades = 0
    
    
    
    
    # Backtest strategy
    for (i in 2:nrow(data)){      # Check for a cross
      # c <- c + 1L
      # #print cross
      # print(paste0("cross: ", c))
      if (!is.na(data$sma_short[i - 1]) &&
          !is.na(data$sma_long[i - 1]) &&
          data$sma_short[i - 1] <= data$sma_long[i - 1] &&
          data$sma_short[i] > data$sma_long[i] && capital > 0) {
        # Buy
        pos = (capital - capital * commission_rate) * as.numeric(data$USD.SEK.Close[i])
        print(paste("BUY:", i, pos))
        capital = 0
        numTrades = numTrades + 1
      }
      else if (!is.na(data$sma_short[i - 1]) &&
               !is.na(data$sma_long[i - 1]) &&
               data$sma_short[i - 1] >= data$sma_long[i - 1] &&
               data$sma_short[i] < data$sma_long[i] && pos > 0) {
        # Sell
        capital = as.numeric(pos / data$USD.SEK.Close[i] - pos / data$USD.SEK.Close[i] * commission_rate)
        print(paste("SELL:", i, capital))
        pos = 0
        numTrades = numTrades + 1
        
        if (capital > init_capital) {
          numWinningTrades = numWinningTrades + 1
          
        } else {
          numLosingTrades = numLosingTrades + 1
          
        }
      }
      
    }
  }
  # c <- 0L
  # Append performance to dataframe
  perf_df <-
    rbind(
      perf_df,
      data.frame(
        n,
        m,
        capital,
        numTrades,
        trades_per_min = numTrades / ( (nrow(data) * 30)/60 ),
        numWinningTrades,
        numLosingTrades,
        mae_short,
        mae_long,
        rmse_short,
        rmse_long,
        corr_short = corr_short,
        corr_long = corr_short
      )
    )
  print(tail(perf_df))
}

  
colnames(perf_df) <-
  c(
    "n",
    "m",
    "capital",
    "numTrades",
    "trades_per_min",
    "numWinningTrades",
    "numLosingTrades",
    "mae_short",
    "mae_long",
    "rmse_short",
    "rmse_long",
    "corr_short",
    "corr_long"
  )




#### TOP PERFORMANCE ####
# Print final max capital
print(perf_df[which.max(perf_df$capital),])

# Print final max numWinningTrades  
print(perf_df[which.max(perf_df$numWinningTrades ),])



#### BEST FIT ####

# Print final max rmse_short   
print(perf_df[which.max(perf_df$rmse_short),1])

# Print final max mae_short   
print(perf_df[which.max(perf_df$mae_short),1])

# Print final max mae_short   
print(perf_df[which.max(perf_df$corr_short),1])

# Print final max rmse_long   
print(perf_df[which.max(perf_df$rmse_long),2])

# Print final max mae_long   
print(perf_df[which.max(perf_df$mae_long),2])

# Print final max mae_long   
print(perf_df[which.max(perf_df$corr_long),2])
```

In terms of performance (capital return) the pair that won is the
`8, 300` followed closely by the `5, 300` for the short and long-run
respectively.

## Long Run Analysis

The optimization of the bands was conducted in a data set that runs over
5 days in candles of 30 seconds, a data set of `94624`. However, to have
a better idea of the behavior of the algorithm, I decided to run the
algorithm using 6 months of data in candles 30 seconds with a total of
`2961360` data points. Testing the algorithm over six months will give
us a better perspective of how well the SMA bands capture the long and
short run trends in the data and a better approximation of the financial
return.

### Improvements

I decided to make some small changes to the previous algorithm. Firstly,
I wanted to compute the `grossprofit/loss` of each transaction.
Secondly, I estimate the return of investment (ROI) of each transaction
to compute the average and standard deviation of the returns at the end
of the exercise and approximate a Sharpe Ratio. Thirdly, I wanted to
correct a misleading `numWinningTrades/numLosingTrades` indicator in the
previous algorithm. In the previous algorithm, I consider a wining trade
if the current capital was higher than the initial capital after each
transaction. However to be more accurate it is better to consider a
winning trade when the `buyPrice > sellPrice`. This is a bit counter
intuitive but remember that the algorithm buys when the price is
increasing, so the USD (dollar) invested will render more Krones (SEK).
For instance, imagine that you invest 10 USD, and the price of the Krone
is 12 (buying price), that is 120 SEK. Then, if the algorithm identifies
a selling signal at a price of 10.5 SEK (selling price), your profit
would have been 1.43 USD for this transaction, calculated as (120 / 10.5
= 11.43).

### First run of the algorithm

In the first run of the algorithm I wanted to secure winning
transactions only. I attempt to achieve this by adding a rule
`buyPrice > as.numeric(data$USD.SEK.Close[i])`, so I will guarantee that
the selling price was always bellow the buying price and make winning
trades all the time. The buying rule was transformed as follows:

``` r
 else if (!is.na(data$sma_short[i - 1]) &&
           !is.na(data$sma_long[i - 1]) &&
           data$sma_short[i - 1] >= data$sma_long[i - 1] &&
           data$sma_short[i] < data$sma_long[i] && pos > 0 && buyPrice > as.numeric(data$USD.SEK.Close[i])) 
```

Unfortunately this change didn’t report a greater performance than the
regular unconstrained moving average. The issue is that the series
eventually reach local maximum or minimum values. For instance, if the
algorithm buys at a local minimum point in the series this condition
will never be fulfilled `buyPrice > as.numeric(data$USD.SEK.Close[i])`.
Because the algorithm bought at a local minimum there is no change the
future values will be smaller and hence this resulted in lower
performance. In a nutshell, it seems that in order to take advance of
the volatility of the series and make higher profit it is necessary to
lose some trades as long that on the averages we are winning more often.
This is the reported performance of the first run:

|           |   n |   m |  capital | net_profit | grossProfit | grossLoss | buynumTrades | sellnumTrades | trades_per_min | numWinningTrades | numLosingTrades | mae_short | mae_long | rmse_short | rmse_long | USD.SEK.Close | USD.SEK.Close.1 |
|:----------|----:|----:|---------:|-----------:|------------:|----------:|-------------:|--------------:|---------------:|-----------------:|----------------:|----------:|---------:|-----------:|----------:|--------------:|----------------:|
| sma_short |   8 | 300 | 2086.763 |     86.763 |      86.763 |         0 |           56 |            55 |          0.001 |               55 |               0 |     0.001 |     0.01 |      1.987 |    84.648 |             1 |               1 |

The total profit over the six months was only 86.763 USD, a return of
investment of only 4.33 %.

### Second run of the algorithm

In my second attempt I ran the unconstrained version (original version)
with the additional elements that I discussed previously, as follows:

``` r
n <- 8
m <- 300

# Calculate moving averages
data$sma_short <- SMA(data$USD.SEK.Close, n = n)
data$sma_long <- SMA(data$USD.SEK.Close, n = m)
# data$sma_short[is.na(data$sma_short)] <- 0
# data$sma_long[is.na(data$sma_long)] <- 0

# Mean Absolute Error (MAE)
mae_short <- mean(abs(data$sma_short - data$USD.SEK.Close),na.rm = TRUE)
mae_long <- mean(abs(data$sma_long - data$USD.SEK.Close), na.rm = TRUE)

# Root Mean Squared Error (RMSE)
rmse_short <-
  sqrt(mean(sum(data$sma_short - data$USD.SEK.Close, na.rm = T) ^ 2))
rmse_long <- sqrt(mean(sum(data$sma_long - data$USD.SEK.Close, na.rm = TRUE) ^ 2))

# Correlation Coefficient
corr_short <- cor(data$sma_short, data$USD.SEK.Close, use = "complete.obs")
corr_long <- cor(data$sma_long, data$USD.SEK.Close, use = "complete.obs")



# Initialize variables
init_capital = 2000
capital = 2000
buyCapital <- 0
pos = 0
grossPnL = 0
buynumTrades = 0
sellnumTrades = 0
numWinningTrades = 0
numLosingTrades = 0
grossProfit = 0
grossLoss = 0
commission_rate = 0
buyPrice = 0  # Initialize previousPrice to 0
sellPrice = 0
roi = vector("numeric", length = 0)

# Backtest strategy
for (i in 2:nrow(data)){      # Check for a cross
  # ...
  if (!is.na(data$sma_short[i - 1]) &&
      !is.na(data$sma_long[i - 1]) &&
      data$sma_short[i - 1] <= data$sma_long[i - 1] &&
      data$sma_short[i] > data$sma_long[i] && capital > 0) {
    # Buy
    buyPrice <- as.numeric(data$USD.SEK.Close[i])  # Store the buy price
    buyCapital <- capital
    pos = (capital - capital * commission_rate) * buyPrice
    print(paste("BUY:", i, pos))
    capital = 0
    buynumTrades = buynumTrades + 1
  }
  else if (!is.na(data$sma_short[i - 1]) &&
           !is.na(data$sma_long[i - 1]) &&
           data$sma_short[i - 1] >= data$sma_long[i - 1] &&
           data$sma_short[i] < data$sma_long[i] && pos > 0){ #&& buyPrice > as.numeric(data$USD.SEK.Close[i])
    # Sell
    sellPrice <- as.numeric(data$USD.SEK.Close[i])  # Calculate PnL based on current capital
    capital = as.numeric(pos / sellPrice - pos / sellPrice * commission_rate)
    grossPnL <- capital - buyCapital
    print(paste("SELL:", i, capital))
    pos = 0
    sellnumTrades = sellnumTrades + 1
    
    roi <- c(roi, (buyPrice-sellPrice/buyPrice)*100)
    if (buyPrice > sellPrice) {
      numWinningTrades = numWinningTrades + 1
      grossProfit = grossProfit + grossPnL
    } else {
      numLosingTrades = numLosingTrades + 1
      grossLoss = grossLoss + abs(grossPnL)
    }
  }
}
```

The reported performance over the same period of data (6 months) was the
following:

|           |   n |   m |  capital | net_profit | grossProfit | grossLoss | buynumTrades | sellnumTrades | trades_per_min | numWinningTrades | numLosingTrades | mae_short | mae_long | rmse_short | rmse_long | USD.SEK.Close | USD.SEK.Close.1 |
|:----------|----:|----:|---------:|-----------:|------------:|----------:|-------------:|--------------:|---------------:|-----------------:|----------------:|----------:|---------:|-----------:|----------:|--------------:|----------------:|
| sma_short |   8 | 300 | 2317.278 |    317.278 |    1700.261 |  1382.983 |         2025 |          2025 |          0.001 |             1612 |             413 |     0.001 |     0.01 |      1.987 |    84.648 |             1 |               1 |

The net profit of the unconstrained simple moving average over six
months was 317.278 with an initial investment of 2000 USD. A total of
15.86 % return of investment in half a year, not bad at all. The
distribution of the Return of Investment (ROI) of each trade is the
following:

|   Min. | 1st Qu. | Median |  Mean | 3rd Qu. | Max. |   sd |
|-------:|--------:|-------:|------:|--------:|-----:|-----:|
| -2.688 |   0.006 |  0.025 | 0.007 |   0.053 | 1.31 | 0.15 |

ROI Summary Statistics

![](01092023_SMA_crossover_strategy_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

## Final remarks and areas of improvement.

The first observation is that the algorithm reported a high level of
gross loss (1382 USD) in comparison to the gross gain (1780). I believe
this can be improved by adding additional rules to the algorithm to
allow for some resistance bands that may reduce the loss when the
algorithm is not able to detect correctly market opportunities. The
second observation is that I need to incorporate more realistic
estimations of the commissions for each transaction that will reduce the
performance of the algorithm. Thirdly, I think would be useful to
optimize and test the performance the algorithm in the equity market
specially on stocks with higher returns and upward trends. Finally, the
next stage would be to implement the algorithm using live market data
with the function `reqMktData` and to test it with the paper trading
account and assess the live performance.
