# Trader Performance vs Market Sentiment — Analysis

## Objective
Analyze how market sentiment (Fear/Greed) relates to trader behavior and 
performance on Hyperliquid, and identify patterns that could inform trading 
strategy decisions.

## Datasets
- **Bitcoin Fear/Greed Index** — daily market sentiment classification (2018–2025)
- **Hyperliquid Historical Trader Data** — 211,224 individual trade executions 
  (2023–2025), including account, execution price, size, side, and closed PnL

## Methodology
1. **Data Preparation:** Cleaned both datasets, converted timestamps, and 
   aggregated trade-level data to account-day level (daily PnL, average trade 
   size, trade frequency, win rate, long ratio) to match sentiment's daily 
   granularity. Merged on date using a left join.
2. **Performance Analysis:** Compared average and median daily PnL and win 
   rate across sentiment categories.
3. **Behavior Analysis:** Compared trading frequency, trade size, and long/short 
   bias across sentiment categories.
4. **Segmentation:** Split traders into Frequent/Infrequent (by trade count) 
   and Consistent/Inconsistent (by win rate), then compared performance across 
   sentiment within each segment.


## Tools
Python, pandas, seaborn, matplotlib

## Key Insights
1. **Mean vs median PnL diverge sharply, especially on Fear days** — average 
   figures are inflated by a small number of outlier accounts; median PnL is 
   actually highest during Extreme Greed and lowest during Fear.
2. **Trading activity is highest during Extreme Fear (133.8 trades/day) and 
   lowest during Extreme Greed (76.0)** — traders are more active during 
   fearful, volatile conditions.
3. **Trader skill/consistency, not sentiment, is the dominant driver of 
   profitability.** Both frequency-based and consistency-based segmentation 
   show that infrequent/inconsistent traders hover near zero median PnL 
   regardless of sentiment, while frequent/consistent traders show strong, 
   sentiment-sensitive performance.

## Strategy Recommendations
1. Target sentiment-based trading rules at already-frequent, already-consistent 
   traders — these adjustments show negligible effect for other traders.

   **Why:** Frequency alone doesn't indicate skill — an account can trade 100 times a day 
and still lose consistently. Win rate is the more direct signal of whether an account 
has a real edge. Gating sentiment-based plays by consistency ensures the strategy only 
amplifies accounts that already know how to convert opportunity into profit, rather than 
scaling activity for accounts where more trades just means more noise.

2. Use median, not mean, when evaluating Fear-day performance — average figures 
   overstate what a typical trader can expect.
   
   **Why:** A 49x mean/median gap in Fear means the "average" outcome almost never happens — 
it's manufactured by a handful of large winners. Sizing decisions based on that mean would 
systematically overestimate what a typical trade will actually return. Extreme Greed's much 
lower ratio (12.3x) means its median is a far more reliable predictor of a typical outcome, 
justifying more confident, standard-to-elevated sizing there.

## Final Result

This analysis set out to determine whether market sentiment (Fear/Greed) drives 
trader performance and behavior on Hyperliquid — and whether that relationship 
could inform a smarter trading strategy.

**The answer is more nuanced than a simple yes or no.** Sentiment does correlate 
with behavior — traders are meaningfully more active during Fear (133.8 trades/day) 
than Greed (76.0), and show a contrarian long-bias, buying into weakness rather 
than chasing strength. But sentiment is a weak, unreliable predictor of actual 
profitability on its own. The data shows that **who is trading matters far more 
than what the market is feeling**: accounts with below-median win rates post a 
median daily PnL of exactly $0.00 in every single sentiment category, regardless 
of how active they are — while consistent, high-win-rate accounts show strong, 
sentiment-sensitive performance throughout.

The clearest actionable signal isn't a directional one ("buy during Fear, sell 
during Greed") — it's a **risk and targeting framework**: sentiment-based 
strategies should be gated to traders who already demonstrate consistency, and 
position sizing should account for the fact that Fear-day outcomes are the most 
outlier-driven and least representative in the dataset (a 49x gap between mean 
and median), while Extreme Greed offers the most statistically reliable typical 
outcome.

In short: **sentiment shapes behavior, but skill determines outcome.** A 
sentiment-aware strategy only adds value layered on top of an already-consistent 
trading approach — it is not a substitute for one.


