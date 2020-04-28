
# HTTP API
The OKChain HTTP API provides access to an OKChain Chain node deployment and market data services.

## 账户（Accounts）
### 获取account地址信息

http接口：
```http
GET okchain/v1/accounts/{address}
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---:|
|address|String|true|账户地址|

Response:

```
    {
      "code": 0,
      "msg": "",
      "detail_msg": "",
      "data": {
        "address": "okchain1gaszdnrmghask7kz8n2tdxq0wk2a69z9336mjh",
        "currencies": [
          {
            "symbol": "okt",
            "available": "10000000.00000000",
            "freeze": "0",
            "locked": "0"
          }
        ]
      }
    }
    
```

### 获取用户所有数字资产信息

http接口:

```http
GET  okchain/v1/accounts/{address}?show=all
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---|
|address|String|	true|	账户地址|
|show|String|false|是否显示所有数字资产，all或者partial,默认为partial|

Response:

```json
{
	"code": 0,
	"data": {
		"address": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
		"currencies": [{
			"symbol": "acoin",
			"available": "10000000.00000000",
			"freeze": "0",
			"locked": "0"
		  }, {
            "symbol": "bcoin",
			"available": "10000000.00000000",
			"freeze": "0",
			"locked": "0"
        }]
	},
	"detail_msg": "",
	"msg": ""
}
```



### 获取用户单个数字资产信息

http接口:

```http
GET okchain/v1/accounts/{address}?symbol="bcoin"
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---:|
|address|String|	true|	账户地址|
|symbol|	String|	true|	数字资产|

Response:

```json
{
	"code": 0,
	"data": {
		"address": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
		"currencies": [{
			"symbol": "acoin",
			"available": "10000000.00000000",
			"freeze": "0",
			"locked": "0"
		}, {
      "symbol": "bcoin",
			"available": "10000000.00000000",
			"freeze": "0",
			"locked": "0"
    }]
	},
	"detail_msg": "",
	"msg": ""
}
```
## 行情（Markets）
### 获取所有数字资产的信息

http接口:

```http
GET okchain/v1/tokens
```

接口参数：无

Response:

```json
{
	"code": 0,
	"data": [{
    "description": "bcoin",
		"symbol": "bcoin",
		"original_symbol": "bcoin",
		"whole_name": "bcoin",
		"total_supply": "210000000",
		"owner": "okchain1kyh26rw89f8a4ym4p49g5z59mcj0xs4j045e39",
		"mintable": true
	}],
	"detail_msg": "",
	"msg": ""
}
```

### 获取单个数字资产的信息

http接口:

```http
GET okchain/v1/token/{symbol}
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---:|
|symbol|	String|	true|	数字资产名称|

Response:

```json
{
	"code": 0,
	"msg": "",
	"detail_msg": "",
	"data": {
		"description": "",
		"symbol": "bcoin-805",
		"original_symbol": "bcoin",
		"whole_name": "bcoin",
		"total_supply": "200000",
		"owner": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
		"mintable": false
	}
}
```

### 获取所有数字资产交易对的信息

http接口: 

```http
GET okchain/v1/products
```

接口参数：无


Response:

```json
{
	"code": 0,
	"msg": "",
	"detail_msg": "",
	"data": [{
		"base_asset_symbol": "acoin",
		"quote_asset_symbol": "okt",
		"price": "10.00000000",
		"max_price_digit": "1",
		"max_size_digit": "2",
		"min_trade_size": "0.10000000",
		"token_pair_id": "0"
	}]
}
```
### 获取交易深度信息

http接口: 
```http
GET okchain/v1/order/depthbook
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---:|
|product|String|    true| 数字资产对信息eg:btc_okt |
|size|Number|false|档位（maxSize:200）,第一版固定为200|


Response:

```Response

{
	"code": 0,
	"data": {
	    "asks": [{
	        #卖方深度  排序：asc
            "price": "string", #价格
            "quantity": "string" #数量
        }],
        "bids": [{
            #买方深度 排序：desc
            "price": "string",#价格
            "quantity": "string"#数量
        }]
    },
    "msg": "string"
}

```

### 获取交易K线信息

http接口: 
```http
GET okchain/v1/candles/{product}?granularity=21600&size=1000
```

接口参数：

|Name |Type |Required|Example|Description|
|:---:|:---:|:------:|:--- : |:-------:|
|product|String|     true|bcoin_okt|数字资产交易对名称|
|granularity|int|false|180<br>60|时间颗粒度，时间粒度，以秒为单位，默认值60. 如[60/180/300/900/1800/3600/7200/14400/21600/43200/86400/604800]<br>对应{1min,3min,5min,15min,30min,1hour,2hour,4hour,6hour,12hour,1day,1week}|
|size|int|false|100|获取k线数据的数量，最多1000条.默认值100|

Response:

```Response

{
    "code": 0,#0:成功，其他：失败
    "data": [[
        "2018-07-12T04:00:00.000Z",#创建时间
        "6343.3587"#开盘价
        "6345.0453",#最高价
        "6142.2336",#最低价
        "6186.8354",#收盘价
        "8429.75582698",#成交量
    ]],
    "detail_msg": "string",
    "msg": "string"
}

```

### 获取所有的交易行情信息

http接口: 
```http
GET okchain/v1/tickers
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---:|
|count|int|false|获取条数,默认值100|

