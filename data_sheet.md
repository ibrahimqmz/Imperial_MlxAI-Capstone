# Gold Trading Dataset Datasheet

## Motivation

### Purpose
This dataset was created for the development and evaluation of an automated gold trading system, designed to predict short-term movements in the gold market.

### Creator 
- **Data Provider**: Alpha Vantage – a leading provider of financial market data APIs  

## Composition

### Data Instances
Each instance represents a single one-minute price bar from gold market trading data.

### Volume and Distribution
- **Total samples**: 19,067 one-minute bars  
  - **Training set**: 13,337 samples (70%)  
  - **Validation set**: 2,858 samples (15%)  
  - **Test set**: 2,859 samples (15%)

### Data Structure
Each instance includes:
- OHLCV data (Open, High, Low, Close, Volume)
- 18 derived technical indicators
- A binary target variable indicating short-term price direction

### Data Quality
- Minor missing data during non-trading periods (e.g. holidays and market closures)
- No personal or confidential data; all information is sourced from publicly available financial markets

## Collection Process

### Data Acquisition
- **Method**: Programmatic collection via Alpha Vantage API  
- **API Key Used**: `Access via https://www.alphavantage.co/support/#api-key`  
- **Ticker Symbol**: `GLD` (SPDR Gold ETF)

### Sampling Strategy
- **Frequency**: 1-minute intervals  
- **Scope**: Market hours only, updated continuously in real time  
- **Timeframe**: Recent historical data from an active gold market period

## Preprocessing, Cleaning and Labelling

### Preprocessing Steps
1. Computation of 18 technical indicators based on OHLCV inputs
2. Standard scaling applied to all numerical features
3. Target variable generated as a binary label (1 if price increases in the next 5 minutes, else 0)
4. NaN values removed or imputed where required (mainly from rolling indicators)
5. Time-series aware data splitting for validation and testing to avoid leakage

### Feature Engineering

- **Price-Based Features**:  
  - Net price change  
  - Candle body size  
  - Upper and lower shadow lengths  
  - Daily and intraday price ranges  

- **Technical Indicators** (selected examples):  
  - Simple and Exponential Moving Averages  
  - Relative Strength Index (RSI)  
  - Moving Average Convergence Divergence (MACD)  
  - Bollinger Bands and other volatility-based indicators  

- **Volume-Based Indicators**:  
  - Volume Price Trend (VPT)  
  - On-Balance Volume (OBV)

### Raw Data Preservation
The original OHLCV data is retained unaltered prior to feature engineering and model training.

## Uses

### Potential Applications
- Short-term gold price forecasting
- Market microstructure analysis
- Trading strategy backtesting and optimisation
- Volatility and risk modelling

### Usage Considerations
- Forecasting models trained on this data should be regularly retrained to adapt to changing market conditions
- This dataset does not include news, macroeconomic indicators or order book data
- Latency and API rate limits should be considered for real-time deployment

### Limitations and Restrictions
This dataset is **not suitable** for:
- Long-term investment strategy modelling
- High-frequency trading systems (due to API constraints)
- Sole use in financial decision-making without broader context

## Distribution

### Access Information
- Accessible via the Alpha Vantage API (https://www.alphavantage.co/)
- Requires a free or paid API key
- Subject to request rate limits based on account level

### Licensing and Terms
- Usage subject to Alpha Vantage’s Terms of Service
- Redistribution of raw data may be restricted; users should consult Alpha Vantage’s API documentation

## Maintenance

### Ongoing Maintenance
- **Maintainer**: Alpha Vantage  
- **Update Frequency**: Real-time updates during market hours  
- **Validation**: Data quality and integrity are managed by Alpha Vantage’s internal systems  
- **Support**: Users can contact Alpha Vantage via their support portal or email for assistance
