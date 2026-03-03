# EKG Empire — Sovereign DRL Trading Engine

<div align="center">

![Status](https://img.shields.io/badge/Status-Live%20Deployed-brightgreen)
![Model](https://img.shields.io/badge/Model-PPO%20DRL-blue)
![Win Rate](https://img.shields.io/badge/Win%20Rate-63.6%25-success)
![Return](https://img.shields.io/badge/Holdout%20Return-%2B6.33%25-success)
![Instruments](https://img.shields.io/badge/Instruments-V75%20%7C%20BTC%20%7C%20Gold-orange)

**A fully autonomous, self-learning algorithmic trading engine built from scratch using Deep Reinforcement Learning.**

*Built by Olaoluwa Emmanuel Bello — Lagos, Nigeria*

</div>

-----

## The Name

**EKG** carries three people in four letters:

|Letter|Person              |Meaning                           |
|------|--------------------|----------------------------------|
|**E** |Emmanuel & Elizabeth|My name and my mother             |
|**K** |Kwabena             |My father — from Ghana            |
|**G** |Gift (Godsgift)     |My wife — a gift from the universe|

Three generations. Two countries. One engine fighting in the financial markets every day.

-----

## What This Is

EKG Empire is a production-grade DRL trading system designed, built, and deployed independently — with no institutional backing, no team, and no pre-built frameworks. Every component from the data pipeline to the live execution bridge was architected from first principles.

The system currently trades Volatility 75 Index (V75) on M15 timeframes with live Telegram signal delivery, and is being extended to BTC/USDT and Gold (XAUUSD).

-----

## Performance — V4.1 Sovereign (Holdout Backtest)

> Tested on 3,499 candles of **completely unseen data** — chronologically separated before training began. No data leakage. No curve fitting.

|Metric          |Result              |
|----------------|--------------------|
|Starting Balance|$10,000.00          |
|Final Balance   |**$10,633.28**      |
|Net Return      |**+6.33%**          |
|Peak Equity     |$10,968.56          |
|Win Rate        |**63.6%**           |
|Avg Trade PnL   |**+1.02% per trade**|
|Best Win Streak |9 consecutive trades|
|Max Drawdown    |8.83%               |
|Total Trades    |22                  |
|Flat (no trade) |37.6% of candles    |

### Equity Curve — Holdout Period

![Equity Curve](equity_curve_v41.jpg)
*Agent stayed profitable from candle 1 to candle 670 on unseen data. Green fill = above baseline. Equity never crossed below $10,000.*

-----

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    EKG EMPIRE ENGINE                     │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  LIVE DATA LAYER                                         │
│  Deriv WebSocket → M15 Candles → Feature Pipeline       │
│  [log_return | ATR-Z | RSI | EMA_dist | momentum |      │
│   vol_rolling | regime_adx]                              │
│                                                          │
│  REGIME DETECTION                                        │
│  ADX Filter → TREND (ADX>25) / CHOP (ADX≤25)           │
│  Agent observes regime — learns its own response        │
│                                                          │
│  PPO BRAIN (11-Dimensional Observation Space)            │
│  7 Market Features + 4 Portfolio Context Features        │
│  Actions: FLAT | BUY 0.5 | BUY 1.0 | SELL 0.5 | SELL 1.0│
│                                                          │
│  RISK MANAGEMENT                                         │
│  2% Hard Stop-Loss | 25% Kill Switch | Sharpe Reward    │
│                                                          │
│  EXECUTION BRIDGE                                        │
│  Shadow Bot → Telegram Alerts → Live Deployment          │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

-----

## Technical Stack

|Component          |Technology                                      |
|-------------------|------------------------------------------------|
|RL Framework       |Stable-Baselines3 (PPO)                         |
|Training           |5M steps, 8 parallel SubprocVecEnv              |
|Neural Network     |MLP [256, 256] policy + value heads             |
|Data Source        |Deriv WebSocket API (V75) / Binance API (BTC)   |
|Feature Engineering|Pure NumPy/Pandas — zero TA library dependencies|
|Regime Detection   |Custom ADX implementation (pure NumPy)          |
|Live Execution     |Python WebSocket bridge + CSV pipeline          |
|Alerts             |Telegram Bot API                                |
|Environment        |Custom Gymnasium with Sharpe-normalized rewards |

-----

## What Makes This Different

**1. Learns, doesn’t follow rules.**
The agent discovered through 5 million market interactions that ranging markets are unrewarding. Nobody programmed that — it emerged from training. The 37.6% flat rate is learned behavior, not a hard-coded filter.

**2. Proper validation methodology.**
Chronological 80/10/10 train/validation/holdout split. The holdout set was locked before training began. This is how professional quant funds validate strategies.

**3. Full stack ownership.**
Every component — data ingestion, feature engineering, environment design, reward shaping, training infrastructure, live execution — built and understood at the code level.

**4. Instrument-agnostic engine.**
Same architecture trains on V75 today, BTC tomorrow, Gold next. This is a trading engine, not a single strategy.

**5. Regime-aware intelligence.**
The ADX regime filter gives the agent market context every candle. It adapts through learned response, not rule-based logic.

-----

## Training Evolution

|Version|Steps|Holdout Return|Key Improvement                   |
|-------|-----|--------------|----------------------------------|
|V1.0   |1M   |—             |Initial architecture              |
|V3.0   |5M   |+1.09%        |Stop-loss penalty, entry price fix|
|V4.1   |3M   |**+6.33%**    |ADX regime observation feature    |

-----

## Live Deployment Status

```
System     : LIVE (Shadow Mode)
Started    : March 2026
Instrument : V75 M15 (Deriv)
Signals    : Telegram (real-time)
Next       : BTC/USDT M15 (Binance) — in training
Pipeline   : Gold (XAUUSD) — scheduled
```

-----

## Roadmap

- [x] V75 live shadow deployment
- [x] ADX regime detection
- [x] 63.6% win rate validated on holdout
- [ ] BTC/USDT model training and shadow deployment
- [ ] Gold (XAUUSD) pipeline
- [ ] Multi-instrument portfolio risk allocator
- [ ] Demo account live execution
- [ ] Prop firm challenge submission

-----

## About

Built independently by a self-taught AI/ML engineer and algorithmic trader.
No institutional backing. No team. No pre-built strategy templates.
Just deep study, grit, and refusal to stop debugging at midnight.

Nigeria → Canada 🇨🇦

**Connect:** [LinkedIn](https://linkedin.com/in/olaoluwa-emmanuel-bello) | [GitHub](https://github.com/KwabenaBellz)

-----

*“The machine carries the family name. It fights every day so we don’t have to.”*