Response:

```Response

{
    "code": 0,
    "data": [{
        "close": "29.777",#24小时 close
        "high": "55.44", #最高成交价
        "low": "22.22", #最低成交价
        "open": "55.44",#24小时 open
        "price": "29.777",#最新成交价
        "product": "bcoin-2ac_okt",#数字资产交易对
        "symbol": "bcoin-2ac_okt",
        "timestamp": "2019-07-25T09:49:04.954Z",#时间戳
        "volume": "266.64",#成交量
    }],
    "detail_msg": "",
    "msg": ""
}

```

### 获取某数字资产交易对最近成交记录

http接口: 
```http
GET okchain/v1/matches
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---|
|product|String|    true|    数字资产交易对|
|start|    int|    false|起始日期（时间戳，以秒为单位）|
|end|    int    |false    |结束日期（时间戳，以秒为单位）|
|page    |int    |false    |页号|
|per_page|    int    |false    |每页条数|

Response:

```

{
  "code": 0,
  "msg": "",
  "detail_msg": "",
  "data": {
    "data": [
        {
          "timestamp": 1559790137,
          "block_height": 386355,
          "product": "acoin-564_okt",
          "price": 3,
          "volume": 0.25
        },
        {
          "timestamp": 1559789554,
          "block_height": 386159,
          "product": "acoin-564_okt",
          "price": 1.9999,
          "volume": 2.9999
        },
        {
          "timestamp": 1559788804,
          "block_height": 385931,
          "product": "acoin-564_okt",
          "price": 1,
          "volume": 1
        }
    ],
    "param_page": {
        "page": 1,
        "per_page": 50,
        "total": 3
    }
  }
}

```

## 交易（Trades）
### 下单（在base中）

http接口： 
```http
POST okchain/v1/txs
```

post发送内容：

```

{
    "tx": {
        "msg": [{
            "type": "okchain/order/MsgNew",
            "value": {
                "sender": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",//发送者address
                "product": "mycoin_okt",//数字资产交易对
                "side": "BUY",
                "price": "1",//价格
                "quantity": "0.1"//数量
            }
        }],
        "signatures": [{
            "pub_key": {
                "type": "tendermint/PubKeySecp256k1",
                "value": "AsfvubxdC51g5kpHh3ibtjEsm0INdvrpOgrzw/BcGExK"
            },
            "signature": "xce6VKVxf5nmOumEqVK2n8QiZG3mBi9P+SGTvDCHLAZxP9p8/zS/+VhVzWGI7tppW2uGNz/iToubTvHTd4y9KA=="
        }],
        "memo": "jin tian ye yao jia you ya"
    },
    "mode": "block"
}

```

签名内容：（拿私钥对以下信息签名生成上面的signature）

```

{
    "account_number": "0",
    "chain_id": "okchain",
    "memo": "jin tian ye yao jia you ya",
    "msgs": [{
	     "price": "1",
	     "product": "mycoin_okt",
	     "quantity": "0.1",
	     "sender": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
	     "side": "BUY"
    }],
    "sequence": “4”
}

```

Response:

```Response
{
	"raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":null}]",
	"logs": [{
		"log": "",
		"success": true,
		"msg_index": 0
	}],
	"events": [{
		"attributes": [{
			"value": "0",
			"key": "fee"
		}, {
			"value": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
			"key": "sender"
		}, {
			"value": "order",
			"key": "module"
		}, {
			"value": "ID1-0000000151-1",
			"key": "order_id"
		}, {
			"value": "new",
			"key": "action"
		}],
		"type": "message"
	}, {
		"attributes": [{
			"value": "okchain183rfa8tvtp6ax7jr7dfaf7ywv870sykx3uvcxn",
			"key": "recipient"
		}, {
			"value": "0.10000000okt",
			"key": "amount"
		}],
		"type": "transfer"
	}],
	"height": "151",
	"txhash": "F5E828BB8F87A95E3E4930FB683A443311EDC7705FEB691D9DA2EFF898127DD4"
}

```

### 撤单 （在base中）

http接口： 
```http
POST okchain/v1/txs
```

post发送内容：

```

{
    "tx": {
        "msg": [{
            "type": "okchain/order/MsgCancel",
            "value": {
                "sender": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
                "order_id": "ID1-0000000151-1"
            }
        }],
        "signatures": [{
            "pub_key": {
                "type": "tendermint/PubKeySecp256k1",
                "value": "AtXflms2umhaIZ4MX4pVFr23y3im37LXz+yvUNnDirtJ"//公钥
            },
            "signature": "/bPROoTE3yBBT9tLb6MzDIdHQHUeRvASRteoJ2aDW00/xEkUqS0zzWxf6GF87Fu1f3uNXle5b0rYOxqbi5IeuA=="
        }],
        "memo": ""//备注
    },
    "mode": "block"//sync模式在checkTx后返回,async模式立即返回,block模式在打包入块之后返回
}

```

签名内容：

```

{
    "account_number": "0",//account在blockchain上面的序号
    "chain_id": "okchain",
    "memo": "",
    "msgs": [{
        "order_id": "ID1-0000000151-1",
        "sender": "cosmos1ln5zguv3pccm59e4dmdtjxuw24a0cv7p4v8cl8"
    }],
    "sequence": "13"//该account发送transaction的序号
}

