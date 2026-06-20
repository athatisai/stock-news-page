# 🌍 Hermes 美股市場情報中心

> **自動更新時間**: 
**自動更新時間**: 2026-06-20 23:51:48
> **數據來源**: 自动化 Cron Jobs (新聞/掃描/技術分析)
> **聲明**: 本頁面僅供市場情報參考，不構成投資建議。

---

## 📰 1. 美股開市前盤前快報
*(每日 21:00 更新)*

✅ 找到報告：2026-06-11_21-10-20.md

**Job ID:** a550048bd0df
**Run Time:** 2026-06-11 21:10:20
**Schedule:** 0 21 * * 1-5

## Prompt

[IMPORTANT: You are running as a scheduled cron job. DELIVERY: Your final response will be automatically delivered to the user — do NOT use send_message or try to deliver the output yourself. Just produce your report/output as your final response and the system handles the rest. SILENT: If there is genuinely nothing new to report, respond with exactly "[SILENT]" (nothing else) to suppress delivery. Never combine [SILENT] with content — either report your findings normally, or say [SILENT] and nothing more.]

你係美股盤前快報生成器。現在係美股開市前，執行以下步驟：

1. 用 terminal + curl 抓取以下股票的盤前數據和最新新聞：SNDK, MU, SOXL, TSLA, APP, NOW, CAT, AMAT, NOK, ALAB
   - 使用 Yahoo Finance Chart API: https://query1.finance.yahoo.com/v8/finance/chart/{ticker}?range=1d&interval=5m
   - 用 curl + python3 -c 處理（唔好用 execute_code + urllib.request，會被 security scan 阻擋）
   - 取得 price, previousClose, change, changePercent, volume
   - 計算 MA20, MA50, RSI(14)（用 3mo daily 數據）

2. 同時抓取今日焦點新聞（用 Yahoo Finance search API）：
   https://query1.finance.yahoo.com/v1/finance/search?q={ticker}&quotesCount=0&newsCount=3&listsCount=0

3. 也抓取 S&P 500 / NASDAQ / Dow Jones 的指數期貨盤前數據（用 ^GSPC ^IXIC ^DJI）

4. 用以下格式生成粵語盤前快報（Cantonese Chinese），唔好用 markdown tables：

**🌅 美股盤前快報**
日期和時間

**📊 指數期貨**
（列出 S&P 500, NASDAQ, Dow 的盤前數字和變化）

**📌 持倉股票盤前動態**
每隻用以下格式：
📈/📉 **TICKER** (Name)
💰 盤前: $PRICE | 📈/📉 $CHANGE (CH%)
📐 MA20: $XX | MA50: $XX | RSI: XX
💡 分析: [粵語分析]

**🔥 今日焦點**
列出 3-5 條最重要新聞（可能影響今日走勢的）


---

## 📉 2. 美股收市全日報告
*(每日 07:00 更新)*

✅ 找到報告：2026-06-12_21-06-55.md

**Job ID:** a550048bd0df
**Run Time:** 2026-06-12 21:06:55
**Schedule:** 0 21 * * 1-5

## Prompt

[IMPORTANT: You are running as a scheduled cron job. DELIVERY: Your final response will be automatically delivered to the user — do NOT use send_message or try to deliver the output yourself. Just produce your report/output as your final response and the system handles the rest. SILENT: If there is genuinely nothing new to report, respond with exactly "[SILENT]" (nothing else) to suppress delivery. Never combine [SILENT] with content — either report your findings normally, or say [SILENT] and nothing more.]

你係美股盤前快報生成器。現在係美股開市前，執行以下步驟：

1. 用 terminal + curl 抓取以下股票的盤前數據和最新新聞：SNDK, MU, SOXL, TSLA, APP, NOW, CAT, AMAT, NOK, ALAB
   - 使用 Yahoo Finance Chart API: https://query1.finance.yahoo.com/v8/finance/chart/{ticker}?range=1d&interval=5m
   - 用 curl + python3 -c 處理（唔好用 execute_code + urllib.request，會被 security scan 阻擋）
   - 取得 price, previousClose, change, changePercent, volume
   - 計算 MA20, MA50, RSI(14)（用 3mo daily 數據）

2. 同時抓取今日焦點新聞（用 Yahoo Finance search API）：
   https://query1.finance.yahoo.com/v1/finance/search?q={ticker}&quotesCount=0&newsCount=3&listsCount=0

