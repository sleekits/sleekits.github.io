---
layout: category
taxonomy: blog
permalink: /blog
author_profile: false
comments: false
header:
  overlay_color: '#141010'
  overlay_filter: '0.7'
  overlay_image: /assets/images/blog.jpg
  caption: 'By [freepik](https://www.freepik.com/vectors/background)'
excerpt: ''
---

# Introduction

By ECastaneda

Ideas to develop:

1. Algorithmic trading \(algo-trading\) is an automated system for executing market orders, based on pre-programmed trading commands or specifications
2. robotic process automation
3. new traders with few time to migrate their strategies to code
4. Quantitative trading is the single best source of semi-passive wealth accumulation
5. From discretionary investing towards a diversified Quant approach.


## Strategy Layer

* what is a strategy?
* how someone can create, evaluate and profit from one?
* Relevant or popular technical indicators
* how do we know it is a good strategy?
* once the strategy works, what do we do with it?
* type of strategies: momentum, mean-reversion, conservative, single assest vs basket of assets
* scope and limitations: daily, scalping, etc


# Automated Trading Architecture

The Sleekits team is developing a set of tools to automate tasks at each stage of a trading operation. The figure below illustrates how such tools are interconnected as well as their components.
The first stage in our automation framework is given by the **Strategy Layer**, which defines the technical indicators that generate the buy-sell signals. This layer also includes the rules for capital and risk allocation, depending on the traded assest and the expected operation period (hours, days, weeks).
The **Service Layer** is in charge of receiving the signals, executing the orders and managing the multiple accounts with brokers and exchanges. The last component of the architecture is the **Optimization Layer**, which includes automated tasks for generating, storing and analyzing the data produced by the implemented strategy. In this post we will focus on the latter layer, providing an overview of both, its main components and promising results.

<figure class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/strategy-optimization/sleekits-service-architecture.png" alt="">
  <figcaption>Sleekits Automated Trading Architecture</figcaption>
</figure> 


## Optimization Layer

### Data Acquisition

