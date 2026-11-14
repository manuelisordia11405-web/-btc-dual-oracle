# Bitcoin Predictor 4.0 — 15-minute research dashboard

A mobile-friendly, static GitHub Pages dashboard. **No API key or paid hosting required.**

## Deploy to GitHub Pages

1. Open your existing GitHub Pages repository.
2. Upload/replace `index.html`, `style.css`, and `app.js` in the repository root (the `main` branch).
3. Commit the changes. In Settings → Pages, set **Deploy from a branch**, branch **main**, folder **/(root)**.
4. Wait for Pages to publish, then hard-refresh your site.

You can also create a new public repository and upload these three files. GitHub Pages is supported for public repositories on free plans.

## Data and signal methodology

- Fetches 1-minute BTC/USD candles from Binance.US, falling back to Coinbase Exchange.
- Uses only **completed** 1-minute candles. Updates once per minute. Displays age and refuses a directional signal when data is over 3 minutes old.
- EMA(9) vs EMA(21), price vs EMA(50), MACD histogram, RSI(14), and 15-minute price change each vote with fixed weights (2,2,2,1,2).
- Score is absolute weighted vote / 9 × 100. **It is not a calibrated probability.**
- UP/DOWN requires at least 6 of 9 net weighted votes in the same direction. Otherwise WAIT.
- WAIT vetoes include relative volume < 0.65, ATR(14) / price > 0.35%, RSI > 75 or < 25, and stale market data.
- Next UTC quarter-hour countdown is only a clock reference. **It is not a claim about the timing or settlement of any specific Kalshi market.**
- Kalshi contract checker requires user-entered YES ask, independent UP probability, and fees. It never invents a probability or submits an order.
- Journal outcomes are manually recorded and kept in browser localStorage. CSV export is available. This is not an automated verified backtest.

## Limitations

Data endpoints may block some browsers/regions or experience downtime. A static website cannot reliably query every Kalshi contract or provide guaranteed market availability without a maintained backend. The dashboard uses spot BTC/USD as a reference, which can differ from Kalshi's contract settlement source and strike. The heuristics are **not validated trading alpha**, and their weights/thresholds are illustrative, not optimized by historical testing. Market fees, bid-ask spread, slippage, and contract rules matter. Do not trade based on the displayed signal alone.
