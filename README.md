# Quant Trading Accelerator

A hands-on implementation of the *Quant Trading Accelerator* course by MemLabs — a 9 part series that builds a complete quantitative trading system from scratch, starting from raw Python fundamentals and ending in a live, automated trading bot connected to a real exchange.

Rather than using existing libraries as black boxes, this repository follows the course's philosophy of building each layer by hand first (arrays, vectors, a data analysis library, statistical models) before using tools like NumPy, pandas, and PyTorch, in order to develop a first-principles understanding of how quantitative trading systems actually work under the hood.

---

## Table of Contents

- [Motivation](#motivation)
- [Course Structure](#course-structure)
- [What This Repository Contains](#what-this-repository-contains)
- [Key Concepts Covered](#key-concepts-covered)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)
- [Progress Log](#progress-log)
- [Key Takeaways](#key-takeaways)
- [Limitations](#limitations)
- [Future Work](#future-work)
- [License](#license)

---

## Motivation

Quantitative trading is often taught as either pure theory (academic econometrics) or pure black-box tooling (import a library, call `.fit()`). This course instead teaches by building: every concept, from a simple variable to a live trading bot, is implemented from first principles before the equivalent library function is introduced.

The core principle demonstrated throughout is that **a small, honest statistical edge, executed well, can be extremely profitable** — and conversely, that a strong model executed poorly can lose money. This repository exists to internalize that lesson through direct implementation rather than passive viewing.

---

## Course Structure

The course is organized into 9 parts, each building directly on the last. Skipping ahead is not recommended, since later parts assume fluency with everything before them.

| Part | Topic | Core Outcome |
|------|-------|---------------|
| 1 | Variables and Data Types | Numbers, strings, type conversion, string parsing |
| 2 | Arrays | Indexing, mutation, NumPy vs. native lists, log returns |
| 3 | Vectorization | A hand-built data analysis library (vectors, columns, data frames) |
| 4 | Time Series | Central tendency, dispersion, correlation, stationarity, the AR(1) model, mean reversion vs. momentum |
| 5 | Matrices and Statistical Edge | Matrix algebra, the first trained regression model, Sharpe ratio, equity curves |
| 6 | Classification | Binary classifiers, directional accuracy vs. profitability, the Girko statistic, decomposed returns |
| 7 | Cross-Validation | Expanding window, rolling window, and time-series split validation |
| 8 | Strategy | Entry/exit signals, trade sizing, compounding, leverage |
| 9 | Live Deployment | A full async trading bot streaming live data and placing real orders on an exchange testnet |

---

## What This Repository Contains

For each part of the course, this repo includes:

- The **from-scratch implementation** built during the video (e.g. a manual dot product before using NumPy's)
- The **exercises** given at the end of each video, solved independently
- Notes on the **key intuition** behind each concept, in plain language
- Where relevant, a **comparison** between the manual implementation and the equivalent library call, including a performance benchmark

---

## Key Concepts Covered

**Foundations**
- Variables, memory referencing, numeric types, string parsing and formatting
- Arrays vs. NumPy arrays, and *why* vectorized (homogeneous, SIMD-backed) arrays are 20x+ faster than native Python loops

**Data Analysis From Scratch**
- A hand-built `Vector`, `Column`, and `DataFrame` implementation, mirroring how pandas works internally
- Log returns and why they are used instead of raw prices or simple returns (time additivity, symmetry)

**Statistics and Time Series**
- Mean vs. median, standard deviation, correlation
- Stationarity vs. non-stationarity, and why differencing does not guarantee stationarity
- Auto-regressive (AR1) modeling of **mean reversion** and **momentum** — the two fundamental trading dynamics

**Modeling**
- Matrix algebra (matrix-scalar, matrix-vector operations, the critical distinction between broadcasting and true matrix multiplication)
- A linear regression model trained with PyTorch to forecast future log returns
- A logistic regression classifier to predict directional movement (up/down), including probability calibration

**Evaluating an Edge (the most important lesson of the course)**
- **Win rate is not the same as profitability.** A model with 50.7% directional accuracy can still be highly profitable if wins are marginally larger than losses and trade frequency is high
- Directional accuracy, precision/recall by direction, confusion matrices, ROC/AUC
- The **Girko statistic** (excess predictability vs. a random-guess benchmark)
- Decomposed returns: separating a prediction into **direction** (sign) and **magnitude** (absolute size)

**Validation**
- Expanding window, rolling window, and time-series split cross-validation, and why standard k-fold cross-validation is invalid for time series data (it breaks temporal order and causes data leakage)

**Strategy and Execution**
- Time-based vs. predicate-based entry/exit signals, and why time-based signals better complement time-series models
- Static vs. compounding trade sizing — demonstrated to produce meaningfully different total returns from the *exact same* underlying model
- Leverage: how it magnifies both gains and losses, and why it should be sized proportionally to statistical edge (e.g. Sharpe ratio), not used indiscriminately
- The course's key formula: **Alpha = Edge × Execution**, where Execution = Compounding × Leverage

**Live Deployment**
- An asynchronous trading bot (Python `asyncio`) that streams live trade data over WebSocket, maintains a sliding-window feature buffer, makes a prediction on a fixed interval, and places real orders on an exchange testnet
- Reconnection handling, a lightweight inference-only linear regression class, and a modular strategy/exchange interface

---

## Tech Stack

- **Python** — all core logic
- **NumPy** — vectorized array and matrix operations
- **pandas** — data frame manipulation (once the hand-built version is understood)
- **PyTorch** — model training (linear regression, logistic regression) and gradient-based optimization
- **Matplotlib** — equity curves, distributions, ROC curves
- **WebSocket / REST API** (exchange testnet, e.g. Hyperliquid or Binance testnet) — live market data and order execution
- **Google Colab** — primary development environment used throughout the course

---

## Project Structure

```
quant-trading-accelerator/
│
├── part1_variables/
│   ├── notes.md
│   ├── exercises.py
│   └── exercises_solutions.py
│
├── part2_arrays/
│   ├── notes.md
│   ├── numpy_benchmark.py
│   └── exercises_solutions.py
│
├── part3_vectorization/
│   ├── vector.py                # hand-built Vector class
│   ├── dataframe.py             # hand-built Column / DataFrame classes
│   ├── notes.md
│   └── exercises_solutions.py
│
├── part4_time_series/
│   ├── ar1_model.py
│   ├── notes.md
│   └── exercises_solutions.py
│
├── part5_matrices_and_edge/
│   ├── matrix_ops.py
│   ├── regression_model.py
│   ├── notes.md
│   └── exercises_solutions.py
│
├── part6_classification/
│   ├── classifier_model.py
│   ├── girko_statistic.py
│   ├── notes.md
│   └── exercises_solutions.py
│
├── part7_cross_validation/
│   ├── expanding_window_cv.py
│   ├── rolling_window_cv.py
│   ├── time_series_split_cv.py
│   └── notes.md
│
├── part8_strategy/
│   ├── entry_exit_signals.py
│   ├── trade_sizing.py
│   ├── notes.md
│   └── exercises_solutions.py
│
├── part9_live_deployment/
│   ├── main.py
│   ├── stream.py
│   ├── model.py
│   ├── strategy.py
│   ├── exchange.py
│   ├── research_notebook.ipynb
│   ├── .env.example
│   └── environment.yml
│
├── results/
│   └── equity_curves/
│
├── requirements.txt
└── README.md
```

---

## How to Run

Most of Parts 1–8 are designed to be run interactively in Google Colab or Jupyter, following each video. Part 9 is a standalone deployable application.

**For Parts 1–8 (research/learning notebooks):**

1. **Clone the repository**
   ```
   git clone <repository-url>
   cd quant-trading-accelerator
   ```

2. **Install dependencies**
   ```
   pip install -r requirements.txt
   ```

3. **Open the relevant part's notebook or script** and run cells sequentially — each part depends on data/functions introduced earlier in that same part.

**For Part 9 (live trading bot):**

1. **Navigate to the deployment folder**
   ```
   cd part9_live_deployment
   ```

2. **Create the conda environment**
   ```
   conda env create -f environment.yml
   conda activate quant-trading-accelerator
   ```

3. **Set up environment variables** — copy `.env.example` to `.env` and fill in your exchange **testnet** wallet address and private key. Never commit real credentials.

4. **Configure trading parameters** in `main.py` — trading interval, coin, model weight and bias (found via the research notebook first).

5. **Run the research notebook** to determine a profitable weight/bias/interval combination before running the live bot.

6. **Run the bot**
   ```
   python main.py
   ```

---

## Progress Log

| Part | Status | Notes |
|------|--------|-------|
| 1 — Variables | ☐ Not started / ☐ In progress / ☐ Complete | |
| 2 — Arrays | ☐ Not started / ☐ In progress / ☐ Complete | |
| 3 — Vectorization | ☐ Not started / ☐ In progress / ☐ Complete | |
| 4 — Time Series | ☐ Not started / ☐ In progress / ☐ Complete | |
| 5 — Matrices & Edge | ☐ Not started / ☐ In progress / ☐ Complete | |
| 6 — Classification | ☐ Not started / ☐ In progress / ☐ Complete | |
| 7 — Cross-Validation | ☐ Not started / ☐ In progress / ☐ Complete | |
| 8 — Strategy | ☐ Not started / ☐ In progress / ☐ Complete | |
| 9 — Live Deployment | ☐ Not started / ☐ In progress / ☐ Complete | |

*(Update this table as each part is completed and committed.)*

---

## Key Takeaways

- **Win rate is not edge.** A directional accuracy just above 50% can still be highly profitable; expected value, not hit rate, is what matters.
- **No discriminative power means no predictive power**, even if a model looks profitable — always check whether a model is simply mimicking a buy-and-hold trend before trusting its edge.
- **Execution is as important as the model.** The exact same statistical edge can produce dramatically different returns depending on trade sizing (static vs. compounding) and leverage.
- **Time series cross-validation must preserve temporal order.** Standard shuffled k-fold validation silently introduces data leakage and produces misleadingly good results.
- **Fees decide feasibility.** A strategy profitable on a gross basis can become unprofitable once realistic maker/taker fees are applied — this must always be checked before considering a strategy real.

---

## Limitations

- The models built in this course are deliberately simple (AR1, single/few-lag linear and logistic regression) for educational clarity, not designed to be maximally competitive alpha
- Live deployment (Part 9) is demonstrated on an exchange testnet, not with real capital
- Transaction fees, slippage, and realistic order book depth are only partially modeled and are left as exercises in several parts
- The course uses hourly OHLCV data; real trading firms typically operate on order book / tick-level data, which is acknowledged but out of scope here

---

## Future Work

- Extend Part 9's single-lag AR1 model to the multi-lag logistic regression developed in Part 6
- Add proper net-P&L calculation with real maker/taker fee schedules (left as an exercise in Part 8)
- Experiment with different resampling intervals (8h, 12h, daily) as suggested in Part 8's exercises
- Explore the decomposed-return approach (direction + magnitude models combined) proposed in Part 6
- Add unit tests to the Part 9 deployment code, which the course intentionally omits for simplicity

---

## Acknowledgements

Course content created by **MemLabs**. This repository contains an independent implementation and personal notes following the course; all conceptual credit belongs to the original creator. Consider supporting the original series via Patreon or Buy Me a Coffee (linked in the course videos), since the course is offered free thanks to that support.

## License

This project is for educational and research purposes only and does not constitute financial advice.
