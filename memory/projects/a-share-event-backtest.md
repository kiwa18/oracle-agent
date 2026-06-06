# A-share Event Backtest Memory

Last updated: 2026-06-06 Asia/Shanghai

## 1. User Goal

The user has a TongDaXin indicator that produces buy-point signals only. It has no sell signal.

The goal is not a normal same-day-buy strategy backtest. The goal is a full A-share event-path research system that answers:

- After a signal appears on date `T`, buying after how many trading days gives the best win rate and return?
- For each buy delay `N`, how does holding or observing for `M` trading days perform?
- What happens in the half-month or one-month path after the signal?
- Which signals launch immediately, fail directly, adjust sideways and then succeed, or adjust sideways and still fail?
- What repeatable factors distinguish success from failure across different boards, industries, concepts, market phases, liquidity layers, and path shapes?

Important user correction:

- Do not assume buying on the signal day.
- Signal day `T` is only the event origin.
- The main research object is the future path after the signal, especially `T+1` to `T+30`.

## 2. Core Design Choice

Because there is no sell signal, V1 should not invent a fake sell indicator.

Use time factors and future observation windows instead:

- Buy delay candidates: `T+1`, `T+2`, `T+3`, `T+5`, `T+10`, optionally `T+15`, `T+20`.
- Observation or holding windows: `5`, `10`, `20`, `30` trading days.
- Outcome targets: maximum forward return, close-to-close return, maximum drawdown, first breakout day, first breakdown day, sideways-adjustment duration, and whether a target return is reached.

This makes the system an event-path research platform rather than a simple entry/exit backtester.

## 3. Recommended Architecture

```text
TongDaXin local historical daily data
  ↓
Local all-A-share price warehouse
  ↓
TongDaXin formula conversion to signal series
  ↓
Signal event table
  ↓
Forward path panel for each event
  ↓
Buy-delay / observation-window matrix
  ↓
Path classification
  ↓
Grouped statistics and factor comparison
  ↓
Reports and next-round rule discovery
```

### 3.1 Data Layer

Primary price source:

- Use local TongDaXin downloaded daily data as the primary historical price source.
- Prefer reading local `vipdoc` daily files or exported daily data, then converting to Parquet.
- This avoids relying on unstable web endpoints for full-market, multi-year batch scans.

Auxiliary data sources:

- Use `a-stock-data` for sector/concept, funds, announcements, research, 龙虎榜, financing, and other auxiliary fields where useful.
- Use `mootdx` or `pytdx` to read TongDaXin-compatible local or online market data when needed.
- Use `MyTT` or a small compatible formula layer to translate common TongDaXin indicator functions.

Storage:

- Use `Parquet + DuckDB` as the default local research warehouse.
- Keep SQLite only for metadata if needed.
- Do not use PostgreSQL in V1 unless there is a clear need for multi-user service or long-running deployment.

Core tables:

- `daily_price`: `code`, `date`, `open`, `high`, `low`, `close`, `volume`, `amount`, `adj_factor`, `source`, `updated_at`
- `stock_meta`: `code`, `name`, `exchange`, `board`, `list_date`, `delist_date`, `is_st`, `is_active`
- `trade_calendar`: `date`, `is_trade_day`, `prev_trade_date`, `next_trade_date`
- `sector_membership`: `code`, `sector_type`, `sector_code`, `sector_name`, `start_date`, `end_date`, `source`
- `signal_event`: `event_id`, `code`, `signal_date`, `signal_name`, `signal_value`, `valid_flag`, `invalid_reason`
- `event_path`: normalized forward path rows for every event and future day offset
- `event_result`: buy-delay and observation-window results
- `path_label`: path classification labels and features

## 4. Formula Conversion

V1 should not build a complete TongDaXin interpreter. Start with a controlled subset.

High-priority functions:

- `REF`
- `MA`
- `EMA`
- `SMA`
- `HHV`
- `LLV`
- `COUNT`
- `CROSS`
- `BARSLAST`
- `EVERY`
- `EXIST`
- `IF`

Rules:

- `REF(C,1)` means yesterday's close; in pandas it is usually `close.shift(1)`.
- `CROSS(A,B)` must be crossing logic, not merely `A > B`: `(A > B) & (A.shift(1) <= B.shift(1))`.
- `HHV(H,0)` in TongDaXin means highest since listing, not a zero-length window.
- Ban or flag future-looking functions in V1, such as `BACKSET`, `DRAWLINE`, `ZIG`, `PEAK`, `TROUGH`, and `REFX`.
- The user's private formula should not be stored in GitHub memory unless the user explicitly asks.

## 5. Signal Event Treatment

A signal on `T` is an event origin, not a trade.

For every valid signal:

