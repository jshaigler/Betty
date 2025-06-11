# Betty

A comprehensive machine learning system for predicting stock prices using technical indicators, fundamental analysis, sentiment analysis, and macroeconomic factors.

## Overview

This system uses a Decision Tree Regressor to predict stock prices 1-24 months into the future by analyzing multiple data sources including:

- **Technical Indicators**: Moving averages, RSI, Bollinger Bands, volume analysis
- **Fundamental Analysis**: P/E ratios, quarterly financial metrics, sector comparisons
- **Sentiment Analysis**: News sentiment and political news sentiment
- **Macroeconomic Factors**: Treasury rates, yield curve analysis, insider trading data

## Features

### Multi-Factor Analysis
- **Technical Indicators**: SMA (20, 50, 200), RSI, Bollinger Bands, Volume patterns
- **Fundamental Metrics**: P/E ratios, revenue/earnings growth, profit margins
- **Sentiment Analysis**: News sentiment scoring using TextBlob
- **Macro Factors**: Treasury yields, interest rates, yield curve spreads
- **Insider Trading**: Net insider trading activity analysis

### Visualization
- Feature importance analysis with grouped categories
- Historical price charts with predictions
- Performance metrics and model scoring

### User-Friendly Interface
- Interactive input for stock tickers and prediction timeframes
- Support for multiple stocks in a single run
- Comprehensive error handling and progress reporting

## Installation

### Required Libraries

```bash
pip install pandas numpy scikit-learn matplotlib seaborn yfinance joblib textblob requests
```

### Additional Dependencies

The system uses several specialized libraries:
- `newsi` - For political news sentiment analysis
- `yfinance` - For stock data and financial information
- `textblob` - For natural language processing and sentiment analysis

## Usage

### Basic Usage

1. Run the script:
```bash
python stock_prediction.py
```

2. Enter stock tickers when prompted (comma-separated):
```
Enter stock tickers separated by commas (e.g., AAPL,MSFT,GOOGL):
AAPL,MSFT,TSLA
```

3. Choose prediction timeframe (1-24 months):
```
Enter the number of months to predict forward (1-24):
6
```

### Input Format
- **Stock Tickers**: Use standard ticker symbols (AAPL, MSFT, GOOGL, etc.)
- **Prediction Period**: 1-24 months (converted to trading days internally)
- **Multiple Stocks**: Separate tickers with commas

## System Architecture

### Data Collection Pipeline

1. **Stock Data**: Historical OHLCV data from Yahoo Finance
2. **Fundamental Data**: Quarterly financials, P/E ratios, sector information
3. **News Sentiment**: Recent news articles processed through TextBlob
4. **Political Sentiment**: Political news analysis using newsi library
5. **Insider Trading**: Net insider trading activity from SEC filings
6. **Treasury Data**: Current interest rates and yield curve data

### Feature Engineering

The system creates 23+ features across 5 categories:

#### Essential Features (5)
- Open, High, Low, Close, Volume

#### Technical Features (11)
- Simple Moving Averages (20, 50, 200 day)
- Relative Strength Index (RSI)
- Bollinger Bands (upper, middle, lower)
- Volume moving average
- News sentiment score
- Political news sentiment
- Insider trading ratio

#### Fundamental Features (12)
- P/E ratio and forward P/E
- P/E relative to sector average
- Revenue and earnings growth rates
- Profit margins (gross, operating, net)
- Treasury rates (short-term, 2Y, 10Y)
- Yield curve spread

### Machine Learning Model

- **Algorithm**: Decision Tree Regressor
- **Sequence Length**: 60 trading days
- **Scaling**: MinMaxScaler normalization
- **Validation**: 80/20 train-test split
- **Performance Metrics**: R² scores for training and testing

## Output Information

For each stock analyzed, the system provides:

### Performance Metrics
- Training R² Score
- Testing R² Score
- Current vs. predicted price comparison
- Percentage change prediction

### Visualizations
1. **Feature Importance Chart**: Shows which factors most influence predictions
2. **Price History & Prediction**: Historical prices with future prediction point
3. **Grouped Feature Analysis**: Features categorized by type (technical, fundamental, macro)

### Example Output
```
Processing AAPL...

Model Performance for AAPL:
Training R² Score: 0.8542
Testing R² Score: 0.7321

Current price for AAPL: $175.25
Predicted price in 6 months: $189.50
Predicted change: +8.13%
```

## Data Sources

- **Yahoo Finance**: Primary source for stock data, fundamentals, and news
- **Treasury Data**: Federal Reserve economic data via Yahoo Finance tickers
- **News APIs**: Multiple sources for sentiment analysis
- **SEC Filings**: Insider trading information

## Limitations and Considerations

### Model Limitations
- Decision trees can overfit to training data
- Predictions become less reliable for longer time horizons
- Market volatility can make predictions uncertain

### Data Limitations
- News sentiment analysis may not capture all market factors
- Some fundamental data may have reporting delays
- Treasury rate proxies may not reflect exact federal policy

### Market Factors Not Included
- Geopolitical events
- Black swan events
- Regulatory changes
- Competitor actions

## Error Handling

The system includes comprehensive error handling for:
- Invalid ticker symbols
- Missing financial data
- Network connectivity issues
- Data processing errors
- Model training failures

## Customization Options

### Model Parameters
- Adjust `max_depth` in DecisionTreeRegressor for complexity control
- Modify `sequence_length` for different historical context windows
- Change `test_size` for different train/validation splits

### Feature Selection
- Add or remove features from the feature lists
- Implement additional technical indicators
- Include additional fundamental metrics

### Visualization
- Customize chart colors and styles
- Modify plot sizes and layouts
- Add additional performance metrics

## Best Practices

1. **Data Quality**: Ensure sufficient historical data (recommended: 2+ years)
2. **Multiple Timeframes**: Test different prediction windows
3. **Portfolio Analysis**: Analyze multiple stocks for diversification insights
4. **Regular Updates**: Re-run analysis periodically as new data becomes available
5. **Risk Management**: Use predictions as one factor among many in investment decisions

## Disclaimer

This system is for educational and research purposes only. Stock market predictions are inherently uncertain, and past performance does not guarantee future results. Always consult with financial professionals before making investment decisions.

## Contributing

To extend this system:
1. Add new data sources in the data collection functions
2. Implement additional technical indicators
3. Experiment with different machine learning algorithms
4. Enhance visualization capabilities
5. Add more comprehensive error handling

## License

This project is provided as-is for educational purposes. Please ensure compliance with data provider terms of service when using financial data APIs.
