# Talking Before Trading: Are StockTwits Comments Linked to Apple's Trading Volume?

BA780 Introduction to Data Analytics · Boston University Questrom School of Business · Fall 2026 · Team B08

## Team

- Alicia Mora
- Almira Lazim
- Ricardo Huang Wei Di
- Pakaporn (Zoe) Leetrairong

## The question

StockTwits is a social media platform like X/Twitter, but only for investors. Users write short comments about stocks and can tag them **Bullish** (optimistic) or **Bearish** (pessimistic).

We wanted to know: **if people comment more about Apple (AAPL) today, is more Apple stock traded tomorrow?**

- **Why volume and not price?** If comments could predict the price, traders would use them to make money and the pattern would disappear.
- **Why the next day?** Same-day comments could just be a reaction to trading that is already happening. Looking at the next day makes sure the comments come first.

## Hypotheses

1. When the number of comments about Apple is above its 30-day average, Apple's trading volume is higher than normal the next trading day.
2. The number of comments has a stronger relationship with next-day volume than whether comments are bullish or bearish.

## Data

| Dataset | Source | What we used |
|---|---|---|
| StockTwits comments about Apple | [StockTwits_2020_2022_Raw (Kaggle)](https://www.kaggle.com/datasets/frankcaoyun/stocktwits-2020-2022-raw) | 914,962 comments from 63,822 users, December 31, 2019 to February 27, 2022 (62 CSV files) |
| Apple daily trading data | [Yahoo Finance](https://finance.yahoo.com/quote/AAPL/history), through the [yfinance](https://pypi.org/project/yfinance/) package | Closing price and volume for 543 trading days |
| Earnings dates | [Apple Investor Relations](https://investor.apple.com) | 9 quarterly earnings announcements |

## What we did

1. **Combined 62 messy files.** They had 14 or 15 columns in different orders, so we kept only the columns all files had in common.
2. **Extracted information from text columns:** sentiment tag, likes, replies, user ID and followers.
3. **Converted timestamps** from UTC to New York time.
4. **Assigned each comment a session date**, meaning the first trading day it could affect. Comments posted after 4pm, on weekends or on holidays were moved to the next trading day. 47% of comments were posted while the market was closed.
5. **Built one row per trading day** with the number of comments, bullish share and Apple's volume.
6. **Compared each day with the average of the 30 trading days before it** (1.0 = a usual day), so days from different periods are comparable.

## Key results

- **Both hypotheses are supported.**
- After days with more comments than usual, next-day trading volume was **15 to 23% above normal**.
- The number of comments (**r = 0.34**) is more strongly related to next-day volume than bullish or bearish sentiment (**r = −0.16**). The correlation is statistically significant (p < 0.05).
- Comments and volume are most closely linked **on the same day** (r = 0.65), so comments mostly react to trading, with some signal left for tomorrow.
- During the **COVID crash** (February 20 to April 7, 2020), the bullish share fell from 71% to 44%, while the number of comments barely changed.
- The **day after earnings**, comments rise to 4 to 6 times their level of the previous five days.
- After the biggest volume spikes, volume and comments return close to normal within about **3 days**.

**Limits:** we studied only Apple from 2020 to 2022, the results show association and not causation, and we did not test whether comments add information beyond today's trading volume. Comments work as an early warning, not as an exact forecast.

## Repository contents

| File | Description |
|---|---|
| `B08_Talking_Before_Trading_StockTwits_and_AAPL.ipynb` | Main notebook: data cleaning, analysis, charts and conclusions |
| `B08_Talking_Before_Trading_StockTwits_and_AAPL.pptx` | Final presentation |
| Release `v1` → `stocktwits.zip` | The 62 StockTwits CSV files (about 1.2 GB) |

## How to run

1. Open the notebook in [Google Colab](https://colab.research.google.com/).
2. Go to **Runtime → Run all**.
3. The notebook downloads the StockTwits files from this repository's release and Apple's data from Yahoo Finance automatically. No manual download is needed.

Main libraries: `pandas`, `matplotlib`, `seaborn`, `yfinance`.

## References

- [StockTwits_2020_2022_Raw Data Set, Kaggle](https://www.kaggle.com/datasets/frankcaoyun/stocktwits-2020-2022-raw)
- [Apple Inc. (AAPL) Historical Data, Yahoo Finance](https://finance.yahoo.com/quote/AAPL/history)
- [Liz Frazier, "The Coronavirus Crash Of 2020, And The Investing Lesson It Taught Us", Forbes, February 11, 2021](https://www.forbes.com/sites/lizfrazierpeck/2021/02/11/the-coronavirus-crash-of-2020-and-the-investing-lesson-it-taught-us/)
- [Mohammad Soltanieh-ha, "BA780 - Introduction to Data Analytics", Colab Notebooks, Fall 2026](https://github.com/soltaniehha/Intro-to-Data-Analytics)

## Generative AI disclosure

We used Claude (Anthropic) as a coding and writing assistant. Details are in the last section of the notebook.
