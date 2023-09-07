---

layout: post
title: "Backtesting a Crossover Moving Average Strategy Algorithm in the Forex Market."
author: "Mario H. Gonzalez-Sauri"
date: "2023-09-08"
keywords: finance, trading, forex

---



## Introduction

This post aims to explore the effectiveness of a straightforward Forex
market investment algorithm. Amidst numerous algorithmic possibilities,
I chose to embrace simplicity as a stepping stone before delving into
more complex strategies. Inspiration was drawn from Gurrib's 2016 paper,
published on the Global Review of Accounting and Finance, available at
SSRN (<https://ssrn.com/abstract=2578302>). Gurrib's study, which
benchmarked a crossover simple moving average strategy on daily S&P500
candles between 1993 and 2014, reported an impressive 24% return over
1593 investment days. Let's embark on this journey to assess the
potential of a similar approach in the Forex market.

## Simple Moving Average(SMA) Basics

The simple moving average (SMA) is a method of forecasting that predicts
the next value in the series based on the mean of a set $$q$$ previous
values (lags). Obviously, the model will perform well if the series has
a tendency to revert to a mean value (stationary) well represented by
the number of selected previous or lag values in the model. In other
words, once we accounted for the correct number of lag values, the
errors $$\epsilon$$ in the model should be independent and identically
distributed (random).

$$Y_t = \bar{Y}(Y_{t-1} + ... Y_{t-q}) + \epsilon$$