```

Response:

```
{
	"raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":null}]",
	"logs": [{
		"log": "",
		"success": true,
		"msg_index": 0
	}],
	"events": [{
		"attributes": [{
			"value": "0",
			"key": "fee"
		}, {
			"value": "okchain183rfa8tvtp6ax7jr7dfaf7ywv870sykx3uvcxn",
			"key": "sender"
		}, {
			"value": "okchain183rfa8tvtp6ax7jr7dfaf7ywv870sykx3uvcxn",
			"key": "sender"
		}, {
			"value": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
			"key": "sender"
		}, {
			"value": "order",
			"key": "module"
		}, {
			"value": "0.00000100okt",
			"key": "fee"
		}, {
			"value": "ID1-0000000151-1",
			"key": "order_id"
		}, {
			"value": "cancel",
			"key": "action"
		}],
		"type": "message"
	}, {
		"attributes": [{
			"value": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
			"key": "recipient"
		}, {
			"value": "0.10000000okt",
			"key": "amount"
		}, {
			"value": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
			"key": "recipient"
		}, {
			"value": "0.25920000okt",
			"key": "amount"
		}, {
			"value": "okchain17xpfvakm2amg962yls6f84z3kell8c5ljresa7",
			"key": "recipient"
		}, {
			"value": "0.00000100okt",
			"key": "amount"
		}],
		"type": "transfer"
	}],
	"height": "152",
	"txhash": "FC789FFDF31AB00EC0EAA3F9D6B18CBD23D36DEA59B1305B523E8AED8BB8C6F3"
}

```

### 转账（在base中）

http接口： 
```http
POST okchain/v1/txs
```

post发送内容：

```
{
	"mode": "block",
	"tx": {
		"memo": "",
		"msg": [{
			"type": "okchain/token/MsgTransfer",
			"value": {
				"amount": [{
					"amount": "16.00000000",
					"denom": "okt"
				}],
				"from_address": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
				"to_address": "okchain1t2cvfv58764q4wdly7qjx5d2z89lewvwq2448n"
			}
		}],
		"signatures": [{
			"pub_key": {
				"type": "tendermint/PubKeySecp256k1",
				"value": "Aga5P7TWoqq+6cmxOTHhj9tLqFlHNlLpWMEdAfHcokp+"
			},
			"signature": "AFwTvZT06TG8fm31Hrf76M9AWmzDakNe1+4s/6czvIVQF+mzL1t+Jwp4bMrYSlgETqm4s18O+q6xt5y1K/t3mw=="
		}]
	}
}

```

签名内容：（拿私钥对以下信息签名生成上面的signature）

```Response
{
	"account_number": "8",
	"chain_id": "okchain",
	"memo": "",
	"msgs": [{
		"amount": [{
			"amount": "16.00000000",
			"denom": "okt"
		}],
		"from_address": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
		"to_address": "okchain1t2cvfv58764q4wdly7qjx5d2z89lewvwq2448n"
	}],
	"sequence": "5"
}

```

Response:

```Response
{
	"raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":null}]",
	"logs": [{
		"log": "",
		"success": true,
		"msg_index": 0
	}],
	"events": [{
		"attributes": [{
			"value": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
			"key": "sender"
		}, {
			"value": "token",
			"key": "module"
		}, {
			"value": "0.01250000 okt",
			"key": "fee"
		}, {
			"value": "send",
			"key": "action"
		}, {
			"value": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
			"key": "sender"
		}],
		"type": "message"
	}, {
		"attributes": [{
			"value": "okchain1t2cvfv58764q4wdly7qjx5d2z89lewvwq2448n",
			"key": "recipient"
		}, {
			"value": "16.00000000okt",
			"key": "amount"
		}, {
			"value": "okchain17xpfvakm2amg962yls6f84z3kell8c5ljresa7",
			"key": "recipient"
		}, {
			"value": "0.01250000okt",
			"key": "amount"
		}],
		"type": "transfer"
	}],
	"height": "237",
	"txhash": "D9427220DF41B3DBF8DE5991F850F90B47FEBDB22B0982FC5ADCC0924AB947E4"
}

```

### 未成交订单

http接口:
```http
GET okchain/v1/order/list/open？product=mycoin_okt&address=cosmos1hghms6dtm8quxegrkcnw4wnzj5e5sc4am0gxyr&start=1556541851&end=1556541851&page=0&per_page=50
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---|
|product    |String|    false|    数字资产交易对|
|address|    String|    true|    地址|
|start    |int|    false|    开始时间戳|
|end    |int|    false|    结束时间戳|
|side|string|false|BUY/SELL|
|page    |int|    false|    第几页|
|per_page    |int|    false|    每页多少行|

Response:

参数：获取全部数字资产交易对的委托单时不传product参数

Response:

```Response

{
    "code": 0,
    "msg": "",
    "detail_msg": "",
    "data": {
        "data":[
            {
                "txhash":"2144D0F85B67D9508066004400BF8044010ED5FC4B43417F9A44CDC3EBAD9765",
                "order_id": "O0000000008-0000",
                "sender": "cosmos1hghms6dtm8quxegrkcnw4wnzj5e5sc4am0gxyr",
                "product": "mycoin_okt",
                "side": "BUY",
                "price": "10.000000000000000000",
                "quantity": "1.100000000000000000",
                "status": 0,  //(0-5) -> (Open, Filled, Cancelled, Expired,
                // PartialFilledCancelled, PartialFilledExpired)
                "filled_avg_price": "10.000000000000000000",
                "remain_quantity": "0.100000000000000000",
                "timestamp": 1553842734
            },
        ],
        "param_page": {
            "total": 3,
            "page": 1,
            "per_page": 50,
        }
    }
}

```