3. 也抓取 S&P 500 / NASDAQ / Dow Jones 的指數期貨盤前數據（用 ^GSPC ^IXIC ^DJI）

4. 用以下格式生成粵語盤前快報（Cantonese Chinese），唔好用 markdown tables：

**🌅 美股盤前快報**
日期和時間

**📊 指數期貨**
（列出 S&P 500, NASDAQ, Dow 的盤前數字和變化）

**📌 持倉股票盤前動態**
每隻用以下格式：
📈/📉 **TICKER** (Name)
💰 盤前: $PRICE | 📈/📉 $CHANGE (CH%)
📐 MA20: $XX | MA50: $XX | RSI: XX
💡 分析: [粵語分析]

**🔥 今日焦點**
列出 3-5 條最重要新聞（可能影響今日走勢的）


---

## 🎯 3. 每日 Sell Put 掃描 (TSLA/MU/SOXL)
*(每日 06:00 更新)*

✅ 找到報告：2026-06-19_06-40-58.md

**Job ID:** 2d2fea4f4e46
**Run Time:** 2026-06-19 06:40:58
**Schedule:** 0 6 * * 1-5

## Prompt

[IMPORTANT: You are running as a scheduled cron job. DELIVERY: Your final response will be automatically delivered to the user — do NOT use send_message or try to deliver the output yourself. Just produce your report/output as your final response and the system handles the rest. SILENT: If there is genuinely nothing new to report, respond with exactly "[SILENT]" (nothing else) to suppress delivery. Never combine [SILENT] with content — either report your findings normally, or say [SILENT] and nothing more.]

你係 Sell Put 同 Spread 交易掃描器。任務：為 TSLA、MU、SOXL、SNDK、APP、NOW、CAT、AMAT、NOK、ALAB 計算 Sell Put 同 Spread 入場評分，同時掃描全市場機會。

**⚠️ 全部用 terminal + curl，唔好用 execute_code**

步驟：
1. 用 curl 抓取各股票即時價格（Yahoo Finance API）
2. 計算每隻股票嘅 Sell Put 評分（0-100）：
   - RSI < 30: +30分
   - RSI 30-40: +20分
   - 價格跌破 MA20: +15分
   - 價格跌破 MA50: +10分
   - MACD 紅柱縮短: +10分
   - 成交量放大: +10分
   - IV Rank > 50%: +15分
3. 掃描全市場（S&P 500 成份股）搵 IV Rank > 60% 嘅股票
4. 評分 > 60 嘅股票發出 Sell Put 信號
5. 評分 > 40 嘅股票發出 Bull Put Spread 信號

錯誤處理：
- 如果 curl 失敗，重試最多 3 次，每次間隔 10 秒
- 如果某隻股票數據唔完整，跳過佢但繼續處理其他
- 如果連續 3 次失敗，用緩存嘅最後一次有效數據
- 記錄所有錯誤日誌到 /tmp/cron_error.log

輸出格式：
📊 每日 Sell Put 掃描報告
日期：YYYY-MM-DD

🟢 Sell Put 機會（評分 > 60）：
- 股票 | 價格 | RSI | 評分 | 建議行權價 | Delta | IV


---

## 🔍 4. 全市場 Sell Put 機會掃描
*(每日 08:00 更新)*

✅ 找到報告：2026-06-19_06-40-58.md

**Job ID:** 2d2fea4f4e46
**Run Time:** 2026-06-19 06:40:58
**Schedule:** 0 6 * * 1-5

## Prompt

[IMPORTANT: You are running as a scheduled cron job. DELIVERY: Your final response will be automatically delivered to the user — do NOT use send_message or try to deliver the output yourself. Just produce your report/output as your final response and the system handles the rest. SILENT: If there is genuinely nothing new to report, respond with exactly "[SILENT]" (nothing else) to suppress delivery. Never combine [SILENT] with content — either report your findings normally, or say [SILENT] and nothing more.]

你係 Sell Put 同 Spread 交易掃描器。任務：為 TSLA、MU、SOXL、SNDK、APP、NOW、CAT、AMAT、NOK、ALAB 計算 Sell Put 同 Spread 入場評分，同時掃描全市場機會。

**⚠️ 全部用 terminal + curl，唔好用 execute_code**

