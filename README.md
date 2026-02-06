# Trading Sentiment Analysis


##  What This Notebook Does

1. **Loads your datasets**:
   - `fear_greed_index.csv` - Market sentiment data (Fear/Greed)
   - `historical_data.csv` - Your trading history

2. **Joins them by date**:
   - Extracts date from `Timestamp IST` in trading data
   - Matches with `date` column in sentiment data
   - Creates a unified dataset

3. **Calculates required metrics**:
   -  **Trade Frequency**: Number of trades per day
   -  **Position Sizes**: Average, median, total volume (USD and tokens)
   -  **Long/Short Bias**: 
     - Buy vs Sell trade counts
     - Buy vs Sell volume
     - Long/Short ratios
     - Net position bias
     - Buy percentage
   -  **Leverage**: Estimated leverage factor (based on position sizes)
   -  **PnL Metrics**: Daily profit/loss, per-trade averages
   -  **Other Metrics**: Fees, execution prices, position tracking


### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn openpyxl
```

### Steps

1. **Place your data files** in the same directory as the notebook:
   ```
   your-folder/
   ├── primetrade_analysis.ipynb
   ├── fear_greed_index.csv
   └── historical_data.csv
   ```

2. **Open Jupyter**:
   ```bash
   jupyter notebook primetrade_analysis.ipynb
   ```

3. **Run all cells** (Cell → Run All)

## Generated Outputs

The notebook will create:

1. **merged_trading_sentiment_data.csv** - Complete dataset with all metrics
2. **sentiment_summary_statistics.csv** - Aggregated stats by sentiment
3. **data_dictionary.csv** - Explanation of all columns
4. **trading_metrics_by_sentiment.png** - 6 key visualizations
5. **time_series_analysis.png** - Trends over time


### Trade Frequency
- **trade_frequency**: Number of trades executed each day

### Position Sizes
- **avg_position_size_usd**: Average trade size in USD
- **median_position_size_usd**: Median trade size (less affected by outliers)
- **total_volume_usd**: Total USD traded per day
- **position_size_std_usd**: Volatility of position sizes

### Long/Short Bias
- **buy_trades**: Count of BUY orders
- **sell_trades**: Count of SELL orders
- **long_short_ratio_count**: Buy trades ÷ Sell trades
- **long_short_ratio_volume**: Buy volume ÷ Sell volume
- **buy_percentage**: % of trades that are buys
- **net_volume_usd**: Buy volume - Sell volume

### Leverage (Estimated)
- **implied_leverage_factor**: Estimated based on position size variation
  - Higher values = more aggressive position sizing
  - Note: Real leverage would come from exchange data

### PnL
- **daily_pnl**: Total profit/loss for the day
- **avg_pnl_per_trade**: Average P&L per trade

## Data Structure

### Input: Trading Data
```
Columns: Execution Price, Size Tokens, Size USD, Side, Timestamp IST, 
         Start Position, Direction, Closed PnL, Fee, ...
```

### Input: Sentiment Data
```
Columns: timestamp, value (0-100), classification (Fear/Greed), date
```

### Output: Merged Dataset
```
Columns (32 total):
- date
- Trade metrics (frequency, sizes, volumes)
- Long/Short bias (ratios, counts, percentages)  
- PnL metrics (daily, per-trade)
- Leverage metrics (estimated)
- Sentiment data (value, category)
```

##  Important Notes

### About Leverage
The notebook calculates an **estimated leverage factor** because the example trading data doesn't have a direct leverage column. This is calculated as:

```
implied_leverage_factor = max_position_size / avg_position_size
```

Higher values suggest more aggressive position sizing relative to typical trades.



### Date Matching
- Sentiment data: Daily values (one per day)
- Trading data: Multiple trades per day
- Join: Aggregates all trades for each day, then matches with that day's sentiment


---

**Last Updated**: February 2026  
**Notebook Version**: 1.0 (Simplified)
