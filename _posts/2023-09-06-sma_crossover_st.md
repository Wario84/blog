---

layout: post
title: "Backtesting a Crossover Moving Average Strategy Algorithm in the Forex Market."
author: "Mario H. Gonzalez-Sauri"
date: "2023-09-06"

---


## Introduction

This post aims to explore the effectiveness of a straightforward Forex
market investment algorithm. Amidst numerous algorithmic possibilities,
I chose to embrace simplicity as a stepping stone before delving into
more complex strategies. Inspiration was drawn from Gurrib's 2016 paper,
published on the Global Review of Accounting and Finance, available at
[SSRN](https://ssrn.com/abstract=2578302). Gurrib's study, which
benchmarked a crossover simple moving average strategy on daily S&P500
candles between 1993 and 2014, reported an impressive 24% return over
1593 investment days. Let's embark on this journey to assess the
potential of a similar approach in the Forex market.

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