- Find the next trade days after `T`.
- Build a forward path from `T+1` to at least `T+30`.
- Exclude or tag invalid cases: insufficient future data, suspension, delisted soon, ST if excluded, one-price limit, missing price, newly listed too short.
- For each buy delay `N`, use the open/close policy decided later, such as buying at `T+N` open or close.

Avoid lookahead leakage:

- Prediction features for buying on `T+N` can only use data from `T` through `T+N`.
- Post-event attribution can use the full future path, but must be labeled as analysis-only, not real-time tradable logic.

## 6. Time-Factor Backtest Matrix

Initial matrix:

- `buy_delay_list = [1, 2, 3, 5, 10, 15, 20]`
- `observe_days_list = [5, 10, 20, 30]`
- Optional target returns: `[0.05, 0.08, 0.10, 0.15, 0.20]`
- Optional stop levels for analysis only: `[-0.03, -0.05, -0.08, -0.10]`

Metrics per `(buy_delay, observe_days)`:

- sample count
- average return
- median return
- win rate
- target-hit rate
- average maximum forward return
- average maximum drawdown
- first target-hit day
- first breakdown day
- return volatility
- worst loss
- invalid or untradable ratio

Do not over-expand the parameter grid in V1 to avoid parameter mining.

## 7. Path Classification

Recommended V1 labels:

- `IMMEDIATE_SUCCESS`: starts rising quickly after signal and reaches target in a short window.
- `DIRECT_FAIL`: breaks down soon after signal and does not recover within the observation window.
- `SIDEWAYS_THEN_SUCCESS`: enters sideways adjustment, then breaks upward and reaches target.
- `SIDEWAYS_THEN_FAIL`: appears to adjust sideways, but later breaks downward or never launches.
- `SLOW_SUCCESS`: no immediate launch, but gradually reaches target later.
- `OSCILLATION_NO_EFFECT`: noisy movement without clear upward or downward outcome.
- `INVALID_BUY`: suspension, one-price limit, missing data, or impossible trade.
- `INSUFFICIENT_FUTURE`: not enough future bars to judge.

## 8. Sideways Adjustment Definition

Sideways adjustment should be measurable, not just visual.

A candidate V1 definition:

Within `K` days after signal, such as `K = 5`, `10`, or `15`:

- maximum return is below a launch threshold, for example `< +8%`
- maximum drawdown does not destroy the setup, for example `> -8%` or not below signal-day low by too much
- price range narrows or remains bounded
- volume contracts compared with the signal day or previous window
- the stock does not sharply underperform its industry/concept/market benchmark

Then judge later outcome:

- If it reaches `+10%`, `+15%`, or `+20%` within `20` or `30` trading days: sideways then success.
- If it breaks below key low, fails to reach target, or continues weakening: sideways then fail.

Important comparison:

- Compare `SIDEWAYS_THEN_SUCCESS` against `SIDEWAYS_THEN_FAIL` to identify repeatable differences.

## 9. Feature System

Event-day features:

- signal strength if formula provides continuous value
- signal-day return
- signal-day volume ratio
- position relative to moving averages
- recent high/low position
- recent volatility
- market cap and turnover amount
- board: main board, ChiNext, STAR, Beijing, ST/non-ST

Post-signal early-window features available by `T+N`:

- return from `T` to `T+N`
- maximum drawdown from `T` to `T+N`
- amplitude compression
- volume contraction or expansion
- whether price stays above signal-day low
- whether price breaks recent high
- relative strength vs index/industry/concept
- number of red/green candles
- limit-up/limit-down and suspension flags

Full-path attribution features:

- maximum future return
- maximum future drawdown
- first target-hit day
- first breakdown day
- sideways duration
- breakout day volume ratio
- pullback depth before launch
- sector strength before launch

## 10. Grouped Statistics

Required grouping dimensions:

- board: main board, ChiNext, STAR Market, Beijing Stock Exchange, ST
- industry
- concept/sector
- year and month
- market phase
- market cap bucket
- liquidity bucket by amount or turnover
- signal strength bucket
- price level bucket
- new listing age bucket

Important caution:

- Do not use current sector membership to judge historical signals if a historical membership table is available.
- Correct structure: `code | sector_id | start_date | end_date`.
- If only current concept membership is available in V1, mark concept backtests as approximate and not historically strict.

## 11. Methods For Finding Repeatable Differences

Start simple, then add models only after labels are stable.

Manual statistical comparison:

- Compare success and failure groups by mean, median, percentile, and distribution.
- Use contingency tables for binary features.
- Use bootstrap confidence intervals for unstable small samples.
- Track sample counts before trusting any high win rate.

Shape and path methods:

- Normalize post-signal paths by signal-day close.
- Cluster paths using DTW or shape-based time-series clustering.
- Use shapelets to discover patterns like shallow pullback, sideways compression, or failed rebound.

Machine learning for explanation, not blind prediction:

