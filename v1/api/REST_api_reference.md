<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Market API](#market-api)
  - [GET /cg/pairs](#get-cgpairs)
  - [GET /cg/tickers](#get-cgtickers)
  - [GET /cg/orderbook](#get-cgorderbook)
  - [GET /cg/historical_trades](#get-cghistorical_trades)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Market API

## GET /cg/pairs  
Get the list of all exchange pairs.

Request: None

Url: https://api.yibi.co/cg/pairs

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

## GET /cg/tickers  
Get a 24-hour pricing and volume summary for each market pair available on the exchange.

Request: None

Url: https://api.yibi.co/cg/tickers

Response: Object[]

Name | Data type | Description 
------------ | ------------ | ------------
ticker_id | string | Identifier of a ticker with delimiter to separate base_target, eg. BTC_USDT.
base_currency	| string |	Symbol/currency code of base pair, eg. BTC
target_currency |	string	| Symbol/currency code of target pair, eg. USDT
last_price | decimal | Last transacted price of base currency based on given target currency
base_volume | decimal | 24-hour trading volume denoted in BASE currency
target_volume | decimal | 24 hour trading volume denoted in TARGET currency
bid |	string |	Current highest bid price
ask |	string |	Current lowest ask price
high |	string |	Rolling 24-hours highest transaction price
low	| string |	Rolling 24-hours lowest transaction price
                      
Data example:
```json
{
	"code": "1",
	"success": true,
	"msg": null,
	"data": [{
		"ticker_id": "BTC_USDT",
		"base_currency": "BTC",
		"target_currency": "USDT",
		"last_price": "40047.48",
		"base_volume": "4.09582",
		"target_volume": "163607.9687558",
		"bid": "40046.82",
		"ask": "40050.7",
		"high": "41208.32",
		"low": "39586.45"
	}, {
		"ticker_id": "ETH_USDT",
		"base_currency": "ETH",
		"target_currency": "USDT",
		"last_price": "3021.59",
		"base_volume": "46.4912",
		"target_volume": "140262.58768",
		"bid": "3021.63",
		"ask": "3021.73",
		"high": "3050.12",
		"low": "2977.73"
	}]
}
```

## GET /cg/orderbook

Order book depth details

Request:  

Name | Data type | Description 
------------ | ------------ | ------------
tickerId | string | A pair such as "BTC_USDT"
depth | integer | (optional)Order depth quantity：[100, 200, 500...]. Depth = 100 means 50 for each buy/sell.

Url: https://api.yibi.co/cg/orderbook?ticker_id=BTC_USDT&depth=100

Response: Object[]

Name | Data type | Description 
------------ | ------------ | ------------
ticker_id | string | A pair such as "BTC_USDT"
timestamp | timestamp | Unix timestamp in milliseconds for when the last updated time occurred.
bids | decimal | An array containing 2 elements. The offer price and quantity for each bid order
asks | decimal | An array containing 2 elements. The ask price and quantity for each ask order



Data example:
```json
{
"code": "1",
"success": true,
"msg": null,
"data": {
    "ticker_id": "BTC_USDT",
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

## GET /cg/historical_trades

Transaction records

Request:  

Name | Data type | Description 
------------ | ------------ | ------------
ticker_id | String | A pair such as "BTC_USDT"
type | String | To indicate nature of trade - buy/sell

Url: https://api.yibi.co/cg/historical_trades?ticker_id=BTC_USDT

Response: Object

Name | Data type | Description 
------------ | ------------ | ------------
trade_id | int | Records id
price | decimal | Transaction price in base pair volume.
base_volume | decimal | Transaction amount in base pair volume.
target_volume | decimal | Transaction amount in target pair volume.
trade_timestamp | timestamp | Unix timestamp in milliseconds for when the transaction occurred.
type | string | Used to determine the type of the transaction that was completed. Buy – Identifies an ask that was removed from the order book. Sell – Identifies a bid that was removed from the order book.
                                                                                                
Data example:
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
