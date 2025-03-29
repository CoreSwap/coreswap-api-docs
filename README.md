# coreswap-api-docs
## Flow
[Currencies](#Currencies)  
[exchange_range](#Exchange%20Range)  
[estimate](#Estimate)  
[exchange](#Exchange)  
[status](#Status)   

## Endpoints

https://coreswap.io/api/

### Currencies
**GET**
https://coreswap.io/api/currencies

##### Request parameters:
None
##### Response example:
```json
{"BTC_BTC":{"currency_id":"BTC","network":"BTC","fullname":"Bitcoin","extraId":false},"ETH_ETH":{"currency_id":"ETH","network":"ETH","fullname":"Ethereum","extraId":false},"XMR_XMR":{"currency_id":"XMR","network":"XMR","fullname":"Monero","extraId":false},"CORE_CORE":{"currency_id":"CORE","network":"CORE","fullname":"CORE (CORE)","extraId":false},"USDT_ETH":{"currency_id":"USDT","network":"ETH","fullname":"Tether USDT (ERC20)","extraId":false},"ETH_ARBITRUM":{"currency_id":"ETH","network":"ARBITRUM","fullname":"Ethereum (Arbitrum)","extraId":false},"ETH_OP":{"currency_id":"ETH","network":"OP","fullname":"Ethereum (Optimism)","extraId":false},"ETH_ZKSYNC":{"currency_id":"ETH","network":"ZKSYNC","fullname":"Ethereum (ZkSync Era)","extraId":false}}
```

##### Response Format:
Returns full list of currencies, each currency object in the format:    
**currency_id** - ID of the currency  
**network** - Network ID of the currency  
**fullname** - Full name of the currency   
**extraId** - If an extra Id (example memo) is optional for that currency  


### Exchange Range
**GET**
https://coreswap.io/api/exchange_range

##### Request parameters:
**from_currency** - ID of the currency from  
**from_network** - Network ID of the currency  from
**to_currency** - ID of the currency from  to  
**to_network** - Network ID of the currency  to  
##### Request example:
https://coreswap.io/api/exchange_range?from_currency=ETH&from_network=ETH&to_currency=USDT&to_network=TRX
##### Response example:
```json
{
"min_amount":0.00433861,
"max_amount":252.918
}
```

##### Response Format:
Returns min & max of the exchange  
**min_amount** - min amount of the exchange  
**max_amount** - max amount of the exchange  

### Estimate
**GET**
https://coreswap.io/api/estimate

##### Request parameters:
**from_currency** - ID of the currency from  
**from_network** - Network ID of the currency  from
**to_currency** - ID of the currency from  to  
**to_network** - Network ID of the currency  to  
**amount** - Amount from  
**rate_type** - OPTIONAL: Rate type, "fixed" or empty (or "float")
##### Request example:
https://coreswap.io/api/estimate?from_currency=ETH&from_network=ETH&to_currency=USDT&to_network=TRX&amount=1
##### Response example:
```json
{
"from_currency":"ETH",
"from_network":"ETH",
"to_currency":"USDT",
"to_network":"TRX",
"amount_from":1,
"amount_to":1895.7228466640001,
"rate_type":"float",
"minimum_amount":0.00434541,
"maximum_amount":252.918,
"fromextraId":false,
"toextraId":false
}
```

##### Response Format:
**from_currency**  
**from_network**  
**to_currency**  
**to_network**  
**amount_from** - Amount from  
**amount_to** - Estimated amount to  
**rate_type** - OPTIONAL: Rate type, "fixed" or empty (or "float")  
**minimum_amount** - payout address  
**maximum_amount** - OPTIONAL: Refund address if exchange fails  
**fromextraId** - OPTIONAL: refund extra Id if from currency has extra id  
**toextraId** - OPTIONAL: refund extra Id if from currency has extra id  

### Exchange
**POST**
https://coreswap.io/api/exchange

##### Request parameters:

**HEADER**:  x-coreswap-apikey: YOURAPIKEY

**from_currency**  
**from_network**  
**to_currency**  
**to_network**  
**amount** - Amount from  
**rate_type** - OPTIONAL: Rate type, "fixed" or empty (or "float")  
**to_address** - payout address  
**extraid_to** - OPTIONAL payout extra Id (Only if extra Id require for to currency)  
**address_refund** - OPTIONAL: Refund address if exchange fails  
**extraid_refund** - OPTIONAL: refund extra Id if from currency has extra id  
##### Request example:
```json
{
 "from_currency":"DAI",
 "from_network":"ETH",
 "to_currency":"USDT",
 "to_network":"TRX",
 "amount":500,
 "rate_type":"float",
 "to_address":"TT2T17KZhoDu47i2E4FWxfG79zdkEWkU9N",
 "address_refund":"",
 "extraid_refund":""
}
```
##### Response example:
```json
{
    "id": "da557db84b",
    "deposit_address": "0xD52530529Bee1a37f9531A060C7c8Ac0f40379FF",
    "deposit_extraId": null,
    "from_currency": "DAI",
    "from_network": "ETH",
    "to_currency": "USDT",
    "to_network": "TRX",
    "to_address": "TT2T17KZhoDu47i2E4FWxfG79zdkEWkU9N",
    "to_extraId": null,
    "from_amount": 500,
    "to_amount": 488.005706,
    "rate_type": "float",
    "partner": "a1f560d7",
    "time_created": "2025-03-29 07:33:04"
}
```

##### Response Format:  
**id** - ID of the exchange  
**deposit_address** - Our address to send the deposit.  
**deposit_extraId** - extra ID of the deposit address (Null if not required).  
**from_currency** - From currency to deposit  
**from_network** - From network  
**to_currency** - To currency to deposit  
**to_network** - To network  
**to_address** - Address that exchanged coins will be sent  
**to_extraId** - Extra id of the address that coins will be sent (Null if not provided or to_currency does not have)  
**from_amount** - Amount expected to send  
**to_amount** - Amount expected to receive   
**rate_type** - Rate type of exchange, fixed or float.  
**partner** - Partner UUID who created the exchange  
**time_created** - Date & Time created  

### status
**GET**
https://coreswap.io/api/status

##### Request parameters:

**id** - ID of exchange  

##### Request example:
https://coreswap.io/api/status?id=da557db84b
##### Response example:
```json
{
    "id": "da557db84b",
    "status": "pending",
    "deposit_address": "0xD52530529Bee1a37f9531A060C7c8Ac0f40379FF",
    "deposit_extraId": null,
    "from_currency": "DAI",
    "from_network": "ETH",
    "to_currency": "USDT",
    "to_network": "TRX",
    "to_address": "TT2T17KZhoDu47i2E4FWxfG79zdkEWkU9N",
    "to_extraId": null,
    "from_amount": 500,
    "to_amount": 488.005706,
    "rate_type": "float",
    "partner": "a1f560d7",
    "time_created": "2025-03-29 07:33:04",
    "inHash": null,
    "amount_received": null,
    "amount_sent": null,
    "outHash": null
}
```
##### Response Format:
Response parameters are the same as /exchange response, with the addition of:  
**status** - Status of the exchange: pending, confirming, processing, sending, complete, refunding, expired  
**inHash** - input hash of the deposit to our our address  
**amount_received** - Amount deposited to our address  
**amount_sent** - Amount sent to the user address  
**outHash** - Out hash to the user address  

