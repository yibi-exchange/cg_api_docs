<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Market API](#market-api)
  - [GET /v1/pairs](#get-v1pairs)
  - [GET /v1/tickers](#get-v1tickers)
  - [GET /v1/orderbook](#get-v1orderbook)
  - [GET /v1/historical_trades](#get-v1historical_trades)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Market API

## GET /v1/pairs  
Get the list of all exchange pairs.

Request: None

Response: Object[]

Name | Data type | Description 
------------ | ------------ | ------------
tickerId | string | Exchange pair name
base | string | Symbol/currency code of a the base crypto asset, eg. BTC
target | string | Symbol/currency code of the target crypto asset, eg. USDT


Data example:
```json
{
"code": "1",
"success": true,
"msg": null,
"data": [{
    "ticker_id": "ETH_USDT",
    "base": "ETH",
    "target": "USDT"
}, {
    "ticker_id": "BTC_USDT",
    "base": "BTC",
    "target": "USDT"
  }]
}
```

## GET /v1/tickers  
Get a 24-hour pricing and volume summary for each market pair available on the exchange.

Request: None

Response: Object[]

Name | Data type | Description 
------------ | ------------ | ------------
tickerId | string | Identifier of a ticker with delimiter to separate base_target, eg. BTC_USDT.
lastPrice | decimal | Last transacted price of base currency based on given target currency
baseVolume | decimal | 24-hour trading volume denoted in BASE currency
targetVolume | decimal | 24 hour trading volume denoted in TARGET currency
isFrozen | integer | Indicates if the market is currently enabled (0) or disabled (1).
                      
Data example:
```json
{
    "code":"1",
    "success":true,
    "msg":null,
    "data":[
        {
            "ticker_id":"BTC_USDT",
            "last_price":"42065.72",
            "base_currency":"1084.92",
            "target_currency":"45448520.44",
            "isFrozen":0
        },
        {
            "ticker_id":"ETH_USDT",
            "last_price":"3147.16",
            "base_currency":"9659.14",
            "target_currency":"30085798.27",
            "isFrozen":0
        }
    ]
}
```

## GET /v1/orderbook

Order book depth details

Request:  

Name | Data type | Description 
------------ | ------------ | ------------
tickerId | string | A pair such as "BTC_USDT"
depth | integer | (optional)Order depth quantity：[100, 200, 500...]. Depth = 100 means 50 for each buy/sell.

Response: Object[]

Name | Data type | Description 
------------ | ------------ | ------------
tickerId | string | A pair such as "BTC_USDT"
timestamp | timestamp | Unix timestamp in milliseconds for when the last updated time occurred.
bids | decimal | An array containing 2 elements. The offer price and quantity for each bid order
asks | decimal | An array containing 2 elements. The ask price and quantity for each ask order



Data example:
```
/* GET /v1/orderBook?tickerId=BTC_USDT */
```
```json
{
"code": "1",
"success": true,
"msg": null,
"data": {
    "tickerId": "BTC_USDT",
    "timestamp": "1639473000000",
    "bids": [
        ["48735.05", "0.200128"],
        ["48735.04", "0.1005"]
  ],
    "asks": [
        ["48735.06", "0.203296"],
        ["48735.07", "0.108152"]
     ]
  }
}
```

## GET /v1/historical_trades

Transaction records

Request:  

Name | Data type | Description 
------------ | ------------ | ------------
tickerId | String | A pair such as "BTC_USDT"

Response: Object

Name | Data type | Description 
------------ | ------------ | ------------
tradeId | int | Records id
price | decimal | Transaction price in base pair volume.
base_volume | decimal | Transaction amount in base pair volume.
target_volume | decimal | Transaction amount in target pair volume.
trade_timestamp | timestamp | Unix timestamp in milliseconds for when the transaction occurred.
type | string | Used to determine the type of the transaction that was completed. Buy – Identifies an ask that was removed from the order book. Sell – Identifies a bid that was removed from the order book.
                                                                                                
Data example:
```
/* GET /v1/historicalTrades?tickerId=BTC_USDT */
```
```json
{
"code": "1",
"success": true,
"msg": null,
"data": {
    "buy": [{
        "trade_id": 187317363,
        "price": 293392.99,
        "base_volume": 0.000146,
        "target_volume": 42.83537654,
        "trade_timestamp": 1639470864000,
        "type": "buy"
}],
    "sell": [{
        "trade_id": 187314280,
        "price": 297323.2,
        "base_volume": 0.45152,
        "target_volume": 134247.37126400,
        "trade_timestamp": 1639470624000,
        "type": "sell"
    }]
  }
}
```