### 历史订单
http接口:

```http
GET okchain/v1/order/list/closed
```

接口参数：address, product, start, end, page, per_page。全部数字资产交易对时不传product参数

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---|
|product    |String|    false|    数字资产交易对|
|address|    String|    true|    地址|
|side|String|false|没有该字段则都要"BUY","SELL"|
|hide_no_fill|int|false|关于完全撤销或者完全过期订单 0:不隐藏 1:隐藏|
|start    |int|    false|    开始时间戳|
|end    |int|    false|    结束时间戳|
|page    |int|    false|    第几页|
|per_page    |int|    false|    每页多少行|

Response:

```Response

{
    "code": 0,
    "msg": "",
    "detail_msg": "",
    "data": {
        "data":[
            {
                "txhash": "2144D0F85B67D9508066004400BF8044010ED5FC4B43417F9A44CDC3EBAD9765",
                "order_id": "O0000000008-0000",
                "sender": "cosmos1hghms6dtm8quxegrkcnw4wnzj5e5sc4am0gxyr",
                "product": "mycoin_okt",
                "side": "BUY",
                "price": "10.000000000000000000",
                "quantity": "1.100000000000000000",
                "status": 0,  //(0-5) -> (Open, Filled, Cancelled, Expired,
                 // PartialFilledCancelled, PartialFilledExpired)
                "filled_avg_price": "10.000000000000000000",
                "remain_quantity": "0.100000000000000000",
                "timestamp": 1553842734
            },
        ],
    "param_page": {
        "total": 3,
        "page": 1,
        "per_page": 50,
    }
}

```

### 链上交易历史
http接口:
```http
GET okchain/v1/block_tx_hashes/{block_height}
```

参数：block_height 块高 int类型

response: txHash列表，string类型
```
    [
        "hash1",
        "hash2",
        ...
    ]

```

### 费用历史
http接口：
```http
GET okchain/v1/fees
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---:|
|address    |String|    true|    账户地址|
|page|    int|    false|    页号|
|per_page|int|false|每页条数|

Response:

```Response
{
    "code": 0,
    "msg": "",
    "detail_msg": "",
    "data": {
        "data": [
            {
                "address": "okchain1lzekrp7dezrs940m7c0nnhjvyhlzppnaf6vjsy",
                "fee": "0.01250000okt",
                "fee_type": "transfer",  // 手续费类型：transfer/new/cancel/expire/deal
                "timestamp": 1558407348
            }
        ],
    "param_page": {
    "page": 1,
    "per_page": 50,
    "total": 1
        }
    }
}

```


## 账单（Deals）
### 获取成交明细

http接口: 
```http
GET okchain/v1/deals
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---|
|address|String|	true|	账户地址|
|product|String|	false|	数字资产交易对|
|side|String|false|没有该字段则都要 "BUY", "SELL"|
|start|	int|	false|起始日期（时间戳，以秒为单位）|
|end|	int	|false	|结束日期（时间戳，以秒为单位）|
|page	|int	|false	|页号|
|per_page|	int	|false	|每页条数|

Response:

```Response

{
    "code": 0,
    "msg": "",
    "detail_msg": "",
    "data": {
        "data": [
            {
                "timestamp": 1558407585,
                "block_height": 463,
                "order_id": "ID0000000463-1",
                "sender": "okchain15wv9q08rv0f8dg08scv2ps45hs6v8qx37466qj",
                "product": "mycoin_okt",
                "side": "SELL",
                "price": 10,
                "volume": 1,
                "fee": "0.00400000okt"
            },
            {
                "timestamp": 1558407585,
                "block_height": 463,
                "order_id": "ID0000000010-1",
                "sender": "okchain1lzekrp7dezrs940m7c0nnhjvyhlzppnaf6vjsy",
                "product": "mycoin_okt",
                "side": "BUY",
                "price": 10,
                "volume": 1,
                "fee": "0.00400000okt"
            }
        ],
        "param_page": {
            "page": 1,
            "per_page": 50,
            "total": 2
        }
    }
}

```

### 获取交易记录

http接口: 
```http
GET okchain/v1/transactions
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---|
|address|    string|    true|    user address|
|type|int|false|账单类型，1:Transfer, 2:NewOrder, 3:CancelOrder|
|start    |int|    false| 起始日期 |
|end    |int|    false|    结束日期|
|page    |int|    false|    页号|
|per_page    |int|    false|    每页条数|

Response:

```Response

{
    "code": 0,
    "msg": "",
    "detail_msg": "",
    "data": {
        "data": [
            {
                "txhash":"3BEE2A0FDDD5EB077236879E139DC565580139F61ED6E391B2557D4A8F74BE83",
                "type": 1,  // 1:Transfer, 2:NewOrder, 3:CancelOrder
                "address": "okchain1lzekrp7dezrs940m7c0nnhjvyhlzppnaf6vjsy",
                "symbol": "okt",
                "side": 3,  // 1:buy, 2:sell, 3:from, 4:to
                "quantity": "1.00000000",
                "fee": "0.01250000okt",
                "timestamp": 1558407348
            },
        ],
        "param_page": {
            "page": 1,
            "per_page": 50,
            "total": 10
        }
    }
}

