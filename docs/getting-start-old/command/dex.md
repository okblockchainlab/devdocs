# dex

dex模块支持运营方发行和管理数字资产交易对，包括增加和赎回撮合金

```bash
okchaincli tx dex 
```

二级子命令主要包含以下几个功能



### 发行数字资产交易对

```shell
okchaincli tx dex list -h
List a trading pair:

$ okchaincli tx dex list --base-asset mytoken --quote-asset okt --from mykey

Usage:
  okchaincli tx dex list [flags]

```

##### 示例

执行命令`okchaincli tx dex list --base-asset tusdk-9a2 --quote-asset tbtc-965 --from mykey -b block -y`

##### 成功返回：

```json
{
  "height": "23969",
  "txhash": "A7F23408B60741CB30834C70D528111D6C02363030BEA5128A3F94DC9B0DC2FA",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":null}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": null
    }
  ],
  "events": [
    {
      "type": "message",
      "attributes": [
        {
          "key": "sender",
          "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
        },
        {
          "key": "list-asset",
          "value": "tusdk-9a2"
        },
        {
          "key": "quote-asset",
          "value": "tbtc-965"
        },
        {
          "key": "init-price",
          "value": "0.01000000"
        },
        {
          "key": "max-price-digit",
          "value": "8"
        },
        {
          "key": "max-size-digit",
          "value": "8"
        },
        {
          "key": "min-trade-size",
          "value": "0.00000001"
        },
        {
          "key": "delisting",
          "value": "false"
        },
        {
          "key": "fee",
          "value": "20000.00000000okt"
        },
        {
          "key": "action",
          "value": "list"
        },
        {
          "key": "sender",
          "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
        }
      ]
    },
    {
      "type": "transfer",
      "attributes": [
        {
          "key": "recipient",
          "value": "okchain17xpfvakm2amg962yls6f84z3kell8c5ljresa7"
        },
        {
          "key": "amount",
          "value": "19999.98750000okt"
        },
        {
          "key": "recipient",
          "value": "okchain17xpfvakm2amg962yls6f84z3kell8c5ljresa7"
        },
        {
          "key": "amount",
          "value": "0.01250000okt"
        }
      ]
    }
  ]
}
```



### 增加数字资产交易对撮合金

```shell
okchaincli tx dex deposit -h
Deposit an amount of token on a product:

$ okchaincli tx dex deposit mytoken_okt 1000okt --from mykey

The 'product' is a trading pair in full name of the tokens: ${base-asset-symbol}_${quote-asset-symbol}, for example 'mytoken_okt'.

Usage:
  okchaincli tx dex deposit [product] [amount] [flags]

Flags:
      --from string             Name or address of private key with which to sign
  -h, --help                    help for deposit
      --indent                  Add indent to JSON response
      --ledger                  Use a connected Ledger device
      --memo string             Memo to send along with transaction
      --node string             <host>:<port> to tendermint rpc interface for this chain (default "tcp://localhost:26657")
      --sequence uint           The sequence number of the signing account (offline mode only)
      --trust-node              Trust connected full node (don't verify proofs for responses) (default true)
  -y, --yes                     Skip tx broadcasting prompt confirmation
```

##### 示例

 ` okchaincli tx dex deposit tusdk-9a2_tbtc-965 100tokt --from mykey -b block -y`

##### 成功返回

```json
{
  "height": "23971",
  "txhash": "53C955AD93DA4F287E4100709CE848571B387114E69F0B58DFEDB6A3A2C9E804",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":null}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": null
    }
  ],
  "events": [
    {
      "type": "message",
      "attributes": [
        {
          "key": "sender",
          "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
        },
        {
          "key": "module",
          "value": "dex"
        },
        {
          "key": "action",
          "value": "deposit"
        },
        {
          "key": "fee",
          "value": "0.01250000okt"
        },
        {
          "key": "sender",
          "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
        }
      ]
    },
    {
      "type": "transfer",
      "attributes": [
        {
          "key": "recipient",
          "value": "okchain1n58mly6f7er0zs6swtetqgfqs36jaarqeyvmcp"
        },
        {
          "key": "amount",
          "value": "100.00000000okt"
        },
        {
          "key": "recipient",
          "value": "okchain17xpfvakm2amg962yls6f84z3kell8c5ljresa7"
        },
        {
          "key": "amount",
          "value": "0.01250000okt"
        }
      ]
    }
  ]
}
```



### 提取数字资产交易对撮合金

