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

If you are interested, this bellow it the python code to recreate this animation:


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
