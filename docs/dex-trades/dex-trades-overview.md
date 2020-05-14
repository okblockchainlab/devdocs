# DEX Traders Overview

## Introduction

在OKChain-OpenDEX中，希望进行币币交换的用户称之为 DEX Traders。

OKChain-OpenDEX, as the first project of the OKChain ecosystem, is a middleware that can freely issue DEX. With the design concept of "everyone can create DEX", it provides various basic functions needed to operate a DEX. 

validators提供了OKChain所需要的机器配置，DEX Operators提供了tokenpair，DEX Trader才可以实现币币交换的功能。


## 获取行情信息

OKChian-OpenDEX提供了基础的功能，订单和撮合都是在链上发生的，但是仅有这些还不够，交易用户需要使用更友好的UI页面以帮助自己的交易决策。
关于这一部分程序建设是由OKChain-OpenDEX生态的其他项目负责解决的，我们提供了一个关于数据展示的[模板](https://www.okex.com/dex-test)。
但同时，OKChain本身也是开源的项目，任何人都可以开发自己的一套工具用于帮助DEX Trade进行更好的交易决策。

## 关于竞价撮合

For a practical guide on matching engine , click [periodic auction](../concepts/periodic-auction.md).

## 交易

For a practical guide on how to trade on okchain , click [DEX Traders Guide (CLI)](../dex-trades/dex-trades-guide-cli.md).