```
## 区块（Blocks）

### 获取最新区块

http接口：
```http
GET okchain/v1/blocks/latest
```

接口参数：无

Response:

```
    {
      "block_meta": {
        "block_id": {
          "hash": "BF623CD9248E2721C12F757A9AAD505DACAD6166903AB0D4E7A6669B4E02BA84",
          "parts": {
            "total": "1",
            "hash": "368C05B48E428C71FCB0C5E2962BD1DC9C0BEC96759D5733C0F141FA7EA7C1A1"
          }
        },
        "header": {
          "version": {
            "block": "10",
            "app": "0"
          },
          "chain_id": "okchain",
          "height": "433",
          "time": "2019-07-23T06:57:30.775579Z",
          "num_txs": "0",
          "total_txs": "18",
          "last_block_id": {
            "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
            "parts": {
              "total": "1",
              "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
            }
          },
          "last_commit_hash": "761C584E0EF03D7812AB16B2A9DE27BB5E6DA954BC19F32D303A634ADE84DB6E",
          "data_hash": "",
          "validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
          "next_validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
          "consensus_hash": "048091BC7DDC283F77BFBF91D73C44DA58C3DF8A9CBC867405D8B7F3DAADA22F",
          "app_hash": "F8F901256CA9F12C253BB6E79144473BF41476A1BB49CA202A788D19CBD65683",
          "last_results_hash": "",
          "evidence_hash": "",
          "proposer_address": "D4640375843B281A9656B3B755D0B227ACDE13D9"
        }
      },
      "block": {
        "header": {
          "version": {
            "block": "10",
            "app": "0"
          },
          "chain_id": "okchain",
          "height": "433",
          "time": "2019-07-23T06:57:30.775579Z",
          "num_txs": "0",
          "total_txs": "18",
          "last_block_id": {
            "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
            "parts": {
              "total": "1",
              "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
            }
          },
          "last_commit_hash": "761C584E0EF03D7812AB16B2A9DE27BB5E6DA954BC19F32D303A634ADE84DB6E",
          "data_hash": "",
          "validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
          "next_validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
          "consensus_hash": "048091BC7DDC283F77BFBF91D73C44DA58C3DF8A9CBC867405D8B7F3DAADA22F",
          "app_hash": "F8F901256CA9F12C253BB6E79144473BF41476A1BB49CA202A788D19CBD65683",
          "last_results_hash": "",
          "evidence_hash": "",
          "proposer_address": "D4640375843B281A9656B3B755D0B227ACDE13D9"
        },
        "data": {
          "txs": null
        },
        "evidence": {
          "evidence": null
        },
        "last_commit": {
          "block_id": {
            "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
            "parts": {
              "total": "1",
              "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
            }
          },
          "precommits": [
            {
              "type": 2,
              "height": "432",
              "round": "0",
              "block_id": {
                "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
                "parts": {
                  "total": "1",
                  "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
                }
              },
              "timestamp": "2019-07-23T06:57:30.775579Z",
              "validator_address": "6B6B879EEC588AC6D6C0A925DF40142558D92EF9",
              "validator_index": "0",
              "signature": "ZQWxt3dKDp7Rl6WuHJDcUr4HPrvDFf1pIUk7L/+f5hP5koL2NNM5GwjgzMzXfUXDfY6FvswXccut9150j/V2Dw=="
            },
            {
              "type": 2,
              "height": "432",
              "round": "0",
              "block_id": {
                "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
                "parts": {
                  "total": "1",
                  "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
                }
              },
              "timestamp": "2019-07-23T06:57:30.775579Z",
              "validator_address": "77E268D7F58CA2A9C81E27481DA5F8947E99E67A",
              "validator_index": "1",
              "signature": "lVo31wzOjdbW2LuMwoktxSoEXvfqdYp19uGqVfaLfRdlJIOcCFUXIFm8sM98qLLdZaILuQCfGzycpTUCiOhvBA=="
            },
            {
              "type": 2,
              "height": "432",
              "round": "0",
              "block_id": {
                "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
                "parts": {
                  "total": "1",
                  "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
                }
              },
              "timestamp": "2019-07-23T06:57:30.877204Z",
              "validator_address": "B576DAE9CEC142CD0E932F5821253B3DAE19B7B2",
              "validator_index": "2",
              "signature": "cAlEne+vWKBjDLwc9hcUYPRHRQvkWHbW8kCEHSBxdkYJJQq/c8Th1lqLRKGGGbM5ZHe6GjMWLyo88HpjmoVaDg=="
            },
            {
              "type": 2,
              "height": "432",
              "round": "0",
              "block_id": {
                "hash": "0DBD77228438CA65F11DD675428E4B7DC9904AC11A9C9AB5D8182C1A250F0AF1",
                "parts": {
                  "total": "1",
                  "hash": "9222C8B073CA130AB057467DD63E45E556DA2314F2EC7CA7B0ACDC738170CCD5"
                }
              },
              "timestamp": "2019-07-23T06:57:30.570501Z",
              "validator_address": "D4640375843B281A9656B3B755D0B227ACDE13D9",
              "validator_index": "3",
              "signature": "/R7mSWoj3qP1YlGMrHtmyxla4gjrWqnx0W57Bpy7knxR6jdFDIK8aWCiCKBm7T76FekvK/3wMg/FYuWB31GHBA=="
            }
          ]
        }
      }
    }
    
