# Financial News Sentiment vs. NIFTY50 Analysis — Project Summary

## Key EDA Finding

The dataset covered 132 trading days (Feb to Aug 2025) with a fairly balanced target (67 down days, 65 up days). A hand-built sentiment scorer (59 positive terms, 53 negative terms drawn from real financial vocabulary) produced scores ranging from -24 to +36, with a right-skewed distribution centered around +6. Grouping by market direction showed a real average difference: up days had a mean sentiment score of about 9.2, versus about 2.8 on down days, over 3x higher. However, the scatter plot of sentiment vs. daily price movement showed no clean linear relationship; large up and down moves both occurred across the full range of sentiment scores. The takeaway: sentiment shows a directional pattern on average, but is too noisy to explain individual day-to-day movement.

## Part A: Same-Day Rule-Based Prediction

A simple rule (positive sentiment → predict "up") was evaluated against same-day market direction:

- **Prediction accuracy: 62.88%**
- **Majority-class baseline: 50.76%**

This is a real lift over baseline (about 12 points), but it measures **same-day co-movement**, not forecasting ability. Sentiment and price often move together on the same day because they share the same underlying cause, for example an earnings report drives both the headline and the price. This rule could not be traded on in practice, since it requires the same day's headlines to already be known before that day's close.

## Part B: Next-Day Machine Learning Pipeline

The target was corrected to predict **tomorrow's** direction using only information available as of today's close (rolling sentiment averages, lagged price movement, volume change, and volatility spread), with a strict chronological 80/20 train/test split (no shuffling) to prevent leakage.

| Model | Test Accuracy |
|---|---|
| Majority-class baseline (test period) | 56.0% |
| Logistic Regression | 48.0% |
| Random Forest (untuned) | 40.0% |
| XGBoost | 36.0% |
| Random Forest (tuned, TimeSeriesSplit + GridSearchCV) | 44.0% |

**None of the trained models beat the majority-class baseline** on the held-out test set, even after hyperparameter tuning. This is a consistent pattern across three different model families, not a fluke of one model. Feature importance from the tuned Random Forest showed pure price-history features (`high_low_spread`, `movement_lag1`) ranked above all sentiment features, with the smoothed 7-day rolling sentiment average outranking the raw daily sentiment score. This suggests that if any sentiment signal exists, it lives in the trend rather than any single day's headlines, and it is weaker than basic price-history signals. A simple backtest showed the strategy tracking close to buy-and-hold over the 25-day test window; this is illustrative only, ignores transaction costs, slippage, and taxes, and should not be read as a viable trading strategy given the small sample size and sub-baseline accuracy.

As a stretch goal, I also tested whether scoring properly joined plain text (instead of the stringified Python list of headlines) changed the sentiment scores. The two approaches produced identical scores for all 132 days, confirming that `.count()` matching on substrings made the list's formatting artifacts (commas, brackets, quotes) irrelevant to the scoring.

## What I Would Do Differently With More Time

With a larger date range (the current dataset only spans about 6 months, yielding just 100 training days after feature engineering), I would revisit whether sentiment adds value once there's enough data for the models to find a stable pattern rather than overfitting noise. I would also compare the hand-built word-list approach against a library-based sentiment tool like VADER, to check whether the scoring method itself, rather than the underlying signal, is the limiting factor.