```shell
okchaincli tx dex  withdraw -h
Withdraw an amount of token from a product:

$ okchaincli tx dex withdraw mytoken_okt 1000okt --from mykey

The 'product' is a trading pair in full name of the tokens: ${base-asset-symbol}_${quote-asset-symbol}, for example 'mytoken_okt'.

Usage:
  okchaincli tx dex withdraw [product] [amount] [flags]

Flags:

      --from string             Name or address of private key with which to sign
  -h, --help                    help for withdraw
      --indent                  Add indent to JSON response
      --ledger                  Use a connected Ledger device
      --memo string             Memo to send along with transaction
      --node string             <host>:<port> to tendermint rpc interface for this chain (default "tcp://localhost:26657")
      --sequence uint           The sequence number of the signing account (offline mode only)
      --trust-node              Trust connected full node (don't verify proofs for responses) (default true)
  -y, --yes                     Skip tx broadcasting prompt confirmation
```

##### 示例

`okchaincli tx dex withdraw tusdk-9a2_tbtc-965 50okt --from mykey -b block -y`

##### 成功返回

```json
{
  "height": "23973",
  "txhash": "F956635818FF01FD243749879A86F5A844D0D21874B662FFFC3D1C8ED265164D",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":null}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": null
    }
  ],
  "events": [
    {
      "type": "message",
      "attributes": [
        {
          "key": "module",
          "value": "dex"
        },
        {
          "key": "action",
          "value": "withdraw"
        },
        {
          "key": "fee",
          "value": "0.01250000okt"
        },
        {
          "key": "sender",
          "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
        }
      ]
    },
    {
      "type": "transfer",
      "attributes": [
        {
          "key": "recipient",
          "value": "okchain17xpfvakm2amg962yls6f84z3kell8c5ljresa7"
        },
        {
          "key": "amount",
          "value": "0.01250000okt"
        }
      ]
    }
  ]
}
```



### dex运营方转移交易对的所有权

我们支持将交易对的所有者转移给另外一个人。为了保证转交易所有权时的安全性，必须通过多签才可以进行交易对所有权的转移，具体分成以下四步：

#### 原owner(from)生成未签名的tx：

##### 示例

`okchaincli tx dex transfer-ownership [flags]`

##### 成功返回

```json
# from alice to jack
okchaincli tx dex transfer-ownership --from okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya --to okchain1eh7953xgu526hfjnyfpkdxrn78746gusg29pmy --product eox-22d_okt > unsignedTx.json

# unsignedTx.json
{
    "type":"cosmos-sdk/StdTx",
    "value":{
        "msg":[
            {
                "type":"dex/MsgTransferOwnership",
                "value":{
                    "from_address":"okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
                    "to_address":"okchain1eh7953xgu526hfjnyfpkdxrn78746gusg29pmy",
                    "product":"eox-22d_okt",
                    "to_signature":{
                        "pub_key":null,
                        "signature":null
                    }
                }
            }
        ],
        "signatures":null,
        "memo":""
    }
}
```

#### 转移的owner(to)来签名

#####示例：

`okchaincli tx dex multisign unsignedTx.json`

##### 成功返回：

```json
okchaincli tx dex multisign --from okchain1eh7953xgu526hfjnyfpkdxrn78746gusg29pmy unsignedTx.json > signedTx1.json -y

# signedTx1.json
{
    "type":"cosmos-sdk/StdTx",
    "value":{
        "msg":[
            {
                "type":"dex/MsgTransferOwnership",
                "value":{
                    "from_address":"okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
                    "to_address":"okchain1eh7953xgu526hfjnyfpkdxrn78746gusg29pmy",
                    "product":"eox-22d_okt",
                    "to_signature":{
                        "pub_key":{
                            "type":"tendermint/PubKeySecp256k1",
                            "value":"AwsiTrrGe4G0gDJj8u8T5s5ik65WmwgR+qdeepx9R4qg"
                        },
                        "signature":"mgf3IxbttnNjel2ZCAxoqIKPX2oqU8YcZxW6fcgGD5o+kDEqBP+LewHtdZf9UIUA1/GVSkzjtG1JjiClDGvstQ=="
                    }
                }
            }
        ],
        "signatures":null,
        "memo":""
    }
}
```



#### 原owner(from)签名

##### 示例：

`okchaincli tx sign [flags]`

##### 成功返回：

