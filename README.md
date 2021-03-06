# Designing Breakout Strategy

The project implements a breakout strategy after finding and removing any outliers. Potential profite is examined using a Histogram and P-Value.

## Data Set
End of day from Quotemedia

New stocks are created to simulate many possible senarios. Example is a scenario where companies mining [Terbium](https://en.wikipedia.org/wiki/Terbium) are making huge profits. All the companies in this sector of the market are made up. They represent a sector with large growth that will be used for demonstration latter in this project.

The following is a snapshot for a sample closing price for one tick
![image](images/close_price_sample.png)


## The Alpha Research Process



The signal-to-noise ratio in trading signals is very low and, as such, one can very easily fall into the trap of _overfitting_ to noise. To help mitigate overfitting, the following questions provide some insight for formulating general hypothesis:

> What feature of markets or investor behaviour would lead to a persistent anomaly that my signal will try to use?

![image](images/alpha_steps.png)

Assuming that the first three steps area already done ("observe & research", "form hypothesis", "validate hypothesis"), the following can be tested:

- In the absence of news or significant investor trading interest, stocks oscillate in a range.
- Traders seek to capitalize on this range-bound behaviour periodically by selling/shorting at the top of the range and buying/covering at the bottom of the range. This behaviour reinforces the existence of the range.
- When stocks break out of the range, due to, e.g., a significant news release or from market pressure from a large investor:
    - the liquidity traders who have been providing liquidity at the bounds of the range seek to cover their positions to mitigate losses, thus magnifying the move out of the range, _and_
    - the move out of the range attracts other investor interest; these investors, due to the behavioural bias of _herding_ (e.g., [Herd Behavior](https://www.investopedia.com/university/behavioral_finance/behavioral8.asp)) build positions which favor continuation of the trend.

## Breakout Strategy

The price highs and lows are used as an indicator for the breakout strategy. 

sample result for the highs and lows for the past 50 days in compararison to its respective stock.
![image](/images/high_low.png)  

sample long-short signals

![ls_10](/images/long_short_10.png)

![ls_10](/images/long_short_20.png)


Lookahead Close Prices

![look_ahead](/images/look_ahead.png)

Lookahead Price Returns (the log price return between the closing price and the lookahead price)
![retrurn](/images/return.png)

Using the price returns generate the signal returns
![signal_return](/images/signal_return.png)

**Test for Significance**

To better visualize the outliers, we compare the 5, 10, and 20 day signals returns to normal distributions with the same mean and deviation for each signal return distributions.

![histo](images/histo.png)

`Kolmogorov-Smirnov Test`
is used to quantify the outliers in the histogram; i.e. finds the stocks that are causing these outlying returns. 
The test (KS test) is performed between a distribution of stock returns (the input dataframe in this case) and each stock's signal returns.

compare the 5, 10, and 20 day signals returns without outliers to normal distributions.
![out](/images/out.png)


> The returns are closer to a normal distribution



## Install Requirements
`!{sys.executable} -m pip install -r requirements.txt`


The other packages that we're importing are `helper`, `project_helper`, and `project_tests`. These are custom packages built to help you solve the problems.  The `helper` and `project_helper` module contains utility functions and graph functions. The `project_tests` contains the unit tests for all the problems.


## Reference
[Artificial Intelligence for Trading on Udacity](https://www.udacity.com/course/ai-for-trading--nd880)