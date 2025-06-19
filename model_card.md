# Gold Trading Model Card

## Model Description

### Input
- **Price Features**:
  - OHLCV (Open, High, Low, Close, Volume) data
  - Price changes and body sizes
  - Upper/lower shadows
  - Price ranges and typical prices

- **Technical Indicators**:
  - Moving Averages (5, 10, 20, 50 periods)
  - RSI (14 periods)
  - MACD (12, 26, 9)
  - Price acceleration
  - Rolling volatility
  - Volume price trends

### Output
- Binary classification (1: Price will increase, 0: Price will decrease)
- Prediction confidence score (0-1)
- Recommended position size based on confidence

### Model Architecture
**Ensemble Model combining:**
1. Random Forest Classifier
   - n_estimators: 100
   - min_samples_split: 50
   - min_samples_leaf: 30
   - max_features: sqrt
   - max_depth: 5

2. Gradient Boosting Classifier
   - Optimized hyperparameters through grid search
   - Learning rate: 0.01-0.1
   - Max depth: 3-5
   - Min samples split: 50-100
   - Subsample: 0.7-0.9

## Performance

### Classification Metrics
- ROC AUC Score: 0.6576
- Average Prediction Confidence: 50.04%

### Trading Performance
- Win Rate: 63.93%
- Average P&L per Trade: $140.89
- Sharpe Ratio: 1.73

### Risk Metrics (Monte Carlo Simulation)
- Mean return: -0.08%
- Median return: -0.16%
- Standard deviation: 2.44%
- 95% VaR: -4.15%
- 99% VaR: -5.74%
- Average maximum drawdown: 2.97%
- Worst maximum drawdown: 9.13%

### Feature Importance
![Feature Importance Graph]
Top contributing features:
1. Close price
2. RSI
3. MACD
4. MACD_Histogram
5. Price_Change_Pct

## Limitations

### Technical Limitations
- Requires minimum 5-minute intervals between trades
- Limited to regular market hours
- API rate limits restrict high-frequency predictions
- Requires stable internet connection for real-time data

### Market Limitations
- Model performance degrades in highly volatile markets
- Not designed for overnight positions
- Limited to gold trading only
- Does not account for:
  - Market sentiment
  - News events
  - Macroeconomic factors
  - Geopolitical events

### Data Limitations
- Training data may not represent all market conditions
- Historical patterns may not repeat
- Limited to recent market data
- Dependent on data provider uptime

## Trade-offs

### Speed vs Accuracy
- Faster prediction times achieved by limiting feature complexity
- Real-time processing requirements restrict model complexity
- Simple ensemble approach chosen over deep learning for interpretability

### Risk vs Return
- Conservative position sizing reduces potential profits
- Strict risk management may miss some profitable opportunities
- Higher confidence threshold (0.6) reduces trade frequency but improves quality

### Resource Usage
- CPU-optimized implementation sacrifices some accuracy
- Memory usage optimized for standard hardware
- Batch processing of features balances efficiency with latency

### Maintenance Requirements
- Regular retraining needed (every 3 months)
- Feature engineering pipeline needs monitoring
- Risk parameters require periodic adjustment