```json
okchaincli tx sign --from alice signedTx1.json > signedTx.json -y

# signedTx.json
{
  "type": "cosmos-sdk/StdTx",
  "value": {
    "msg": [
      {
        "type": "dex/MsgTransferOwnership",
        "value": {
          "from_address": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya",
          "to_address": "okchain1eh7953xgu526hfjnyfpkdxrn78746gusg29pmy",
          "product": "eox-22d_okt",
          "to_signature": {
            "pub_key": {
              "type": "tendermint/PubKeySecp256k1",
              "value": "AwsiTrrGe4G0gDJj8u8T5s5ik65WmwgR+qdeepx9R4qg"
            },
            "signature": "mgf3IxbttnNjel2ZCAxoqIKPX2oqU8YcZxW6fcgGD5o+kDEqBP+LewHtdZf9UIUA1/GVSkzjtG1JjiClDGvstQ=="
          }
        }
      }
    ],
    "signatures": [
      {
        "pub_key": {
          "type": "tendermint/PubKeySecp256k1",
          "value": "AgYaL1tZ7ekqvweQhKojG8sDHUfN23qJWviAsTDIWvYU"
        },
        "signature": "82HJ0dHE1la3/fph1IDcl6Uarxi1lKOAIQ51Q6Z0YgBnilXPgGzy+9er+RQFnTZa2SG8cyTK6LWr8LyiGMTQWQ=="
      }
    ],
    "memo": ""
  }
}
```

#### 广播多签后的tx

##### 示例

`okchaincli tx broadcast signedTx.json`

##### 成功返回

```json
okchaincli tx broadcast signedTx.json -b block -y

# 示例
{
  "height": "54",
  "txhash": "54FB441E4589EE333663D4C9903FCFC3CE65FF614DC32B12CBB75867BE7C15B9",
  "raw_log": "[{\"msg_index\":\"0\",\"success\":true,\"log\":\"\"}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": [
        {
          "type": "message",
          "attributes": [
            {
              "key": "module",
              "value": "dex"
            },
            {
              "key": "fee",
              "value": "10okt"
            },
            {
              "key": "action",
              "value": "transferOwnership"
            }
          ]
        }
      ]
    }
  ]
}
```

必须由原owner(from)和转移后的owner(to)共同签名才可以成功转移Token的所有权。

### 社区Validator 发起下架交易对对提案

社区有权利发起提案将运营方的数字资产交易对下架

```shell
okchaincli tx gov submit-proposal delist-proposal -h
Submit a dex delist proposal along with an initial deposit.
The proposal details must be supplied via a JSON file.

Example:
$ okchaincli tx gov submit-proposal delist-proposal <path/to/proposal.json> --from=<key_or_address>

Where proposal.json contains:

{
 "title": "delist xxx/okt",
 "description": "delist asset from dex",
 "base_asset": "xxx",
 "quote_asset": "okt",
 "deposit": [
   {
     "denom": "okt",
     "amount": "100"
   }
 ]
}

Usage:
  okchaincli tx gov submit-proposal delist-proposal [proposal-file] [flags]
```
#### 示例
`okchaincli tx gov submit-proposal delist-proposal ./proposal.json --from mykey -b block`

#### 成功返回

```json
{
  "height": "238",
  "txhash": "F3116C165ACF3F4F3D4E4643B04E7780490089246054D2CCAF8F1F5338C536A3",
  "data": "0101",
  "raw_log": "[{\"msg_index\":0,\"success\":true,\"log\":\"\",\"events\":null}]",
  "logs": [
    {
      "msg_index": 0,
      "success": true,
      "log": "",
      "events": null
    }
  ],
  "events": [
    {
      "type": "message",
      "attributes": [
        {
          "key": "sender",
          "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
        },
        {
          "key": "module",
          "value": "governance"
        },
        {
          "key": "sender",
          "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
        },
        {
          "key": "action",
          "value": "submit_proposal"
        },
        {
          "key": "fee",
          "value": "0.01250000okt"
        },
        {
          "key": "sender",
          "value": "okchain10q0rk5qnyag7wfvvt7rtphlw589m7frsmyq4ya"
        }
      ]
    },
    {
      "type": "proposal_deposit",
      "attributes": [
        {
          "key": "amount",
          "value": "100.00000000okt"
        },
        {
          "key": "proposal_id",
          "value": "1"
        }
      ]
    },
    {
      "type": "submit_proposal",
      "attributes": [
        {
          "key": "proposal_id",
          "value": "1"
        },
        {
          "key": "voting_period_start",
          "value": "1"
        }
      ]
    },
    {
      "type": "transfer",
      "attributes": [
        {
          "key": "recipient",
          "value": "okchain10d07y265gmmuvt4z0w9aw880jnsr700jccf4qs"
        },
        {
          "key": "amount",
          "value": "100.00000000okt"
        },
        {
          "key": "recipient",
          "value": "okchain17xpfvakm2amg962yls6f84z3kell8c5ljresa7"
        },
        {
          "key": "amount",
          "value": "0.01250000okt"
        }
      ]
    }
  ]
}
```



### 查询账户创建的交易对

如果不输入账户，则显示所有，通过`--owner`指定账户查询

