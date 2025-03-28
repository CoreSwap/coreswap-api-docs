# coreswap-api-docs
## Flow

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
{"min_amount":0.00433861,"max_amount":252.918}
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
{"from_currency":"ETH","from_network":"ETH","to_currency":"USDT","to_network":"TRX","amount_from":1,"amount_to":1895.7228466640001,"rate_type":"float","minimum_amount":0.00434541,"maximum_amount":252.918,"fromextraId":false,"toextraId":false}
```

##### Response Format:
Returns min & max of the exchange  
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
{"from_currency":"ETH","from_network":"ETH","to_currency":"USDT","to_network":"TRX","amount":1,"rate_type":"float","to_address":"T42ebd8921db2718d0gd87dfsnuiwfw"}
```
##### Response example:

##### Response Format:
Returns min & max of the exchange  
**id** - exchange ID

### status
**GET**
https://coreswap.io/api/status?id=42332553212

##### Request parameters:

**id** - ID of exchange  
##### Request example:
https://coreswap.io/api/status?id=42332553212

##### Response example:

##### Response Format:


