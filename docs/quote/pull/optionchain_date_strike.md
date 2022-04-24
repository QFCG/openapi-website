---
id: quote_optionchain_date_strike
title: 获取标的的期权链到期日期权标的列表
slug: quote-optionchain-date-strike
sidebar_position: 12
---

### 介绍：
    获取标的的期权链到期日期权标的列表
### 协议指令：
    21
### 请求
* 参数

| 名称 | 类型   | 必须  | 描述      |  默认值  |  示例   |
|-------|-------|-----|---------|-----|----|
| symbol | string   | 是  | 标的代码。ticker.region。  | | 00700.HK|
| expiry_date | string   | 是  | [期权到期日](./quote-optionchain-date)。格式：YYMMDD  | | 20220404|

* proto
```
message OptionChainDateStrikeInfoRequest {
  string symbol = 1;
  string expiry_date = 2;
}
```
### 响应
* 参数

| 名称 | 类型   | 描述  | 
|-------|-------|-----|
|strike_price_info|object[]| 到期日期权标的列表 |
|∟price|string| 行权价 |
|∟call_symbol|string|call 期权标的代码 |
|∟put_symbol|string|put 期权标的代码 |
|∟standard|string| 是否标准期权 |

* proto
```
message OptionChainDateStrikeInfoResponse {
  repeated StrikePriceInfo strike_price_info = 1;
}

message StrikePriceInfo {
  string price = 1;
  string call_symbol = 2;
  string put_symbol = 3;
  bool  standard = 4;
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
|7 | 301600| 请求数据非法 | 检查请求的 symbol，expiry_date 数据格式 |