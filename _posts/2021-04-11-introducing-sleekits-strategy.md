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

# Sleekits Algorithmic Trading

Ideas to develop:

1. Algorithmic trading \(algo-trading\) is an automated system for executing market orders, based on pre-programmed trading commands or specifications
2. robotic process automation
3. new traders with few time to migrate their strategies to code
4. Quantitative trading is the single best source of semi-passive wealth accumulation
5. From discretionary investing towards a diversified Quant approach.


<figure class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/strategy-optimization/sleekits-service-architecture.png" alt="">
  <figcaption>Sleekits Service Architecture</figcaption>
</figure> 


## Strategy Layer

What’s my downside? What’s my upside? What’s the probability I get said downside vs. said upside?
Momentum vs Mean-Reversion
Technical analysis

* Chart Patterns \(head and shoulders, ascending triangle, etc\)
* Support/Resistance zones
* Technical Indicators \(SMA, MACD, RSI etc\)

## Service Layer

@overider


## Optimization Layer


Machine learning, genetic algorithms and numerical optimization.


# Case Study

## Crypto Strategy

* [N1](https://www.tradingview.com/script/RJBjyl2W-Ichimoku-Daily-Candle-X-HULL-MA-X-MacD/): based on the popular **Ichimoku-Daily-Candle-X-HULL-MA-X-MacD** strategy originally used for the ticker `ETHBTC/BITSTAMP`.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/strategy-optimization/N1/N1_ETHBTC_BITSTAMP_profit_factor_7.png){: .align-center}

## Forex Strategy

* [N2](https://www.tradingview.com/script/vObmEraY-Open-Close-Cross-Strategy-R5-revised-by-JustUncleL/): based on the popular **Open-Close-Cross-Strategy-R5-revised-by-JustUncleL**originally used for the ticker `USDCAD/FX`.

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

We recently rolled out a bunch of new features and UI changes, and we value speaking with as many new customers as possible to make sure we are on the right track.

