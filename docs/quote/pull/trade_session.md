---
id: quote_trade_session
title: 获取各市场当日交易时段
slug: quote-trade-session
sidebar_position: 15
---

### 介绍：
    获取各市场当日交易时段
### 协议指令：
    8
### 响应
* 参数

| 名称 | 类型   | 描述  | 
|-------|-------|-----|
|market_trade_session|object[]| 市场交易时段 |
|∟market|string| 市场。US/SG/HK/CN|
|∟trade_session|object[]| 交易时段 |
|∟∟beg_time|string| 交易开始时间。格式：hhmm 例：900|
|∟∟end_time|string| 交易结束时间。格式：hhmm 例：1400|
|∟∟trade_session|[TradeSession](../quote-object#tradesession)| 交易时段 |

* proto
```
message MarketTradePeriodResponse {
  repeated MarketTradePeriod market_trade_session = 1;
}

message MarketTradePeriod {
  string market = 1;
  repeated TradePeriod trade_session = 2;
}

message TradePeriod {
  int32 beg_time = 1;
  int32 end_time = 2;
  int32 trade_session = 3;
}
```
### 接口限制
每秒平均请求次数 10。瞬时并发次数 5。

### 错误码

| 协议错误码 | 业务错误码   | 描述  | 排查建议 |
|-------|-------|-----|----|
|3 | 301600| 无效的请求 | 请求参数有误或解包失败 |
|3 | 301606| 限流 | 降低请求频次 |
|7 | 301602| 服务端内部错误 ||

