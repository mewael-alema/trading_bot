# FinBERT Trading Bot

A machine learning-powered algorithmic trading bot that leverages sentiment analysis of financial news to make trading decisions.

## Overview

This trading bot uses the FinBERT model (a financial sentiment analysis model based on BERT) to analyze recent news sentiment related to a specific stock or ETF. Based on the sentiment analysis, the bot makes buy or sell decisions with predefined risk management parameters.

The bot is built using:
- Lumibot for the trading strategy framework
- Alpaca for paper trading and market data
- FinBERT for financial news sentiment analysis
- PyTorch for running the sentiment analysis model

## Features

- Sentiment-based trading strategy using NLP
- Backtesting capabilities using historical data
- Automatic bracket orders with take-profit and stop-loss
- Position sizing based on capital at risk
- Paper trading support via Alpaca

## Project Structure

```
Trading Bot/
├── finbert_utils.py  # Utility functions for sentiment analysis
└── tradingbot.py     # Main trading strategy implementation
```

## Requirements

- Python 3.8+
- PyTorch
- Transformers (Hugging Face)
- Lumibot
- Alpaca Trade API
- Timedelta

## Installation

1. Clone the repository:
```
git clone https://github.com/yourusername/finbert-trading-bot.git
cd finbert-trading-bot
```

2. Install the required packages:
```
pip install torch transformers lumibot alpaca-trade-api timedelta
```

3. Set up your Alpaca API credentials in the `tradingbot.py` file or use environment variables.

## Usage

### Backtesting

The default configuration runs a backtest on the SPY ETF for a specific date range:

```python
python tradingbot.py
```

### Live Trading

To run the bot in live paper trading mode, uncomment the following lines in `tradingbot.py`:

```python
# trader = Trader()
# trader.add_strategy(strategy)
# trader.run_all()
```

And comment out the backtest section:

```python
# strategy.backtest(YahooDataBacktesting, 
#                 start_date, 
#                 end_date,
#                 parameters={"symbol":"SPY",
#                           "cash_at_risk":.5})
```

## How It Works

1. The bot retrieves recent news related to the specified symbol from Alpaca.
2. It analyzes the sentiment of the news headlines using the FinBERT model.
3. If sentiment is positive with high probability, it places a buy order.
4. If sentiment is negative with high probability, it places a sell order.
5. Each order includes take-profit and stop-loss parameters.

## Customization

You can customize the following parameters in the `MLTrader` class:
- `symbol`: The stock or ETF to trade (default: "SPY")
- `cash_at_risk`: Percentage of cash to risk per trade (default: 0.5)
- Take-profit and stop-loss thresholds
- Sentiment probability threshold (currently set at 0.999)

## Disclaimer

This trading bot is for educational and research purposes only. It is not financial advice. Trading involves risk, and you should never trade with money you cannot afford to lose.

## License

[MIT License](LICENSE)

## Acknowledgements

- [ProsusAI/finbert](https://huggingface.co/ProsusAI/finbert) for the FinBERT model
- [Lumibot](https://github.com/Lumibot/lumibot) for the trading strategy framework
- [Alpaca](https://alpaca.markets/) for their trading API