步驟：
1. 用 curl 抓取各股票即時價格（Yahoo Finance API）
2. 計算每隻股票嘅 Sell Put 評分（0-100）：
   - RSI < 30: +30分
   - RSI 30-40: +20分
   - 價格跌破 MA20: +15分
   - 價格跌破 MA50: +10分
   - MACD 紅柱縮短: +10分
   - 成交量放大: +10分
   - IV Rank > 50%: +15分
3. 掃描全市場（S&P 500 成份股）搵 IV Rank > 60% 嘅股票
4. 評分 > 60 嘅股票發出 Sell Put 信號
5. 評分 > 40 嘅股票發出 Bull Put Spread 信號

錯誤處理：
- 如果 curl 失敗，重試最多 3 次，每次間隔 10 秒
- 如果某隻股票數據唔完整，跳過佢但繼續處理其他
- 如果連續 3 次失敗，用緩存嘅最後一次有效數據
- 記錄所有錯誤日誌到 /tmp/cron_error.log

輸出格式：
📊 每日 Sell Put 掃描報告
日期：YYYY-MM-DD

🟢 Sell Put 機會（評分 > 60）：
- 股票 | 價格 | RSI | 評分 | 建議行權價 | Delta | IV


---

## 📊 5. TSLA/MU/SOXL 技術指標監控
*(每 2 小時更新)*

✅ 找到報告：2026-06-18_06-54-38.md

**Job ID:** 2d2fea4f4e46
**Run Time:** 2026-06-18 06:54:38
**Schedule:** 0 6 * * 1-5

## Prompt

[IMPORTANT: You are running as a scheduled cron job. DELIVERY: Your final response will be automatically delivered to the user — do NOT use send_message or try to deliver the output yourself. Just produce your report/output as your final response and the system handles the rest. SILENT: If there is genuinely nothing new to report, respond with exactly "[SILENT]" (nothing else) to suppress delivery. Never combine [SILENT] with content — either report your findings normally, or say [SILENT] and nothing more.]

你係 Sell Put 同 Spread 交易掃描器。任務：為 TSLA、MU、SOXL、SNDK、APP、NOW、CAT、AMAT、NOK、ALAB 計算 Sell Put 同 Spread 入場評分，同時掃描全市場機會。

**⚠️ 全部用 terminal + curl，唔好用 execute_code**

步驟：
1. 用 curl 抓取各股票即時價格（Yahoo Finance API）
2. 計算每隻股票嘅 Sell Put 評分（0-100）：
   - RSI < 30: +30分
   - RSI 30-40: +20分
   - 價格跌破 MA20: +15分
   - 價格跌破 MA50: +10分
   - MACD 紅柱縮短: +10分
   - 成交量放大: +10分
   - IV Rank > 50%: +15分
3. 掃描全市場（S&P 500 成份股）搵 IV Rank > 60% 嘅股票
4. 評分 > 60 嘅股票發出 Sell Put 信號
5. 評分 > 40 嘅股票發出 Bull Put Spread 信號

錯誤處理：
- 如果 curl 失敗，重試最多 3 次，每次間隔 10 秒
- 如果某隻股票數據唔完整，跳過佢但繼續處理其他
- 如果連續 3 次失敗，用緩存嘅最後一次有效數據
- 記錄所有錯誤日誌到 /tmp/cron_error.log

輸出格式：
📊 每日 Sell Put 掃描報告
日期：YYYY-MM-DD

🟢 Sell Put 機會（評分 > 60）：
- 股票 | 價格 | RSI | 評分 | 建議行權價 | Delta | IV


---

## ⚙️ 自動化監控狀態

| 情報來源 | 運行狀態 | 下次更新 |
|----------|----------|----------|
| 盤前快報 | 🟢 運行中 | 週一至五 21:00 |
| 收市報告 | 🟢 運行中 | 週二至六 07:00 |
| Sell Put 掃描 (個股) | 🟢 運行中 | 週一至五 06:00 |
| Sell Put 掃描 (全市場) | 🟢 運行中 | 週一至五 08:00 |
| 技術指標監控 | 🟡 需檢查 | 每 2 小時 |

> 💡 **提示**: 如果看到「暫無數據」，代表對應嘅 Cron Job 尚未運行或未生成新報告。
> 由於報告係自動生成，內容可能較長，此處僅顯示摘要。完整報告請查看 Hermes 歷史訊息或 Cron 輸出目錄。

---
🚀 **Hermes 市場情報系統運行中**