The raw material for Machine Learning is data, which is defined by the  key performance indicators (KPIs) produced by a trading strategy over a given period. Several trading platforms, such as [TradingView](https://www.tradingview.com/gopro/?share_your_love=sleekits), provide a set of [indicators](https://www.tradingview.com/support/solutions/43000561856-how-are-strategy-tester-report-values-calculated-and-what-do-they-mean/) to assess how effective your strategy performs in back testing using net profit, percent profitable, profit factor and the like. All these KPIs help us to quantify the strategy outcome over time for a particular asset. We can combine the inputs' value with the KPIs to produce a predictive ML model, assess the stability of the strategy and optimize the performance. The Sleekits team has developed a Robotic Process Automation (RPA) Solution to perform the data acquisition model shown in the figure below. The RPA solution collects the inputs that define the strategy for a target asset (e.g. BTC, Tesla, etc) and the resulting KPIs from the strategy execution over a testing period. The data acquisiton solution can be configured to run automatically for a predefined number of times or until a stop criterion is reached.

<figure class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/strategy-optimization/sleekits-data-acquisition.png" alt="">
  <figcaption>Data Acquisition Model</figcaption>
</figure> 

The figure shows how a trading strategy can be thought as a collection of interconnected layers of inputs (floats, boolean, etc), which produce a signal to sell, buy or hold the asset. Such signals generate a set of outputs that quantify the performance (KPIs). The inputs and KPIs are stored and manipulated using data science tools to extract strategy insights.


### ML Modeling

The ML modeling applied over the data helps us to understand the relationship between the inputs, the KPIs and the cost function under optimization.
The model is constrained to the granularity of the data and the time frame it represents.
Therefore, our methodology analyzes the quality of the model, the magnitude of the coefficients associated with each input and the overall stability.

An example of ML modeling for a momentum strategy for ETH is illustrted in the figure below, where the weighted profit factor (WPF) is defined as a function of the inputs. The coefficient of determination **R2** measures how well the real values fit the prediction of the model. 
In our example, R2 ~ 88% of the WPF can be explained by a given set of inputs. It is worth noting that the ML model in this example contains more than 50 inputs, but the figure shows only the most important ones sorted by magnitude. 

The information that we require to initialize the optimization algorithms lies in the coefficients and their characteristics. For instance, the linear ML model reveals that an increment of one unit of *input-17* results in an increment about 300 units in the WPF. Similar analysis is done for the rest of the coefficients to determine the stability of the strategy, the implicit constraints each input imposes to the KPIs and the set of inputs or conditions that do not provide an edge to the strategy.

<figure class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/strategy-optimization/sleekits-ml-coefficients.png" alt="">
  <figcaption>Largest Coefficients in the ML Model</figcaption>
</figure> 


### Numerical Optimization

In the  momentum strategy for ETH in the example, our objective is to maximize the WPF subject to a set of constraints defined by the range of operation of each input. The RPA solution not only acquires the data but also provides a set of anchoring points in the inputs universe for which the WPF has a local maximum value. In the heat map below every point represents a tuple: (inputs, KPIs, WPF). In the figure, two KPIs are used to visualize the performance of each tuple, namely the profit factor and the percentage of profitability. Additionally, the figure shows the anchors used in the data acquisition stage which define the fastest optimization path to maximize the WPF.

<figure class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/strategy-optimization/sleekits-search-optimization.png" alt="">
  <figcaption>Sleekits Search Optimization Approach</figcaption>
</figure> 

For some trading strategies the inner layer structures are too complex to converge to the global maximum using tools such as a linear ML Model. An optimization method inspired by the genetic algorithms has been implemented to handle such kind of complex strategies. The fundamental idea is to collect a represtative set of (inputs, KPIs, Cost Function) tuples. From this first generation of tuples the inputs that produce the best cost function values will be combine to create a new set of inputs. Such a new generation of inputs will have some KPIs and cost function values from which a new generation of inputs will be created. Such an iterative process provides insightful data about the strategies.

# Case Study

In this section we present results of our optimization approach with three popular strategies. Each strategy targets a different asset type: crypto, currencies and stocks.

## Crypto Strategy

* [N1](https://www.tradingview.com/script/RJBjyl2W-Ichimoku-Daily-Candle-X-HULL-MA-X-MacD/): based on the popular **Ichimoku-Daily-Candle-X-HULL-MA-X-MacD** strategy originally used for the ticker `ETHBTC/BITSTAMP`.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/strategy-optimization/N1/N1_ETHBTC_BITSTAMP_profit_factor_7.png){: .align-center}

## Forex Strategy

* [N2](https://www.tradingview.com/script/vObmEraY-Open-Close-Cross-Strategy-R5-revised-by-JustUncleL/): based on the popular **Open-Close-Cross-Strategy-R5-revised-by-JustUncleL** originally used for the ticker `USDCAD/FX`.

## Stocks Strategy

* [N3](https://www.tradingview.com/script/8fjvDU2x-Wave-Trend-Strategy-Lazy-Bear/): based on the **Wave-Trend-Strategy-Lazy-Bear** strategy optimized for an old ticker, `Sprint/NYSE`, a company that was acquired by T-Mobile some years ago.



# Sleekits Strategies

* SMTS: sleekits momentum trading strategy 

## BTC Optimization


## ETH Optimization


# Benchmarking

We have developed a strategy ...

| Strategy | Ticker | Net Profit % | Total Closed Trades | Percent Profitable % | Profit Factor | Max Drawdown % | Avg Trade | Avg bars in trades |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| [N1](https://www.tradingview.com/script/RJBjyl2W-Ichimoku-Daily-Candle-X-HULL-MA-X-MacD/) | ETHBTC/BITSTAMP | 7535.46 | 56 | 66.07 | 7.03 | 44.35 | 134.56 | 141 |
| [N1](https://www.tradingview.com/script/RJBjyl2W-Ichimoku-Daily-Candle-X-HULL-MA-X-MacD/) | BTCUSDT/BINANCE | 1092.42 | 12 | 66.67 | 5.311 | 15.89 | 91.03 | 92 |
| [N1](https://www.tradingview.com/script/RJBjyl2W-Ichimoku-Daily-Candle-X-HULL-MA-X-MacD/) | ETHUSTD/BINANCE | 23650.26 | 44 | 59.09 | 9.77 | 47 | 537.51 | 87 |
| [N2](https://www.tradingview.com/script/vObmEraY-Open-Close-Cross-Strategy-R5-revised-by-JustUncleL/) | USDCAD/FX | 1.74 | 67 | 98.51 | 1660.67 | 0 | 0 | 43 |
| [N2](https://www.tradingview.com/script/vObmEraY-Open-Close-Cross-Strategy-R5-revised-by-JustUncleL/) | BTCUSDT/BINANCE | 33.13 | 82 | 98.78 | 1906.64 | 0 | 0.4 | 73 |
| [N2](https://www.tradingview.com/script/vObmEraY-Open-Close-Cross-Strategy-R5-revised-by-JustUncleL/) | ETHUSTD/BINANCE | 22.44 | 61 | 98.36 | 3479.31 | 0 | 0.37 | 62 |
| [N3](https://www.tradingview.com/script/8fjvDU2x-Wave-Trend-Strategy-Lazy-Bear/) | VZ/NYSE | 1.9 | 4035 | 41.14 | 0.982 | 7.71 | 0 | 3 |
| [N3](https://www.tradingview.com/script/8fjvDU2x-Wave-Trend-Strategy-Lazy-Bear/) | BTCUSDT/BINANCE | 6044.48 | 136 | 39.71 | 2.58 | 63.2 | 44.44 | 10 |
| [N3](https://www.tradingview.com/script/8fjvDU2x-Wave-Trend-Strategy-Lazy-Bear/) | ETHUSTD/BINANCE | 217.46 | 148 | 40.54 | 1.94 | 14.3 | 1.47 | 10 |
| SMTS | BTCUSDT/BINANCE | 8253.58 | 144 | 79.86 | 78.35 | 7.31 | 57.32 | 85 |
| SMTS | ETHUSTD/BINANCE | 10021.38 | 82 | 82.93 | 128.35 | 11.68 | 122.21 | 497 |

## Follow up

The Sleekits team is woking to launch an alpha service for testing and optimizing trading strategies.
Currently we are only working with strategies developed in [TradingView](https://www.tradingview.com/gopro/?share_your_love=sleekits), so if you are a trader with curiosity and interest about improving your strategies please drop us a line to admin@sleekits.com.