通过`-p` (指定第几页)和`-i`（指定每页数量）进行分页查询。

  ```shell
  okchaincli query dex products -h
  Query the list of token pairs
  
  Usage:
    okchaincli query dex products [flags]
  
  Flags:
        --height int           Use a specific height to query state at (this can error if the node is pruning state)
    -h, --help                 help for products
        --indent               Add indent to JSON response
    -i, --items-per-page int   items per page (default 50)
        --ledger               Use a connected Ledger device
        --node string          <host>:<port> to Tendermint RPC interface for this chain (default "tcp://localhost:26657")
        --owner string         address of the product owner
    -p, --page-number int      page num (default 1)
        --trust-node           Trust connected full node (don't verify proofs for responses)
  ```

##### 示例

` okchaincli query dex products -p 1 -i 1`

##### 成功返回：

  ```json
  [
    {
      "base_asset_symbol": "xxb",
      "quote_asset_symbol": "okt",
      "price": "10.00000000",
      "max_price_digit": "8",
      "max_size_digit": "8",
      "min_trade_size": "0.00000000",
      "token_pair_id": "0",
      "delisting": false,
      "owner": "okchain1w7xcg4t90fxcpe95dzhykcvs9skzz2xsy60g3u",
      "deposits": {
        "denom": "okt",
        "amount": "100.00000000"
      },
      "block_height": "0"
    }
  ]
  ```



### 查询账户撮合金

查询某个账户中交易对的撮合金，返回交易对名称与撮合金数量

通过`-p` (指定第几页)和`-i`（指定每页数量）进行分页查询。

  ```shell
  okchaincli query dex deposits -h
  Query product deposits
  
  Usage:
    okchaincli query dex deposits [account-addr] [flags]
  
  Flags:
        --height int           Use a specific height to query state at (this can error if the node is pruning state)
    -h, --help                 help for deposits
        --indent               Add indent to JSON response
    -i, --items-per-page int   items per page (default 50)
        --ledger               Use a connected Ledger device
        --node string          <host>:<port> to Tendermint RPC interface for this chain (default "tcp://localhost:26657")
    -p, --page-number int      page num (default 1)
        --trust-node           Trust connected full node (don't verify proofs for responses)
  ```

#####  示例

`okchaincli query dex deposits okchain1w7xcg4t90fxcpe95dzhykcvs9skzz2xsy60g3u -i 1`

##### 成功返回

  ```json
[
    {
      "product": "xxb_okt",
      "deposits": [
        {
          "denom": "okt",
          "amount": "100.00000000"
        }
      ]
    }
  ]
  ```

  

### 查询所有交易对撮合顺序

查询交易对的撮合顺序，返回交易对名称即可

通过`-p` (指定第几页)和`-i`（指定每页数量）进行分页查询。

  ```shell
  okchaincli query dex match-order -h
  Query the match order of token pairs
  
  Usage:
    okchaincli query dex match-order [flags]
  
  Flags:
        --height int           Use a specific height to query state at (this can error if the node is pruning state)
    -h, --help                 help for match-order
        --indent               Add indent to JSON response
    -i, --items-per-page int   items per page (default 50)
        --ledger               Use a connected Ledger device
        --node string          <host>:<port> to Tendermint RPC interface for this chain (default "tcp://localhost:26657")
    -p, --page-number int      page num (default 1)
        --trust-node           Trust connected full node (don't verify proofs for responses)
  ```

##### 示例  

`okchaincli query dex match-order -i 1`

##### 成功返回

  ```json
  [
    "xxb_okt"
  ]
  ```

### 查询dex模块的相关参数

查询交易对的相关参数

  ```shell

	okchaincli query dex  params -h
	Query the all the parameters for the governance process:

	$ okchaincli query dex params

	Usage:
  		okchaincli query dex params [flags]
  ```

##### 示例  

`okchaincli query dex  params --node 127.0.0.1:26657`

##### 成功返回

  ```json
{
  "dex_list_fee": [
    {
      "denom": "okt",
      "amount": "20000.00000000"
    }
  ],
  "transfer_ownership_fee": [
    {
      "denom": "okt",
      "amount": "10.00000000"
    }
  ],
  "delist_max_deposit_period": "86400000000000",
  "delist_min_deposit": [
    {
      "denom": "okt",
      "amount": "100.00000000"
    }
  ],
  "delist_voting_period": "259200000000000",
  "withdraw_period": "259200"
}
  ```


### 查询所有处于下架状态中的交易对

查询所有处于下架状态中的交易对，返回币对名称即可

  ```shell

	Query all the products' names involved in dex delisting:

	$ okchaincli query dex products-delisting

	Usage:
  		okchaincli query dex products-delisting [flags]
  ```

##### 示例  

`okchaincli query dex  products-delisting --node 127.0.0.1:26657`

##### 成功返回

  ```json
  [
  	"tusdk-b72_tbtc-f6e"
  ]
  ```




