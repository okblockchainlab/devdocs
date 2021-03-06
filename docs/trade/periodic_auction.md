# 撮合系统

## 背景


DEX撮合系统采用的是集合竞价模型。由于在区块链系统中，订单不是连续产生的，而是按出块时间间隔离散地产生，
因而DEX不像大多数中心化交易所对订单采用连续竞价算法，而是按照出块时间间隔，
周期性地以集中竞价的方式对订单进行撮合。

每个区块采用集合竞价的方式，保证一个数字资产交易对在一个区块内只会有一个成交价，成交时按"价格优先，时间优先"的顺序成交，
可以大大弱化交易在区块内的排序对最终撮合结果的影响，增加矿工预先交易的难度，并减少矿工预先交易带来的收益，
从而保证交易的公平性。

## 撮合流程

![match](../../img/match.png)

## 基准价格选取算法

* 规则0：最佳出价<最佳询价，无可成交订单，不撮合；

* 规则1：最大成交量原则。以基准价格成交时，可以获得最大的成交量，如果多个价格都能满足最大成交量，则进入下一步；

* 规则2：最小过剩原则。过剩指的是当前价位的累计买单总量与累计卖单总量之差。最小过剩原则，指的是从满足规则1的价格中选取过剩值的绝对值最小的价格。如果满足此规则的价格有多个，则进入下一步。

* 规则3：市场压力原则。同时满足规则1和规则2的价格有多个时（最大值为max，最小值为min）。则需要确定潜在价格的市场压力的位置。过剩全为正号，表示买多卖少，为买方压力；过剩全为负号，表示买少卖多，为卖方压力；过剩有正有负，则无明显买卖方压力。
按以下规则确定参考价（ref）。如果ref在\[min, max\]区间内，则选取ref作为基准价格；如果ref在\[min, max\]区间外，则选取最接近ref的min或者max作为基准价格。
    
    * 规则3a：如果过剩全为正数，买方压力。以上次成交价的105%作为参考价。
    
    * 规则3b：如果过剩全为负数，卖方压力。以上次成交价的95%作为参考价。
    
    * 规则3c：如果过剩有正有负，则无明显买卖方压力。以最近成交价作为参考价。

![matchPrice](../../img/matchPrice.png)

## 以基准价格作为成交价撮合


所有的买委托按照委托限价由高到低的顺序排列，所有的卖委托按照委托限价由低到高的顺序排列，
价格相同的委托按时间（区块高度，区块内tx顺序）先后排序，时间较早的订单排在前面。

基准价格选定之后，按照最大成交量，依序逐笔将排在前面的买委托与卖委托成交，即按照 “价格优先，同等价格下时间优先”的成交顺序
依次成交，直至完成最大成交量。所有成交都以同一基准价格成交。


## 基准价格算法示例


选取的基准价格用*表示。

可成交量=MIN(累计卖单量,累计买单量)

未成交量（过剩）=累计买单量-累计卖单量

以下案例的价格最小精度均为0.1。


示例1：最大成交量原则（规则1）

| 累计卖单量 | 申报卖单量 | 申报价格 | 申报买单量 | 累计买单量 | 可成交量 | 未成交量 |
|------------|------------|----------|------------|------------|----------|----------|
| 3          |            | 1.0      | 2          | 2          | 2        |          |
| 3          | 2          | 0.8*     | 2          | 4          | 3        |          |
| 1          | 1          | 0.7      |            | 4          | 1        |          |

示例2：最小过剩原则（规则2）

| 累计卖单量 | 申报卖单量 | 申报价格 | 申报买单量 | 累计买单量 | 可成交量 | 未成交量 |
|------------|------------|----------|------------|------------|----------|----------|
| 12         |            | 1.2      | 2          | 2          | 2        |          |
| 12         |            | 1.1      | 2          | 4          | 4        |          |
| 12         |            | 0.9      | 5          | 9          | 9        | -3       |
| 12         | 2          | 0.8      |            | 9          | 9        | -3       |
| 10         | 5          | 0.7*     |            | 9          | 9        | -1       |
| 5          |            | 0.6      | 2          | 11         | 5        |          |
| 5          | 5          | 0.5      |            | 11         | 5        |          |

示例3：市场压力原则。买方压力（规则3a）。最近成交价10.0，参考价为10.0*1.05=10.5。基准价为10.4

| 累计卖单量 | 申报卖单量 | 申报价格 | 申报买单量 | 累计买单量 | 可成交量 | 未成交量 |
|------------|------------|----------|------------|------------|----------|----------|
| 5          |            | 10.4*    | 6          | 6          | 5        | 1        |
| 5          | 3          | 10.3     |            | 6          | 5        | 1        |
| 2          | 2          | 9.9      |            | 6          | 2        |          |

示例4：市场压力原则。买方压力（规则3a）。最近成交价10.0，参考价为10.0*1.05=10.5。基准价为10.5

| 累计卖单量 | 申报卖单量 | 申报价格 | 申报买单量 | 累计买单量 | 可成交量 | 未成交量 |
|------------|------------|----------|------------|------------|----------|----------|
| 5          |            | 10.8     | 6          | 6          | 5        | 1        |
| 5          | 3          | 10.3     |            | 6          | 5        | 1        |
| 2          | 2          | 9.9      |            | 6          | 2        |          |


示例5：市场压力原则。卖方压力（规则3b）。最近成交价10.0，参考价为10.0*0.95=9.5。基准价为9.6

| 累计卖单量 | 申报卖单量 | 申报价格 | 申报买单量 | 累计买单量 | 可成交量 | 未成交量 |
|------------|------------|----------|------------|------------|----------|----------|
| 6          |            | 10.1     | 2          | 2          | 2        |          |
| 6          |            | 9.7      | 3          | 5          | 5        | -1       |
| 6          | 6          | 9.6*     |            | 5          | 5        | -1       |

示例6：市场压力原则。卖方压力（规则3b）。最近成交价10.0，参考价为10.0*0.95=9.5。基准价为9.5

| 累计卖单量 | 申报卖单量 | 申报价格 | 申报买单量 | 累计买单量 | 可成交量 | 未成交量 |
|------------|------------|----------|------------|------------|----------|----------|
| 6          |            | 10.1     | 2          | 2          | 2        |          |
| 6          |            | 9.7      | 3          | 5          | 5        | -1       |
| 6          | 6          | 9.4      |            | 5          | 5        | -1       |

示例7：市场压力原则。无明显买卖方压力（规则3c）。最近成交价10.0，参考价10.0，基准价为10.0

| 累计卖单量 | 申报卖单量 | 申报价格 | 申报买单量 | 累计买单量 | 可成交量 | 未成交量 |
|------------|------------|----------|------------|------------|----------|----------|
| 5          |            | 10.2     | 2          | 2          | 5        | -3       |
| 5          | 3          | 10.0*    |            | 2          | 5        | -3       |
| 2          |            | 9.8      | 3          | 5          | 5        | 3        |
| 2          | 2          | 9.4      |            | 5          | 5        | 3        |

示例7：市场压力原则。无明显买卖方压力（规则3c）。最近成交价10.5，参考价10.5，基准价为10.2

| 累计卖单量 | 申报卖单量 | 申报价格 | 申报买单量 | 累计买单量 | 可成交量 | 未成交量 |
|------------|------------|----------|------------|------------|----------|----------|
| 5          |            | 10.2*    | 2          | 2          | 5        | -3       |
| 5          | 3          | 10.0     |            | 2          | 5        | -3       |
| 2          |            | 9.8      | 3          | 5          | 5        | 3        |
| 2          | 2          | 9.4      |            | 5          | 5        | 3        |
