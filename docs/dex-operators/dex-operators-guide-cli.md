# DEX Operators Guide (CLI)

在OKChain-OpenDEX中，任何用户都可以发行自己的Token和Tokenpair。

## cli command
staking cli contains the following 3 commands for DEX operator, providing complete support for equity circulation.

*  issue: issue token

*  list: list a token pair

*  deposit: deposit an amount of okt on a tokenpair

*  withdraw: withdraw an amount of okt from a tokenpair


### Issue token

任何用户都可以发行自己的Token，除了按gas收取的系统手续费之外，还会收取一部分OKT作为业务手续费。关于具体费率请参考[Fee Model]().

```shell
okchaincli tx token issue --from alice --symbol bcoin --total-supply 200000 --whole-name 'bcoin' --desc 'blockchain coin' -b block --mintable  

```

* symbol ：symbol is a non-case-sensitive token ticker limited to 6 alphanumeric characters, but the first character cannot be a number, eg. “bcoin” since the system will automatically add 3 random characters, such as "bcoin-gf6"
* whole-name ：full token name
* desc ：token description limited to 256 bytes
* total-supply ：total token supply
* mintable ：indicate whether to increase the supply of tokens



### List a tokenpair

任何用户都可以发行Tokenpair成为DEX operator，在OpenDEX中，任意两个Token都可以组成一个且只能组成一个Tokenpair。

```shell
okchaincli tx dex list --base-asset tusdk-9a2 --quote-asset tbtc-965 --from mykey -b block -y

```
  
* base-asset ：base-asset should be issued before listed to opendex (default "btc")
* from ：Name or address of private key with which to sign
* init-price ：init-price should be valid price (default "0.01")
* quote-asset ：quote-asset should be issued before listed to opendex (default "okt")


### Deposit an amount of okt on a tokenpair

为了公平，开放的使用区块链的撮合资源，OpenDEX采用竞价排名的方式分配系统资源，DEX可以通过添加[**数字资产撮合金**]()，使自己交易对的撮合被优先处理。


```shell
    okchaincli tx dex deposit tusdk-9a2_tbtc-965 100tokt --from mykey -b block -y
```



### Withdraw an amount of okt from a tokenpair

相对的，DEX operator也可以赎回自己的撮合金，赎回的部分会延迟2周到账。


```shell
    okchaincli tx dex withdraw tusdk-9a2_tbtc-965 50okt --from mykey -b block -y
```
