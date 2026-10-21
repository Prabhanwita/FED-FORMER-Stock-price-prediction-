# Nifty 50 Stock Price Forecasting using FEDformer

## Overview

This repository contains a Jupyter Notebook for short-horizon
forecasting of Nifty 50 stock prices using minute-level stock-market
data. The notebook downloads a Kaggle dataset, loads a subset of stock
CSV files, checks data quality, engineers technical indicators, trains
deep-learning time-series models, evaluates predictions, visualizes
comparisons, and includes an exploratory backtesting routine.

**Notebook:** `Final_Submission_FED_FORMER_Group_5.ipynb`

## Objectives

-   Prepare and validate minute-level stock price data.
-   Engineer technical indicators from OHLCV data.
-   Implement a FEDformer-style encoder-decoder with frequency-enhanced
    attention and trend/seasonal decomposition.
-   Compare FEDformer with PatchTST and other model variants present in
    the notebook.
-   Evaluate forecasts using MAE, RMSE, and directional accuracy.
-   Explore sector-level comparisons and a basic prediction-driven
    backtest.

## Dataset

The notebook retrieves data using KaggleHub from:

`debashis74017/stock-market-data-nifty-50-stocks-1-min-data`

The code loads a subset of CSV files from the downloaded dataset
(currently the first 20 files returned by the directory listing).
Because file listing order may vary, consider sorting the filenames and
explicitly recording the selected stocks for reproducible runs.

Check the dataset's license and Kaggle terms before redistributing data.
Raw data files are not required to be committed to this repository.

## Models and approach

### FEDformer

The notebook includes a FEDformer-style architecture with: -
Trend/seasonal decomposition blocks. - Frequency-enhanced attention
using frequency-domain operations. - Encoder and decoder layers. -
Separate trend and seasonal output components.

### Comparison models

-   **PatchTST** --- patch-based time-series Transformer baseline.
-   **Autoformer-related implementation/components** --- additional
    comparison logic appears in the notebook.

Use the actual executed notebook results to determine which model
performs best; this README does not assume or invent a performance
ranking.

## Features

The feature-engineering workflow is designed around OHLCV fields and
technical indicators including: - Open, high, low, close, and volume -
RSI (Relative Strength Index) - MACD - Bollinger Bands - EMA
(Exponential Moving Average)

Confirm the final feature list and column ordering in the executed
notebook before reproducing a run.

## Evaluation

The notebook calculates or prepares evaluation using: - **MAE** --- Mean
Absolute Error - **RMSE** --- Root Mean Squared Error - **Directional
Accuracy** --- whether predicted price direction matches actual movement

It also includes model/sector comparison visualizations and a simple
backtesting routine with configurable initial capital and
transaction-cost assumptions. Backtest output is exploratory and is not
investment advice.

## Active configuration note

The notebook's introductory section describes intended horizons of 24,
48, 96, and 192 minutes. The later active configuration sets:

``` python
PRED_HORIZONS = [12]
```

Therefore, document the horizon actually used in the run, rather than
assuming all originally planned horizons were evaluated. Verify the
executed train/validation/test split, sequence lengths, and selected
stocks before reporting results.

## Technology stack

-   Python
-   Jupyter Notebook
-   Pandas and NumPy
-   PyTorch
-   Scikit-learn
-   KaggleHub
-   `ta` technical-analysis library
-   Matplotlib

## Repository structure

``` text
.
├── Final_Submission_FED_FORMER_Group_5.ipynb
├── Agile_Software_Development_Document_FEDformer_Nifty50.pdf
└── README.md
```

The PDF is optional; include it in the repository only if you want to
publish the project documentation alongside the notebook.

## Getting started

### 1. Clone the repository

``` bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
```

Replace the placeholders with your actual GitHub repository URL and
directory name.

### 2. Install dependencies

``` bash
pip install jupyter kagglehub pandas numpy torch scikit-learn matplotlib ta
```

Install a PyTorch build suitable for your CPU/GPU environment. Package
versions may need adjustment to match the notebook runtime.

### 3. Run the notebook

``` bash
jupyter notebook Final_Submission_FED_FORMER_Group_5.ipynb
```

Run the cells in order. KaggleHub may require access to the dataset and
appropriate Kaggle authentication or permissions.

## Reproducibility checklist

-   Sort and record selected stock filenames.
-   Record dataset version, random seeds, and package versions.
-   Preserve chronological ordering when splitting time-series data.
-   Fit scalers using training data only.
-   Ensure target timestamps are strictly after input timestamps.
-   Compare models on the same stocks, test windows, and forecast
    horizons.
-   Report the exact active configuration and actual test metrics.
-   Save plots and result tables from the executed notebook.

## Limitations

-   Financial time series are noisy and non-stationary.
-   Results can vary across stocks, sectors, market regimes, and
    forecast horizons.
-   Missing or inconsistent input data can affect training and
    evaluation.
-   A small selected stock subset may not represent the full Nifty 50
    universe.
-   A simplified backtest may omit practical constraints such as
    slippage, liquidity, taxes, and execution delays.
-   Forecasting performance does not guarantee profitable trading.

## Future improvements

-   Explicitly select and document stocks instead of relying on
    directory order.
-   Evaluate multiple horizons consistently.
-   Add a strict walk-forward evaluation protocol.
-   Include per-stock and per-sector error analysis.
-   Expand backtesting with realistic transaction costs and trading
    constraints.
-   Save model checkpoints, metrics, plots, and configuration files.
-   Add a verified `requirements.txt`.

## License and citations

Add a license that matches your intended code-sharing terms. Cite the
dataset and relevant model papers in the final report, and comply with
dataset-provider terms.