- Start with decision trees or random forests for interpretable splits.
- Consider LightGBM later when sample size and labels are reliable.
- Use feature importance or SHAP-style explanation to identify drivers.
- Always separate tradable prediction features from post-event attribution features.

## 12. Key Risks And Anti-Distortion Rules

High-risk distortions:

- using current stock universe and omitting delisted stocks
- using current sector membership to judge historical events
- assuming signal-day buy when the signal may only be known after close
- assuming one-price limit-up stocks can be bought
- assuming one-price limit-down stocks can be sold
- treating suspension days as normal trading days
- using adjusted prices to judge limit-up/limit-down
- mixing ST, new stocks, and normal stocks without tags
- sweeping too many parameters and overfitting
- failing to detect future-looking TongDaXin functions

V1 should tag all questionable samples instead of silently including them.

## 13. Candidate Open-Source Projects And References

A-share data and TongDaXin-related:

- `simonlin1212/a-stock-data`: https://github.com/simonlin1212/a-stock-data
  - GitHub README checked on 2026-06-06. It is an A-share data Skill/tool package. README showed V3.2.2, seven-layer architecture, 27 endpoints, 13 data sources, and no akshare dependency in V3.x. Use as auxiliary data source, not as the only historical warehouse.
- `mootdx/mootdx`: https://github.com/mootdx/mootdx
  - GitHub README checked on 2026-06-06. It supports reading TongDaXin offline daily data via `Reader.factory(...).daily(symbol=...)`, plus online bars.
- `yutiansut/pytdx`: https://github.com/yutiansut/pytdx
  - GitHub README checked on 2026-06-06. It is a pure Python TongDaXin-like market data API and includes data-file reading capability.
- `mpquant/MyTT`: https://github.com/mpquant/MyTT
  - GitHub README checked on 2026-06-06. It provides common TongDaXin/TongHuaShun-style indicator functions in Python, including `REF`, `MA`, `EMA`, `CROSS`, `COUNT`, `EVERY`, `EXIST`, `BARSLAST`, `HHV`, and `LLV`.

Data warehouse:

- DuckDB Parquet docs: https://duckdb.org/docs/stable/data/parquet/overview
- Apache Parquet: https://parquet.apache.org/

Event labeling and path research:

- Triple barrier method concept: useful for labeling whether a path first reaches an upper target, lower target, or time barrier.
- Candidate Python project: https://github.com/mchiuminatto/triple_barrier
- tsfresh feature extraction docs: https://tsfresh.readthedocs.io/
- tslearn time-series methods docs: https://tslearn.readthedocs.io/

## 14. Recommended V1 Implementation Plan

Step 1: Confirm data source

- User downloads complete daily history in TongDaXin.
- Locate TongDaXin data directory.
- Read a few sample stocks and verify date, open/high/low/close/volume/amount correctness.

Step 2: Build local price warehouse

- Convert daily files into Parquet partitioned by market/year or by code.
- Build stock list, trading calendar, and basic validity flags.

Step 3: Convert the TongDaXin formula

- User provides the indicator formula.
- Translate only necessary functions first.
- Detect and reject future-looking functions.
- Produce a signal event table.

Step 4: Build event path panel

- For every signal, create `T+1` to `T+30` forward bars.
- Normalize by signal-day close.
- Add flags for suspension, limit, ST, and insufficient future data.

Step 5: Run time-factor matrix

- Test buy delay `N` and observation/holding window `M`.
- Output win rate, return, drawdown, target-hit rate, and invalid ratio.

Step 6: Label paths

- First implement rule-based labels.
- Visualize sample paths from each label to check whether labels match human intuition.

Step 7: Compare success and failure

- Compare `IMMEDIATE_SUCCESS` vs `DIRECT_FAIL`.
- Compare `SIDEWAYS_THEN_SUCCESS` vs `SIDEWAYS_THEN_FAIL`.
- Group by board, industry, concept, market phase, liquidity, and signal strength.

Step 8: Report and iterate

- Generate tables and charts.
- Identify robust candidate rules.
- Keep all thresholds explicit and adjustable.

## 15. Open Questions For Next Session

- Where is the user's TongDaXin installed and where is the downloaded daily data directory?
- What is the exact TongDaXin indicator formula?
- Should ST, newly listed stocks, Beijing Exchange, and one-price limit-up days be included or tagged only?
- Should buy price use next-day open, next-day close, or configurable execution policy?
- What return threshold defines success: `+8%`, `+10%`, `+15%`, `+20%`, or multiple thresholds?
- What drawdown threshold defines failure: `-5%`, `-8%`, `-10%`, or multiple thresholds?
- What is the first report format: CSV, Excel, web dashboard, or notebook-style HTML?

## 16. Continuation Trigger

When the user says `继续回测输出`, `继续回策输出`, `调出回测记忆`, or asks to continue the A-share buy-point research, read this file first and continue from Section 14.