```

### 获取区块高度

http接口：
```http
GET okchain/v1/blocks/{height}
```

接口参数：

|Name|Type|Required|Description|
|---|---|---|---|
|height|    number|true|    Block height|

Response:

```
   {
     "block_meta": {
       "block_id": {
         "hash": "AE7D7FC321447A7F63031E28FD55CD9FF885EE73C38C62F63706C2ED3623ECFF",
         "parts": {
           "total": "1",
           "hash": "0E3BE14D6711CEEC468D44D1DB6FF702E92ACA521E8121698DD8BD521F07794F"
         }
       },
       "header": {
         "version": {
           "block": "10",
           "app": "0"
         },
         "chain_id": "okchain",
         "height": "1",
         "time": "2019-07-23T06:42:15.957762Z",
         "num_txs": "0",
         "total_txs": "0",
         "last_block_id": {
           "hash": "",
           "parts": {
             "total": "0",
             "hash": ""
           }
         },
         "last_commit_hash": "",
         "data_hash": "",
         "validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
         "next_validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
         "consensus_hash": "048091BC7DDC283F77BFBF91D73C44DA58C3DF8A9CBC867405D8B7F3DAADA22F",
         "app_hash": "",
         "last_results_hash": "",
         "evidence_hash": "",
         "proposer_address": "6B6B879EEC588AC6D6C0A925DF40142558D92EF9"
       }
     },
     "block": {
       "header": {
         "version": {
           "block": "10",
           "app": "0"
         },
         "chain_id": "okchain",
         "height": "1",
         "time": "2019-07-23T06:42:15.957762Z",
         "num_txs": "0",
         "total_txs": "0",
         "last_block_id": {
           "hash": "",
           "parts": {
             "total": "0",
             "hash": ""
           }
         },
         "last_commit_hash": "",
         "data_hash": "",
         "validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
         "next_validators_hash": "DEFD0C2394B21CF2DD2A49054E968C8754AB0CD20F31804028FA499A40358B19",
         "consensus_hash": "048091BC7DDC283F77BFBF91D73C44DA58C3DF8A9CBC867405D8B7F3DAADA22F",
         "app_hash": "",
         "last_results_hash": "",
         "evidence_hash": "",
         "proposer_address": "6B6B879EEC588AC6D6C0A925DF40142558D92EF9"
       },
       "data": {
         "txs": null
       },
       "evidence": {
         "evidence": null
       },
       "last_commit": {
         "block_id": {
           "hash": "",
           "parts": {
             "total": "0",
             "hash": ""
           }
         },
         "precommits": null
       }
     }
   }
```

### 根据Tx哈希值获取Tx

http接口：
```http
GET okchain/v1/txs/{hash}
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---:|
|hash|    string|true|    Tx hash|

Response:

```
    {
      "height": "468",
      "txhash": "0020A8D7EB798F223319DB636109DC00D258F2756B52F494A92BCABB14BC8BCC",
      "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
      "logs": [
        {
          "msg_index": "0",
          "success": true,
          "log": ""
        }
      ],
      "tags": [
        {
          "key": "fee",
          "value": "0.01250000 okt"
        },
        {
          "key": "action",
          "value": "send"
        }
      ],
      "tx": {
        "type": "auth/StdTx",
        "value": {
          "msg": [
            {
              "type": "token/Send",
              "value": {
                "from_address": "okchain1gaszdnrmghask7kz8n2tdxq0wk2a69z9336mjh",
                "to_address": "okchain1g7c3nvac7mjgn2m9mqllgat8wwd3aptdqket5k",
                "amount": [
                  {
                    "denom": "okt",
                    "amount": "10000.00000000"
                  }
                ]
              }
            }
          ],
          "signatures": [
            {
              "pub_key": {
                "type": "tendermint/PubKeySecp256k1",
                "value": "AnHEWKSC/pE4VIX8rbUpQFIRA88BNv/wC7e7mHAJ0+7I"
              },
              "signature": "SawuipMAXPkE/JFAv0SnS9rcsCbw1EIS8ZZo3qoW7QoPLa+60jPmvQhoRJaa3o+1b1/HnoBvIsn9On8UyKRv1A=="
            }
          ],
          "memo": ""
        }
      },
      "timestamp": "2019-07-23T06:58:22Z"
    }
    
```

## 交易币对(Dex)
### 查询账户创建的币对

如果不输入账户，则显示所有的币对信息 

http接口：

```http
GET okchain/v1/products
```

接口参数：

|   Name   |  Type  | Required |           Description            |
| :------: | :----: | :------: | :------------------------------: |
| address  | String |  false   | 币对拥有者的okchain地址（owner） |
|   page   |  int   |  false   |               页号               |
| per_page |  int   |  false   |             每页条数             |

Response:

```Response
{
  "code": 0,
  "msg": "",
  "detail_msg": "",
  "data": [
    {
      "base_asset_symbol": "xxb",
      "quote_asset_symbol": "okt",
      "price": "10.00000000",
      "max_price_digit": "8",
      "max_size_digit": "8",
      "min_trade_size": "0.00000000",
      "token_pair_id": "0",
      "delisting": false,
      "owner": "okchain183rfa8tvtp6ax7jr7dfaf7ywv870sykx3uvcxn",
      "deposits": {
        "denom": "okt",
        "amount": "0.00000000"
      },
      "block_height": "0"
    }
  ]
}
```

