## Quant Trading Accelerator: Code, Exercises & Solutions

A companion repo for the **Quant Trading Accelerator**, a free 9-part YouTube course by [MemLabs](https://www.youtube.com/@memlabs-research) that teaches quant trading from zero by building things. Each lecture has its own folder here with the code from the video, a short explanation, and my solutions to the exercises the instructor sets at the end.

> **Playlist:** [Quant Trading Accelerator](https://www.youtube.com/playlist?list=PLdsqLas3-Kg1vGriabIjpaUNWzMQIbXH9) · **Course site:** [memlabs.dev](https://www.memlabs.dev/)

This is an unofficial, community companion, not the instructor's repo. All teaching content and original code belong to MemLabs.

---

### If you're watching the course, start here

The course only works if you build along, and the instructor says so himself. A good loop for each part:

1. **Watch** the video (about 20-40 min each).
2. **Open the folder** for that part and read its `README.md` (what it covers, what you need installed).
3. **Do the exercises yourself** in the video's Colab notebook. Each exercise has a built-in test that turns `True` when you're right.
4. **Only then** open `exercises_solutions.ipynb` to compare. Mine is one valid answer, not the only one.

If you're stuck on an exercise for a long time, peeking at one solution is fine. Just re-type it yourself rather than pasting it.

### Repo layout

```
.
├── README.md
├── 01-variables/
│   ├── README.md                  # what this lecture covers + requirements
│   ├── requirements.txt
│   ├── lecture.ipynb              # code from the video, explained in markdown cells
│   └── exercises_solutions.ipynb  # the video's exercises with my solutions
├── 02-arrays/
│   └── ...                        # same structure
├── ...
└── 09-trading-bot/
    └── README.md                  # notes + pointer to the instructor's bot repo
```

Every folder is self-contained: open the notebook in Colab or Jupyter, install that folder's `requirements.txt`, run. Explanations live in the notebook as markdown cells and short code comments. They are meant to help you follow along, not replace the video.

### Course map

| # | Lecture | Key ideas | Exercises (solutions in folder) |
|---|---------|-----------|----------------------------------|
| 1 | [Variables](https://www.youtube.com/watch?v=GgFW5R71UXM) | Variables, memory references, int/float, operator precedence, strings, f-strings | Price delta · Total P&L · Parse a raw string into symbol + price |
| 2 | [Arrays](https://www.youtube.com/watch?v=3rxwZN-Er-Y) | Lists, indexing, `pop()` speed, NumPy and SIMD, compounding, log returns | Average log return · Total log return of a portfolio · Cumulative log returns |
| 3 | [Vectorization](https://www.youtube.com/playlist?list=PLdsqLas3-Kg1vGriabIjpaUNWzMQIbXH9) | Vector algebra, vectorised mean/variance/std, Sharpe, a mini DataFrame from scratch, lags | Log returns as a one-liner · Add a log-return lag column · (optional) vectorised NaN filter |
| 4 | [Time Series](https://www.youtube.com/playlist?list=PLdsqLas3-Kg1vGriabIjpaUNWzMQIbXH9) | Mean vs median, dispersion, correlation, differencing, stationarity, AR(1) | No set exercises. Suggested: compute correlation by hand |
| 5 | [Statistical Edge](https://www.youtube.com/watch?v=5ZJK3LnCojs) | Matrix algebra, temporal train/test split, PyTorch regression, directional accuracy vs expected value | Dot product with loops · Transpose · Element-wise error (Hadamard) |
| 6 | [Classification](https://www.youtube.com/playlist?list=PLdsqLas3-Kg1vGriabIjpaUNWzMQIbXH9) | Predicting up/down with a probability | See video |
| 7 | [Cross Validation](https://www.youtube.com/playlist?list=PLdsqLas3-Kg1vGriabIjpaUNWzMQIbXH9) | Time-series split, rolling window, expanding window | Rolling window with independent train/test sizes · Expanding window across window sizes |
| 8 | [Strategy](https://www.youtube.com/watch?v=hI7UaWCEY9E) | Entry/exit signals, static vs compounding sizing, leverage, maker vs taker | Net P&L as taker · Net P&L as maker · Resample to 8h / 12h / 1d / 7d |
| 9 | [Trading Bot](https://www.youtube.com/watch?v=x2rBDc3wsL0) | Websockets, async tasks, sliding window, model → strategy → exchange | Run it on testnet · Experiment with intervals and lags in the research notebook |

Follow them in order. Each part builds on the last.

### Requirements

Parts 1-8 run in **Google Colab**, so you don't need to install anything locally. To run locally, each folder has a `requirements.txt` with only what that part needs (typically `numpy`, then `pandas` and `matplotlib` from Part 4, then `torch` from Part 5).

Part 9 is different: the bot lives in the instructor's own repository and uses a conda environment, so my folder only holds notes and a link there. Run it against **testnet** only.

### What the course teaches (the short version)

A quant strategy is a pipeline: **data → model → forecast → strategy → orders → exchange**. The course builds that whole pipeline on Bitcoin perpetual futures. Four ideas recur:

- **Win rate is not alpha.** A ~50.7% hit rate can still have positive expected value.
- **Never shuffle time series.** Split by time, or the future leaks into training.
- **Execution matters as much as the model.** Sizing and leverage change results a lot.
- **Gross is not net.** Early results ignore fees, which can erase the edge at short horizons.

### Progress

- [ ] 1 Variables
- [ ] 2 Arrays
- [ ] 3 Vectorization
- [ ] 4 Time Series
- [ ] 5 Statistical Edge
- [ ] 6 Classification
- [ ] 7 Cross Validation
- [ ] 8 Strategy
- [ ] 9 Trading Bot

### Disclaimer

Educational only. Most results in the course are gross of fees and the bot runs on testnet. Nothing here is financial advice, and a backtest is not a promise of live performance.
