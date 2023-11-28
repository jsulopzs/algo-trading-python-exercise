# Snippets

## Download Stock Market Data

```python
import yfinance as yf

df = yf.download('SPY')
```

## DataFrame Operations

### Select Columns

```python
df_close = df[['Adj Close']]
df_close
```

### Filter DataFrame by Date

```python
df = df.loc['2018-01-01':'2020-12-31']
df = df.loc['2018-01-01':]
df = df.loc[:'2020-12-31']
```

### Daily Returns

```python
df['return_daily'] = df['close'].pct_change().fillna(0).add(1)
```

### Cumulative Returns

```python
df['return_cumulative'] = df['return_daily'].cumprod().sub(1)
```

## Alpaca API


### Order configuration

```python
from alpaca.trading.requests import MarketOrderRequest
from alpaca.trading.enums import OrderSide, TimeInForce

market_order_data = MarketOrderRequest(
    symbol="SPY", qty=0.023,
    side=OrderSide.BUY, time_in_force=TimeInForce.DAY)
```

### Synchronize Credentials

```python
from alpaca.trading.client import TradingClient

API_KEY = '???'
SECRET_KEY = '???'

trading_client = TradingClient(API_KEY, SECRET_KEY, paper=True)
```

# Submit Order

```python
market_order = trading_client.submit_order(order_data=market_order_data)
```

## Backtesting.py

### Create Investment Strategy

```python
from backtesting import Strategy

class BuyAndHold(Strategy):
    def init(self):
        self.buy()
    
    def next(self):
        pass
```

### Backtest Strategy

```python
from backtesting import Backtest

backtest = Backtest(df, BuyAndHold, cash=10000, commission=.002)
backtest.run()
```

### Plot Results

```python
backtest.plot()
```

## Strategies

### Backtesting.py Example: SMA Crossover

https://kernc.github.io/backtesting.py/

### And more...

They'll be [uncovered in the Bootcamp](https://maven.com/datons-academy).