### 查询账户保证金

查询某个账户中币对的保证金，返回币对名称与保证金数量
http接口：

```http
GET okchain/v1/dex/deposits
```

接口参数：

|   Name   |  Type  | Required |           Description            |
| :------: | :----: | :------: | :------------------------------: |
| address  | String |   true   | 币对拥有者的okchain地址（owner） |
|   page   |  int   |  false   |               页号               |
| per_page |  int   |  false   |             每页条数             |

Response:

```Response
{
  "code": 0,
  "msg": "",
  "detail_msg": "",
  "data": [
    {
      "product": "xxb_okt",
      "deposits": {
        "denom": "okt",
        "amount": "100.00000000"
      }
    }
  ]
}
```

### 查询所有币对撮合顺序

查询币对的撮合顺序，返回有序币对名称

http接口：

```http
GET okchain/v1/dex/match_order
```

接口参数：

|   Name   | Type | Required | Description |
| :------: | :--: | :------: | :---------: |
|   page   | int  |  false   |    页号     |
| per_page | int  |  false   |  每页条数   |

Response：

```Response
{
  "code": 0,
  "msg": "",
  "detail_msg": "",
  "data": [
    "xxb_okt"
  ]
}
```


## 抵押(Staking)

### 获取所有validators

http接口：
```http
GET okchain/v1/staking/validators
```

接口参数：无

Response:

```
   [
     {
       "operator_address": "okchainvaloper13q7gl0jvk79qz7fgcty3qc49g8h2prnaa4v8m4",
       "consensus_pubkey": {
         "type": "tendermint/PubKeyEd25519",
         "value": "eLwaM5se0V3xjSf1VSPNafbxo8duuPIKc/O2P4P/BQI="
       },
       "jailed": false,
       "status": 2,
       "tokens": "1.00000000",
       "delegator_shares": "1.00000000",
       "description": {
         "moniker": "node1",
         "identity": "",
         "website": "",
         "details": ""
       },
       "unbonding_height": "0",
       "unbonding_time": "1970-01-01T00:00:00Z",
       "commission": {
         "rate": "0.00000000",
         "max_rate": "0.00000000",
         "max_change_rate": "0.00000000",
         "update_time": "2019-07-23T06:42:15.957762Z"
       },
       "min_self_delegation": "1.00000000"
     },
     {
       "operator_address": "okchainvaloper1n0az59a0xt263ngeqndxqcuhx2d4yyd0mayyzc",
       "consensus_pubkey": {
         "type": "tendermint/PubKeyEd25519",
         "value": "UwQZC3vQ7mZJ0zgAh5+OiXxn4MLddjTuRsOcFoitGDE="
       },
       "jailed": false,
       "status": 2,
       "tokens": "1.00000000",
       "delegator_shares": "1.00000000",
       "description": {
         "moniker": "node0",
         "identity": "",
         "website": "",
         "details": ""
       },
       "unbonding_height": "0",
       "unbonding_time": "1970-01-01T00:00:00Z",
       "commission": {
         "rate": "0.00000000",
         "max_rate": "0.00000000",
         "max_change_rate": "0.00000000",
         "update_time": "2019-07-23T06:42:15.957762Z"
       },
       "min_self_delegation": "1.00000000"
     },
   ]
   
```

### 列举全部operator_address-validator_address地址对

http接口：
```http
GET okchain/v1/staking/address
```

接口参数：无

Response:

```
   [
     {
       "operator_address": "okchainvaloper13q7gl0jvk79qz7fgcty3qc49g8h2prnaa4v8m4",
       "validator_address": "6B6B879EEC588AC6D6C0A925DF40142558D92EF9"
     },
     {
       "operator_address": "okchainvaloper1n0az59a0xt263ngeqndxqcuhx2d4yyd0mayyzc",
       "validator_address": "77E268D7F58CA2A9C81E27481DA5F8947E99E67A"
     },
   ]
   
```

### 通过operator_address查询对应account_address

