# crypto-p2p-spread-finder

I write this to monitor P2P spreads on Binance across different payment methods. It helps me find quick arbitrage paths (e.g. buying via one bank and selling via another) without constantly clicking through the web UI.

It queries the Binance P2P API directly, filters out unrealistic ads using a minimum transaction volume, and outputs a clean matrix of spreads.

## Installation

Clone the repository and install the dependencies. I recommend using a virtual environment:

```bash
pip install -r requirements.txt
```

## Usage

Run the script directly from your terminal. By default, it looks for USDT spreads using USD fiat, comparing popular payment options.

```bash
python find_spread.py --fiat USD --methods Revolut,Wise,Zen --amount 100
```

### Options

* `--fiat`: The fiat currency to scan (e.g., USD, EUR, GBP, KZT). Default is `USD`.
* `--asset`: The crypto asset to target. Default is `USDT`.
* `--methods`: Comma-separated list of payment methods to compare.
* `--amount`: Filter ads that don't support this minimum transaction amount in fiat. Important to filter out tiny noise ads.
* `--watch`: Keep running every N seconds (e.g., `--watch 30`).
* `--fee`: Apply a custom fee percentage (e.g., `0.1` for 0.1% maker fee) to the spread calculations.

### Example Output

```
[14:23:10] Scanning USDT spreads for USD (Min Amount: 100.0)

Top rates found:
  Wise (BUY): 1.012
  Wise (SELL): 1.009
  Revolut (BUY): 1.015
  Revolut (SELL): 1.011
  Zen (BUY): 1.005
  Zen (SELL): 1.002

Profitability Matrix (Spread % minus 0.00% fee):
  Buy Method    Sell Method   Buy Price   Sell Price  Spread %
  ------------------------------------------------------------
  Zen           Revolut       1.005       1.011       +0.60%
  Zen           Wise          1.005       1.009       +0.40%
  Wise          Revolut       1.012       1.011       -0.10%
```

<!-- verified: 2026-09-22 -->
