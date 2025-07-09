# 📊 Crypto Trade Analysis with Sentiment Data

This project analyzes detailed trade data alongside market sentiment. Each row in the trade dataset represents an individual transaction, enriched with information like execution price, trade direction, profit/loss, and timestamps. The goal is to merge this trade data with sentiment indicators (like the Bitcoin Fear & Greed Index) for deeper behavioral insights.

---

## 📁 Dataset Description

Each row contains:

- **Execution Price**: Price at which trade was executed.
- **Size USD**: Total trade value in USD.
- **Side**: Trade direction (`BUY` or `SELL`).
- **Timestamp IST**: When the trade occurred (format: `DD-MM-YYYY HH:MM`).
- **Closed PnL**: Profit or loss upon trade closure.
- **Fee**: Transaction cost.
- **Start Position**: Position value at the beginning of the trade.
- Plus other identifiers (Transaction Hash, Order ID, etc.)

> 🔁 We will convert the timestamp to `datetime` format and extract the `date` field to join with sentiment data.

---

## ⚙️ Setup Instructions

### 1. Clone the Repo / Upload Files
Make sure you have your trade CSV and sentiment CSV (e.g., Fear & Greed Index) ready in your workspace.

### 2. Environment Requirements

Use Python 3.8+ with:

```bash
pip install pandas matplotlib seaborn
```

If using Google Colab:

```python
from google.colab import drive
drive.mount('/content/drive')
```

### 3. Load the Data

```python
import pandas as pd

# Load trade data
df_trades = pd.read_csv('your_trade_data.csv')

# Convert timestamp to datetime and extract date
df_trades['Timestamp IST'] = pd.to_datetime(df_trades['Timestamp IST'], format='%d-%m-%Y %H:%M')
df_trades['Date'] = df_trades['Timestamp IST'].dt.date
```

---

## 🧠 Sentiment Data Integration

1. Load the sentiment CSV (e.g., Fear & Greed Index):

```python
df_sentiment = pd.read_csv('fear_greed_index.csv')

# Convert date if necessary
df_sentiment['Date'] = pd.to_datetime(df_sentiment['Date']).dt.date
```

2. Merge trade data with sentiment on `Date`:

```python
merged_df = pd.merge(df_trades, df_sentiment, on='Date', how='left')
```

---

## 📈 Analysis Ideas

- Analyze average PnL on high vs low sentiment days
- Compare BUY vs SELL behavior based on market sentiment
- Visualize execution price trends vs fear/greed scores
- Correlate trade frequency with daily sentiment shifts

---

## 📝 Notes

- Ensure all timestamps are in IST and cleanly formatted.
- Missing sentiment values may appear for non-trading days—handle accordingly.
- You can use Matplotlib or Seaborn for plotting behavior insights.

---

## ✅ Example Output

- 📌 Trendline: Execution Price vs Sentiment Index  
- 📌 Histogram: PnL distribution by Trade Side  
- 📌 Heatmap: Trade volume across Time of Day vs Sentiment Score

---

## 📬 Contact

Feel free to reach out for suggestions, issues, or collaborations!