http接口：
```http
GET okchain/v1/staking/address/{operator_addr}/account_address 
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---:|
|operator_addr|    string|true|   operator_address|


Response:

```
"okchain13q7gl0jvk79qz7fgcty3qc49g8h2prnaptazwn"
```

### 通过validator_address查询对应operator_address

http接口：
```http
GET okchain/v1/staking/address/{validator_addr}/validator_address
```

接口参数：

|Name|Type|Required|Description|
|:---:|:---:|:---:|:---:|
|validator_addr|    string|true|   validator_address|


Response:

```
"okchainvaloper1uujtlcc9u6w8gh0quzhtml4llu8pj02v87plt0"
```



### 查询一个delegator的资产信息，

包括抵押token，投票给了那些validator及票数，是否是proxy以及作为proxy的相关信息等

http接口：

```http
GET /staking/delegators/{delegatorAddr}
```

接口参数：

| Name          | Type   | Required | Description                                                  |
| ------------- | ------ | -------- | ------------------------------------------------------------ |
| validatorAddr | string | true     | validator_address   eg: okchain1ytjqlpdysv8dxnnzc3umxwacjkysy04t0u93ny |

Response:

```
{
    "delegator_address": "okchain1ytjqlpdysv8dxnnzc3umxwacjkysy04t0u93ny",
    "validator_address": null,
    "shares": "0.00000000",
    "tokens": "2000.00000000",
    "is_proxy": false,
    "total_delegated_tokens": "0.00000000",
    "proxy_address": ""
}
```



### 查询指定delegator的unbonding token信息

http接口：

```http
GET /staking/delegators/{delegatorAddr}/unbonding_delegations
```

接口参数：

| Name          | Type   | Required | Description                                                  |
| ------------- | ------ | -------- | ------------------------------------------------------------ |
| validatorAddr | string | true     | validator_address   eg: okchain1ytjqlpdysv8dxnnzc3umxwacjkysy04t0u93ny |

Response:

```
{
    "delegator_address": "okchain1ytjqlpdysv8dxnnzc3umxwacjkysy04t0u93ny",
    "quantity": "2.00000000",
    "completion_time": "2020-04-28T04:25:40.887546Z"
}
```



### 查询一个proxy（代理投票人）身上的代理关系

http接口：

```http
GET /staking/delegators/{delegatorAddr}/proxy
```

接口参数：

| Name          | Type   | Required | Description                                                  |
| ------------- | ------ | -------- | ------------------------------------------------------------ |
| validatorAddr | string | true     | validator_address   eg: okchain1ytjqlpdysv8dxnnzc3umxwacjkysy04t0u93ny |

Response:

```
[
    "okchain1g5h0mgydukwfm9f8j54vuqyhn5m39ufy0rz0ce"
]
```



### 查询一个validator身上所有的投票信息

http接口：

```http
GET /staking/validators/{validatorAddr}/votes
```

接口参数：

| Name          | Type   | Required | Description                                                  |
| ------------- | ------ | -------- | ------------------------------------------------------------ |
| validatorAddr | string | true     | validator_address   eg: okchain1ytjqlpdysv8dxnnzc3umxwacjkysy04t0u93ny |

Response:

```
[
    {
        "voter_address": "okchain1ytjqlpdysv8dxnnzc3umxwacjkysy04t0u93ny",
        "votes": "2665830913.08478000"
    }
]
```



### 查询当前所有的validator信息（bonded状态）

http接口：

```http
GET okchain/v1/staking/pool
```

接口参数：无

Response:

```
[
    {
        "operator_address": "okchainvaloper10q0rk5qnyag7wfvvt7rtphlw589m7frs863s3m",
        "consensus_pubkey": "okchainvalconspub1zcjduepqqxsxcjjletkq40ypzuqz8n925pk0ycw9h8g4saw27adyf2t93szsvpk77u",
        "jailed": false,
        "status": 2,
        "tokens": "0",
        "delegator_shares": "1000.00000000",
        "description": {
            "moniker": "node0",
            "identity": "",
            "website": "",
            "details": ""
        },
        "unbonding_height": "0",
        "unbonding_time": "1970-01-01T00:00:00Z",
        "commission": {
            "commission_rates": {
                "rate": "1.00000000",
                "max_rate": "1.00000000",
                "max_change_rate": "0.00000000"
            },
            "update_time": "1970-01-01T00:00:00Z"
        },
        "min_self_delegation": "1000.00000000"
    }
]
```



### 查询指定的一个validator的信息

http接口：

```http
GET okchain/v1/staking/validators/{validatorAddr}
```

接口参数：

| Name          | Type   | Required | Description                                                  |
| ------------- | ------ | -------- | ------------------------------------------------------------ |
| validatorAddr | string | true     | validator_address   eg: okchainvaloper10q0rk5qnyag7wfvvt7rtphlw589m7frs863s3m |

Response:

```
{
    "operator_address": "okchainvaloper10q0rk5qnyag7wfvvt7rtphlw589m7frs863s3m",
    "consensus_pubkey": "okchainvalconspub1zcjduepqqxsxcjjletkq40ypzuqz8n925pk0ycw9h8g4saw27adyf2t93szsvpk77u",
    "jailed": false,
    "status": 2,
    "tokens": "0",
    "delegator_shares": "1000.00000000",
    "description": {
        "moniker": "node0",
        "identity": "",
        "website": "",
        "details": ""
    },
    "unbonding_height": "0",
    "unbonding_time": "1970-01-01T00:00:00Z",
    "commission": {
        "commission_rates": {
            "rate": "1.00000000",
            "max_rate": "1.00000000",
            "max_change_rate": "0.00000000"
        },
        "update_time": "1970-01-01T00:00:00Z"
    },
    "min_self_delegation": "1000.00000000"
}
```



### 查询当前staking pool的资产情况

http接口：

```http
GET okchain/v1/staking/pool
```

接口参数：无

Response:

```
{
    "not_bonded_tokens": "0.00000000",
    "bonded_tokens": "1000.00000000"
}
```



### 查询staking的模块参数

http接口：

```http
GET okchain/v1/staking/parameters
```

接口参数：无

Response:

```
{
    "unbonding_time": "1209600000000000",
    "max_bonded_validators": 21,
    "bond_denom": "okt",
    "epoch": 252,
    "max_validators_to_vote": 30,
    "min_self_delegation": "0.00100000",
    "min_delegation": "0.00010000"
}
```

