# 🕯️ Hermes 美股市場情報生成器 (V5 陰陽燭專業版)

> **版本**: 5.0.0 | **類別**: 金融/自動化 | **作者**: Moss Li & Hermes Agent

---

## 📖 技能介紹

本技能 (Skill) 用於生成 **專業級別嘅美股市場情報報告**，包含以下豪華功能：

- 🕯️ **正宗陰陽燭圖表** (Candlestick Chart)：60 日走勢，清晰展示開高低收。
- 📊 **技術指標集成**：MA50/200、布林帶 (Bollinger Bands)、RSI、MACD。
- 🎯 **自動支撐/阻力位**：算法自動識別關鍵價位並喺圖表標註。
- 🔥 **成交量分析**：自動標註 **放量** (🔥) / **縮量** (💤) / **正常** (💧)。
- 📰 **真實新聞抓取**：整合 Google News 相關 headlines。
- 📢 **Telegram 自動通知**：報告生成後即時發送摘要去你手機。
- 📁 **歷史數據庫**：自動建立 `reports/` 資料夾，保留所有歷史報告。

---

## ⚙️ 前置設定

使用前請確保已完成以下設定：

### 1. 環境變數 (.env)
請在 `~/.hermes/.env` 中加入：

```bash
# GitHub 發布用 (必需)
GITHUB_PERSONAL_ACCESS_TOKEN=*** Telegram 通知用 (可選，如無設定會跳過通知)
TELEGRAM_BOT_TOKEN=你的BotT...atID (例如: 1082397901)
```

### 2. 安裝 Python 依賴
本技能需要 `matplotlib` 同 `pandas`。如未安裝，首次運行會自動安裝，或手動執行：
```bash
pip install matplotlib pandas
```

### 3. GitHub 倉庫
確保你有一個已開啟 **GitHub Pages** 嘅倉庫 (例如：`athatisai/stock-news-page`)。
技能會自動 Clone 並推送，無需手動建立結構。

---

## 🚀 使用方法

### 方法 A: 手動觸發 (透過 Hermes 對話)
隨時同 Hermes 講：
> **「幫我生成今日嘅市場情報報告」**

Hermes 會載入本技能並即時執行。

### 方法 B: 全自動化 (Cron Job)
建議設定為 **每日收市後** 自動運行：
- **時間**：週一至五 早上 07:00 (美股收市後)
- **指令**：
  ```bash
  0 7 * * 1-5 cd /home/upsn150 && /usr/bin/python3 ~/.hermes/skills/finance/market-intelligence/scripts/generate_report.py
  ```

---

## 📊 報告內容預覽

執行後會自動喺你嘅 GitHub 倉庫建立以下結構：

```
stock-news-page/
├── index.md              # 首頁摘要 (含最新數據表格)
├── docs/                 # 說明文件
│   └── skill-intro.md    # 本介紹頁面
├── reports/              # 歷史報告資料夾
│   └── 2026-06-21.md     # 每日報告 (含陰陽燭圖)
└── charts/               # 圖表圖片庫
    ├── TSLA.png
    ├── NVDA.png
    └── ...
```

### 首頁 (`index.md`) 包含：
- **最新數據表格**：價格、漲跌%、RSI、成交量狀態。
- **歷史報告連結**：按日期排序，方便翻查。
- **系統狀態**：顯示自動化運行狀態。

### 每日報告 (`reports/YYYY-MM-DD.md`) 包含：
- **核心數據總覽表**。
- **個股陰陽燭分析**：每隻股票一張圖，含支撐/阻力線。
- **技術指標解讀**：RSI 超買/超賣、MACD 信號。
- **相关新闻連結**。

---

## 💡 常見問題 (FAQ)

### Q1: 點解圖表有 `Glyph missing` 警告？
A: 呢個係因為 matplotlib 默認字體唔支援中文/Emoji，但 **唔影響圖表生成**。紅綠蠟燭、指標線都會正常顯示。

### Q2: 週末/假期點算？
A: 腳本會自動偵測市場狀態。如果係非交易時段，會顯示 **上一個交易日嘅收市數據**，並標註「休市」。

### Q3: Telegram 點解收唔到通知？
A: 請檢查 `.env` 中嘅 `TELEGRAM_BOT_TOKEN` 是否正確填寫。如果無設定，腳本會跳過通知但不影響報告生成。

### Q4: 可以改股票名單嗎？
A: 可以！編輯腳本中嘅 `STOCKS` 列表 (約第 15 行)，加入你想追蹤嘅股票代碼 (例如：`["TSLA", "NVDA", "AAPL"]`)。

---

## 📜 技術細節

- **數據源**: Yahoo Finance API (實時/收市價)。
- **圖表庫**: Matplotlib (專業財經圖表繪製)。
- **數據處理**: Pandas (高效計算 MA, RSI, BB 等指標)。
- **自動化**: Git + GitHub Actions (通過 Hermes Cron Job 驅動)。

---

> 🚀 **Powered by Hermes Agent V5** | [返回首頁](../index.md)
