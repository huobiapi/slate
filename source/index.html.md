---
title: 火币 API 文档

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='https://www.hbg.com/zh-cn/apikey/'>创建 API Key </a>
includes:

search: true
---

# 更新日志

<style>
table {
    max-width:100%
}
table th {
    white-space: nowrap; /*表头内容强制在一行显示*/
}
</style>

| 生效时间<BR>(UTC +8) | 接口                                                         | 变化      | 摘要                                                         |
| -------------------- | ------------------------------------------------------------ | --------- | ------------------------------------------------------------ |
| 2020.11.26 19:00     | `GET /v2/user/uid`                                           | 新增      | 新增获取用户UID接口                                          |
| 2020.10.16 19:00     | `orders#${symbol}`                                           | 优化      | 订单创建事件新增accountId                                    |
| 2020.10.10 19:00     | `POST /v2/account/repayment`,<BR>`GET /v2/account/repayment` | 新增      | 新增通用还币接口及还币交易记录查询接口                       |
| 2020.8.28 19:00      | `GET /v1/common/symbols`                                     | 优化      | 新增API交易使能标记                                          |
| 2020.8.21 19:00      | `accounts.update#${mode}`, <BR>`accounts`                    | 优化      | 新增账户变更事件类型deposit，withdraw                        |
| 2020.8.11 19:00      | `GET /v1/common/symbols`,<BR> `GET /market/etp`, <BR>`market.$symbol.etp`,<BR> `GET /market/history/kline`, <BR>`market.$symbol$.kline.$period$`,<BR> `GET /v2/etp/reference`, <BR>`POST /v2/etp/creation`,<BR> `POST /v2/etp/redemption`,<BR> `GET /v2/etp/transactions`,<BR> `GET /v2/etp/transaction`, <BR>`GET /v2/etp/rebalance` | 新增+优化 | 新增/优化相关接口支持杠杆ETP                                 |
| 2020.8.10 19:00      | `GET v1/stable-coin/quote`, <BR>`POST v1/stable-coin/exchange` | 优化      | 新增稳定币兑换手续费字段                                     |
| 2020.8.4 19:00       | `GET /v1/account/history`                                    | 优化      | 新增返回字段“next-id”                                        |
| 2020.8.3 19:00       | `POST /v2/algo-orders`, <BR>`GET /v2/algo-orders/opening`, <BR>`GET /v2/algo-orders/history`, <BR>`GET /v2/algo-orders/specific` | 优化      | 新增追踪委托                                                 |
| 2020.7.24 19:00      | `trade.clearing#${symbol}#${mode}`                           | 优化      | 新增撤单推送                                                 |
| 2020.7.17 19:00      | `GET /v2/account/asset-valuation`                            | 新增      | 新增账户资产估值查询节点                                     |
| 2020.7.16 19:00      | `GET /v1/common/symbols`                                     | 优化      | 新增返回字段                                                 |
| 2020.7.10 19:00      | `GET /v2/point/account`,<BR> `POST /v2/point/transfer`       | 新增      | 新增点卡余额查询节点及点卡划转节点                           |
| 2020.7.10 19:00      | `POST /v1/order/batch-orders`                                | 优化      | 限频值调整                                                   |
| 2020.7.8 19:00       | `orders#{symbol}`                                            | 优化      | 新增两个事件类型                                             |
| 2020.6.27 19:00      | `GET /v2/market-status`                                      | 新增      | 新增市场状态查询节点                                         |
| 2020.6.27 19:00      | `market.$symbol.mbp.$levels`                                 | 优化      | 新增五档MBP逐笔增量订阅                                      |
| 2020.6.27 19:00      | 若干新增节点                                                 | 新增      | 新增策略委托相关节点                                         |
| 2020.6.24 19:00      | `GET /v1/order/orders/{order-id}/matchresults` <BR> `GET /v1/order/matchresults` | 优化      | 增加fee-currency字段                                         |
| 2020.6.24 19:00      | `GET /v2/account/withdraw/address`                           | 新增      | 提币地址查询                                                 |
| 2020.6.23 19:00      | 若干新增节点                                                 | 新增      | 新增C2C杠借币相关节点                                        |
| 2020.6.16 10:00      | `GET /v2/sub-user/user-list`,<BR> `GET /v2/sub-user/user-state`, <BR>`GET /v2/sub-user/account-list` | 新增      | 新增子用户列表查询、子用户状态查询、子用户账户查询接口       |
| 2020.6.15 19:00      | `POST /v2/sub-user/api-key-generation`,<BR>`POST /v2/sub-user/api-key-modification` | 优化      | 增加单用户可创建API Key数量以及增加单个API Key可绑定IP地址数量 |
| 2020.6.11 19:00      | `POST /v1/account/transfer`                                  | 优化      | 新增币币账户与逐仓杠杠账户的划转，逐仓杠杠账户内部的划转     |
| 2020.6.11 19:00      | `GET /v1/query/deposit-withdraw`                             | 优化      | 新增返回提币失败原因                                         |
| 2020.6.5 19:00       | `POST /v2/sub-user/api-key-generation`,<BR> `GET /v2/user/api-key`, <BR>`POST /v2/sub-user/api-key-modification`,<BR> `POST /v2/sub-user/api-key-deletion` | 新增      | 新增母子用户API key管理接口                                  |
| 2020.6.4 19:00       | 若干私有REST接口                                             | 优化      | 变更限频值                                                   |
| 2020.6.1 19:00       | `orders#${symbol}`                                           | 优化      | Taker订单成交前首推创建事件                                  |
| 2020.6.1 19:00       | `GET /v2/reference/transact-fee-rate`, <BR>`GET /v1/order/orders/{order-id}/matchresults`,<BR> `GET /v1/order/matchresults`, <BR>`trade.clearing#${symbol}`, <BR>`GET /v1/account/history`, <BR>`accounts`, `accounts.update#${mode}` | 优化      | 支持交易手续费返佣相关字段                                   |
| 2020.5.29 19:00      | `POST /v2/sub-user/tradable-market`                          | 新增      | 新增母用户设置子用户交易权限接口                             |
| 2020.5.29 19:00      | `POST /v2/sub-user/transferability`                          | 新增      | 新增母用户设置子用户资产转出权限接口                         |
| 2020.5.29 19:00      | `POST /v2/sub-user/creation`                                 | 新增      | 新增子用户创建接口                                           |
| 2020.5.29 19:00      | `POST /v1/account/transfer`                                  | 新增      | 新增通用资产划转接口                                         |
| 2020.4.28 11:00      | `market.$symbol.mbp.$levels` & `market.$symbol.mbp.refresh.$levels` | 优化      | 支持所有交易对                                               |
| 2020.4.27 11:00      | `orders#${symbol}`                                           | 优化      | 更改IOC订单的更新行为                                        |
| 2020.4.17 11:00      | `GET /v2/account/deposit/address`,<BR>`GET /v2/sub-user/deposit-address`,<BR>`GET /v1/query/deposit-withdraw`,<BR>`GET /v2/sub-user/query-deposit` | 新增      | 支持子用户充值                                               |
| 2020.4.3 11:00       | `orders#${symbol}`                                           | 新增      | 新增v2版本订单更新推送主题                                   |
| 2020.3.31 21:00      | `accounts.update#${mode}`                                    | 优化      | 订阅成功后首推各账户初始值                                   |
| 2020.3.31 11:00      | `GET /v2/account/ledger`                                     | 新增      | 新增财务流水查询接口                                         |
| 2020.3.30 19:00      | `market.$symbol.mbp.refresh.$levels`                         | 新增      | 新增MBP全量推送接口                                          |
| 2020.3.30 19:00      | `POST /v1/order/orders/place`,<BR>`POST /v1/order/batch-orders`,<BR>`GET /v1/order/openOrders`,<BR>`GET /v1/order/orders/{order-id}`,<BR>`GET /v1/order/orders/getClientOrder`,<BR>`GET /v1/order/orders/`<BR>`{order-id}/matchresults`,<BR>`GET /v1/order/orders`,<BR>`GET /v1/order/history`,<BR>`GET /v1/order/matchresults`,<BR>`orders.$symbol`,<BR>`trade.clearing#${symbol}`,<BR>`orders.$symbol.update` | 优化      | 增加FOK订单类型                                              |
| 2020.3.27 19:00      | `GET /v1/order/orders`<BR>`GET /v1/order/history`            | 优化      | 已完全撤销订单的可查询范围缩短为2小时                        |
| 2020.3.24 19:00      | `market.$symbol.mbp.$levels`                                 | 优化      | 增加可请求交易代码                                           |
| 2020.3.17 19:00      | `GET /v1/order/matchresults`                                 | 优化      | size取值上限由100上调至500                                   |
| 2020.3.12 19:00      | `GET /market/tickers`                                        | 优化      | 增加买一卖一字段                                             |
| 2020.3.5 19:00       | `GET /v1/fee/fee-rate/get`                                   | 删除      | 移除旧版费率查询接口                                         |
| 2020.3.2 11:00       | `GET https://status.huobigroup.com`<BR>`/api/v2/summary.json` | 新增      | 新增获取当前系统状态接口                                     |
| 2020.2.28 11:00      | 母子用户相关接口                                             | 优化      | 将文档中“母子账号”的称谓更改为“母子用户”                     |
| 2020.2.28 11:00      | `GET /v1/cross-margin/loan-orders`,<br>`GET /v1/cross-margin/accounts/balance` | 优化      | 新增可选请求参数                                             |
| 2020.2.28 11:00      | `GET /v1/subuser/aggregate-balance`,<br>`GET /v1/account/accounts/{sub-uid}` | 优化      | 新增账户类型字段枚举值                                       |
| 2020.2.28 11:00      | `POST /v1/cross-margin/transfer-in`,<br>`POST /v1/cross-margin/transfer-out`,<br>`GET /v1/cross-margin/loan-info`,<br>`POST /v1/cross-margin/orders`,<br>`POST /v1/cross-margin/orders/`<br>`{order-id}/repay`,<br>`GET /v1/cross-margin/loan-orders`,<br>`GET /v1/cross-margin/accounts/balance` | 优化      | 允许授权子用户调用该接口                                     |
| 2020.2.5 19:00       | `GET /v1/order/orders/{order-id}`,<BR>`GET /v1/order/orders/getClientOrder`,<BR>`GET /v1/order/openOrders`,<BR>`GET /v1/order/orders`,<BR>`GET /v1/order/history` | 优化      | 新增client-order-id字段                                      |
| 2020.2.5 19:00       | `GET /v1/order/orders`                                       | 优化      | 新增start-time/end-time请求参数                              |
| 2020.2.3 19:00       | `GET /v2/reference/transact-fee-rate`                        | 新增      | 新增交易手续费率查询节点                                     |
| 2020.2.3 19:00       | `GET /v2/reference/currencies`                               | 优化      | 增加底层链字段                                               |
| 2020.2.3 19:00       | `GET /v1/margin/loan-info`                                   | 优化      | 增加抵扣后实际币息率字段                                     |
| 2020.1.10 19:00      | `GET /v1/cross-margin/loan-info`                             | 优化      | 增加抵扣后实际币息率字段                                     |
| 2020.1.7 19:00       | `GET /v1/account/history`                                    | 优化      | 允许子用户调用此节点                                         |
| 2019.12.27 19:00     | `POST /v2/sub-user/management`                               | 新增      | 新增冻结/解冻子用户接口                                      |
| 2019.12.27 19:00     | `POST /v1/order/orders/batchcancel`                          | 优化      | 允许以client order ID为请求参数批量撤单                      |
| 2019.12.27 19:00     | `POST /v1/order/batch-orders`                                | 新增      | 新增批量下单节点                                             |
| 2019.12.23 15:00     | `market.$symbol.mbp.$levels`                                 | 新增      | 新增深度行情增量推送订阅主题                                 |
| 2019.12.05 11:00     | `trade.clearing#${symbol}` & `accounts.update#${mode}`       | 新增      | 新增v2版本资产及订单推送订阅主题                             |
| 2019.11.22 15:00     | `GET /v1/order/orders`<br />`GET /v1/order/history`          | 优化      | 已完全撤销的历史订单可查询时间范围缩短为最近1天              |
| 2019.11.13 19:00     | `GET /v1/margin/loan-info`<br />`GET /v1/cross-margin/loan-info` | 新增      | 新增借币币息及额度查询节点                                   |
| 2019.11.08 19:45     | `GET /v1/order/orders/{order-id}/matchresult`<br />`GET /v1/order/matchresults` | 新增      | 新增返回字段trade-id                                         |
| 2019.10.18 19:00     | `GET /v1/account/history`                                    | 新增      | 新增账户流水查询节点                                         |
| 2019.10.12 11:00     | `POST /v1/dw/withdraw/api/create`                            | 优化      | 设置ERC20为USDT的默认链                                      |
| 2019.10.11 10:00     | 支持全仓杠杆资产划转、借币、还币、查询借币订单、查询账户余额等相关节点 | 新增      | 新增全仓杠杆相关节点                                         |
| 2019.10.09 20:00     | `GET /market/trade`<br />`GET /market/history/trade`<br />`market.$symbol.trade.detail` | 优化      | 新增返回字段trade id                                         |
| 2019.09.25 20:00     | `GET /v2/account/withdraw/quota`                             | 新增      | 新增提币额度查询节点                                         |
| 2019.09.23 15:00     | `POST /v1/order/orders/`<BR>`{order-id}/submitcancel` <br />`POST /v1/order/orders/batchcancel` | 优化      | 优化错误码返回                                               |
| 2019.09.20 10:00     | `GET /v2/reference/currencies`                               | 新增      | 新增币链参考信息节点                                         |
| 2019.09.19 16:00     | `market.$symbol.bbo`                                         | 新增      | 新增买一卖一逐笔推送                                         |
| 2019.09.18 20:00     | `GET /v1/subuser/aggregate-balance`<br />`GET /v1/account/accounts/{sub-uid}`<br />`GET /v1/margin/loan-orders`<br />`GET /v1/margin/accounts/balance` | 新增      | 支持子用户逐仓杠杆交易                                       |
| 2019.09.16 15:00     | `GET /v2/account/deposit/address`                            | 新增      | 新增APIv2节点 - 充币地址查询                                 |
| 2019.09.11 17:00     | `GET /v1/stable-coin/quote`<br />`POST /v1/stable-coin/exchange` | 新增      | 新增稳定币兑换节点                                           |
| 2019.09.11 16:00     | 删除部分代码示例                                             | 删除      | 删除部分代码示例                                             |
| 2019.09.10 10:00     | 除了`POST /v1/order/orders/submitCancelClientOrder` <BR> `GET /v1/order/openOrders`<BR>之外其他订单相关API | 修改      | 除节点"POST /v1/order/orders/submitCancelClientOrder" & "GET /v1/order/openOrders"以外，去除了其它节点中订单状态取值submitting以及cancelling |
| 2019.09.09 11:00     | `POST /v1/order/orders/submitCancelClientOrder`              | 修改      | 修改返回数据描述                                             |
| 2019.09.09 10:00     | `GET /v1/order/orders`<br />`GET /v1/order/matchresults`     | 修改      | 修改请求字段start-date与end-date的默认值及取值范围的描述     |
| 2019.09.02 18:00     | `POST /v1/order/orders/batchCancelOpenOrders`                | 优化      | 更改请求字段"symbol"的描述                                   |
| 2019.09.02 16:00     | 删除稳定币兑换相关节点。                                     | 删除      |                                                              |
| 2019.08.29 21:00     | 下单、查询、订阅接口                                         | 新增      | 支持止盈止损订单类型。                                       |
| 2019.08.21 18:00     | `GET /v1/order/openOrders`                                   | 优化      | 修改请求字段列表。                                           |
| 2019.08.05 18:00     | `orders.$symbol.update`                                      | 新增      | 新增字段"client-order-id"和"order-type"。                    |
| 2019.08.02 18:00     | `orders.$symbol.update`                                      | 优化      | 修改对字段"unfilled-amount"的描述。                          |
| 2019.07.23 21:00     | `GET /v1/order/orders/{order-id}/matchresult`<br>`GET /v1/order/matchresults` | 新增      | 新增手续费抵扣详情字段。                                     |
| 2019.07.23 20:00     | `GET /v1/fee/fee-rate/get`                                   | 新增      | 新增费率查询接口。                                           |
| 2019.07.22 12:00     | `GET /v1/order/orders/{order-id}/matchresults`<br/>`GET /v1/order/matchresults` | 新增      | 新增成交角色"role"字段以标识每笔成交角色是"taker"还是"maker"。 |
| 2019.07.11 20:00     | `POST /v1/order/orders/place`<br/>`POST /v1/order/orders/submitCancelClientOrder`<br/>`GET /v1/order/orders/getClientOrder` | 优化/新增 | 下单/撤单/查询可基于client order ID。                        |
| 2019.07.08 12:00     | Websocket 订单资产推送接口                                   | 优化      | 优化Websocket 订单资产推送接口[心跳和限频](#5ea2e0cde2-3)。  |
| 2019.06.14 16:00     | `POST /v1/dw/withdraw/api/create`                            | 优化      | 支持快速提币                                                 |
| 2019.06.17 16:00     | `GET /v1/stable_coin/exchange_rate`<br/>`POST /v1/stable_coin/exchange` | 新增      | 新增接口支持用户随时获取最新的稳定币兑换汇率信息，并对稳定币执行兑入或兑出。 |
| 2019.06.12 16:00     | `GET /v1/common/symbols`                                     | 优化      | 对交易对基础信息接口返回的内容进行优化，该优化向后兼容       |
| 2019.06.06 18:00     | `GET /v1/query/deposit-withdraw`                             | 优化      | 对充提记录查询接口的请求参数进行优化，该优化向后兼容         |
| 2019.06.05 20:00     | 所有需要验签的接口                                           | 优化      | 访问验签接口时，API Key需要有适当的权限，现有的API Key都默认有全部权限。权限分为3类：读取，交易和提币。每个接口相应的权限类别均已更新在各接口说明中 |
| 2019.06.10 00:00     | `GET /v1/order/orders`<br/>`GET /v1/order/matchresults`      | 修改      | 查询窗口调整为48小时，可查询整体时间范围不变                 |
| 2019.05.15 10:00     | `POST /v1/futures/transfer`                                  | 新增      | 提供币币与合约账户间的资产划转                               |
| 2019.04.29 19:00     | `GET /v1/order/history`                                      | 新增      | 新增最近48小时内历史订单查询节点。新节点的上线后，现有订单查询节点“GET /v1/order/orders”仍将被保留。然而，新节点“GET /v1/order/history”被赋予更高服务等级。极端情况下，当服务荷载超过系统既定阈值时，节点“GET /v1/order/orders”的服务可能会不可用，而新节点“GET /v1/order/history”仍将继续提供服务。另外，火币正在计划支持另一个新节点专门用于用户48小时外的历史订单查询。此新节点上线的同时，现有节点“GET /v1/order/orders”将被弃用。火币将及时告知用户这一变更，一旦变更时间确定。 |
| 2019.04.17 10:00     | `GET /v1/order/orders`                                       | 修改      | 文档优化，增加Start-date限制说明                             |
| 2019.04.16 10:00     | `GET /v1/order/openOrders`                                   | 修改      | 文档错误，参数account-id和symbol都是必填参数                 |
| 2019.01.17 07:00     | Websocket accounts                                           | 修改      | 增加订阅参数 model；<br>订阅返回的内容中不再推送交易子账户冻结余额的变化。 |
| 2018.07.10 11:00     | `GET /market/history/kline`                                  | 修改      | `size` 取值范围由 [1-1000] 修改为 [1-2000]。                 |
| 2018.07.06 16:00     | `POST /v1/order/orders/place`                                | 修改      | 添加 `buy-limit-maker`，`sell-limit-maker` 两种下单类型支持；<br>新增获取某个帐号下指定交易对或者所有交易对的所有尚未成交订单接口: `/v1/order/openOrders`。 |
| 2018.07.06 16:00     | `GET /v1/order/openOrders`<br/>`POST /v1/order/orders/batchCancelOpenOrders` | 新增      | 新增获取某个帐号下指定交易对或者所有交易对的所有尚未成交订单接口；<br>新增批量取消某个帐号下指定的订单列表中所有订单接口。 |
| 2018.07.02 16:00     | ETF 相关接口                                                 | 新增      | 本次接口变更主要是支持 HB10 ETF 的换入和换出。               |
| 2018.06.20 16:00     | `GET /market/tickers`                                        | 新增      | 新增 Tickers 接口，Tickers 为当前所有交易对行情数据。        |

# 简介

## API 简介

欢迎使用火币 API！  

此文档是火币API的唯一官方文档，火币API提供的功能和服务会在此持续更新，请大家及时关注。  

你可以通过点击上方菜单来切换获取不同业务的API，还可通过点击右上方的语言按钮来切换文档语言。  

文档右侧是请求参数以及响应结果的示例。

## 更新订阅

关于API新增、更新、下线等信息火币会提前发布公告进行通知，建议您关注和订阅我们的公告，及时获取相关信息。  

您可以点击 <a href='https://huobiglobal.zendesk.com/hc/zh-cn/sections/360000070201-API-%E5%85%AC%E5%91%8A'>这里 </a> 订阅公告。

订阅流程为：点击“API公告”右上角“关注”按钮，用账号登录成功后，再次点击“关注”按钮，并选择需要关注的内容类型，按钮变为“正在关注”，即表示订阅成功。若无账号，点击弹窗左下角“注册”按钮，进行注册。

## 做市商项目

欢迎有优秀 maker 策略且交易量大的用户参与长期做市商项目。如果您的火币现货账户或者合约账户中有折合大于10BTC资产（币币和合约账户分开统计），请提供以下信息发送邮件至：

- [MM_service@huobi.com](mailto:MM_service@huobi.com) Huobi Global（现货 / 杠杆）做市商申请；
- [dm_mm@huobi.com](mailto:dm_mm@huobi.com) HBDM（合约）做市商申请。

1. 提供 UID （需不存在返佣关系的 UID）；
2. 提供其他交易平台 maker 交易量截图证明（比如30天内成交量，或者 VIP 等级等）；
3. 请简要阐述做市方法，不需要细节。 

<aside class="notice">
做市商项目不支持点卡抵扣、VIP、交易量相关活动以及任何形式的返佣活动。
</aside>

## 联系我们

使用过程中如有问题或者建议，您可选择以下任一方式联系我们：

- 加入官方QQ群（Huobi Global Spot API交流群 1160839820），入群申请请注明UID和编程语言。
- 通过官网的“帮助中心”或者发送邮件至support@huobigroup.com联系客服。

如您遇到API错误，请按照如下模板向我们反馈问题。

`1. 问题描述`  
`2. 问题发生的用户Id(UID)，账户Id和订单Id(如果和账户、订单有关系)`  
`3. 完整的URL请求`  
`4. 完整的JSON格式的请求参数（如果有）`  
`5. 完整的JSON格式的返回结果`  
`6. 问题出现时间和频率（如何时开始出现，是否可以重现）`  
`7. 签名前字符串（如果是签名认证错误）`  

下方是一个应用了模版的例子：

`1. 问题简要说明：签名错误`   
`2. UID：123456`  
`3. 完整的URL请求：GET https://api.huobi.pro/v1/account/accounts?&SignatureVersion=2&SignatureMethod=HmacSHA256&Timestamp=2019-11-06T03%3A25%3A39&AccessKeyId=rfhxxxxx-950000847-boooooo3-432c0&Signature=HhJwApXKpaLPewiYLczwfLkoTPnFPHgyF61iq0iTFF8%3D`  
`4. 完整的JSON格式的参数：无`     
`5. 完整的JSON格式的返回：{"status":"error","err-code":"api-signature-not-valid","err-msg":"Signature not valid: Incorrect Access key [Access key错误]","data":null}`  
`6. 问题出现频率：每次都会出现`  
`7. 签名前字符串`    
`GET\n`  
`api.huobi.pro\n`  
`/v1/account/accounts\n`   
`AccessKeyId=rfhxxxxx-950000847-boooooo3-432c0&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2019-11-06T03%3A26%3A13`   

注意：Access Key仅能证明您的身份，不会影响您账户的安全。切记**不**要将Secret Key信息分享给任何人，若您不小心将Secret Key暴露，请尽快[删除](https://www.hbg.com/zh-cn/apikey/)其对应的API Key，以免造成您的账户损失。

# 快速入门

## 接入准备

如需使用API ，请先登录网页端，完成API key的申请和权限配置，再据此文档详情进行开发和交易。  

您可以点击 <a href='https://www.hbg.com/zh-cn/apikey/'>这里 </a> 创建 API Key。

每个母用户可创建20组Api Key，每个Api Key可对应设置读取、交易、提币三种权限。  

权限说明如下：

- 读取权限：读取权限用于对数据的查询接口，例如：订单查询、成交查询等。
- 交易权限：交易权限用于下单、撤单、划转类接口。
- 提币权限：提币权限用于创建提币订单、取消提币订单操作。

创建成功后请务必记住以下信息：

- `Access Key`  API 访问密钥
  
- `Secret Key`  签名认证加密所使用的密钥（仅申请时可见）

<aside class="notice">
每个 API Key 最多可绑定 20个IP 地址(主机地址或网络地址)，未绑定 IP 地址的 API Key 有效期为90天。出于安全考虑，强烈建议您绑定 IP 地址。
</aside>
<aside class="warning">
<red><b>风险提示</b></red>：这两个密钥与账号安全紧密相关，无论何时都请勿将二者<b>同时</b>向其它人透露。API Key的泄露可能会造成您的资产损失（即使未开通提币权限），若发现API Key泄露请尽快删除该API Key。
</aside> 

## SDK与代码示例

**SDK（推荐）**

[Java](https://github.com/huobiapi/huobi_Java) | [Python3](https://github.com/huobiapi/huobi_Python) | [C++](https://github.com/huobiapi/huobi_Cpp) | [C#](https://github.com/HuobiRDCenter/huobi_CSharp) | [Go](https://github.com/huobirdcenter/huobi_golang)

**其它代码示例**

[https://github.com/huobiapi?tab=repositories](https://github.com/huobiapi?tab=repositories)

## 测试环境（已停止）

测试环境运行了一段时间后，因用户访问量很少，而维护成本很高，我们慎重决定后将其停止。

线上环境更稳定，流动性更好，建议您直接使用线上环境。

## 接口类型

火币为用户提供两种接口，您可根据自己的使用场景和偏好来选择适合的方式进行查询行情、交易或提币。  

### REST API

REST，即Representational State Transfer的缩写，是目前较为流行的基于HTTP的一种通信机制，每一个URL代表一种资源。

交易或资产提币等一次性操作，建议开发者使用REST API进行操作。

### WebSocket API

WebSocket是HTML5一种新的协议（Protocol）。它实现了客户端与服务器全双工通信，通过一次简单的握手就可以建立客户端和服务器连接，服务器可以根据业务规则主动推送信息给客户端。

市场行情和买卖深度等信息，建议开发者使用WebSocket API进行获取。

**接口鉴权**

以上两种接口均包含公共接口和私有接口两种类型。

公共接口可用于获取基础信息和行情数据。公共接口无需认证即可调用。

私有接口可用于交易管理和账户管理。每个私有请求必须使用您的API Key进行签名验证。

## 接入URLs
您可以自行比较使用api.huobi.pro和api-aws.huobi.pro两个域名的延迟情况，选择延迟低的进行使用。     

其中，api-aws.huobi.pro域名对使用aws云服务的用户做了一定的链路延迟优化。  

**REST API**

**`https://api.huobi.pro`**  

**`https://api-aws.huobi.pro`**  

**Websocket Feed（行情，不包含MBP增量行情）**

**`wss://api.huobi.pro/ws`**  

**`wss://api-aws.huobi.pro/ws`**  

**Websocket Feed（行情，仅MBP增量行情）**

**`wss://api.huobi.pro/feed`**  

**`wss://api-aws.huobi.pro/feed`** 

**Websocket Feed（资产和订单）**

**`wss://api.huobi.pro/ws/v1`**  

**`wss://api-aws.huobi.pro/ws/v1`**     

<aside class="notice">
请使用中国大陆以外的 IP 访问火币 API。
</aside>
<aside class="notice">
鉴于延迟高和稳定性差等原因，不建议通过代理的方式访问火币API。
</aside>
<aside class="notice">
为保证API服务的稳定性，建议使用日本AWS云服务器进行访问。如使用中国大陆境内的客户端服务器，连接的稳定性将难以保证。 
</aside> 

## 签名认证

### 签名说明

API 请求在通过 internet 传输的过程中极有可能被篡改，为了确保请求未被更改，除公共接口（基础信息，行情数据）外的私有接口均必须使用您的 API Key 做签名认证，以校验参数或参数值在传输途中是否发生了更改。  
每一个API Key需要有适当的权限才能访问相应的接口，每个新创建的API Key都需要分配权限。在使用接口前，请查看每个接口的权限类型，并确认你的API Key有相应的权限。

一个合法的请求由以下几部分组成：

- 方法请求地址：即访问服务器地址 api.huobi.pro，比如 api.huobi.pro/v1/order/orders。
- API 访问Id（AccessKeyId）：您申请的 API Key 中的 Access Key。
- 签名方法（SignatureMethod）：用户计算签名的基于哈希的协议，此处使用 HmacSHA256。
- 签名版本（SignatureVersion）：签名协议的版本，此处使用2。
- 时间戳（Timestamp）：您发出请求的时间 (UTC 时间)  。如：2017-05-11T16:22:06。在查询请求中包含此值有助于防止第三方截取您的请求。
- 必选和可选参数：每个方法都有一组用于定义 API 调用的必需参数和可选参数。可以在每个方法的说明中查看这些参数及其含义。 
  - 对于 GET 请求，每个方法自带的参数都需要进行签名运算。
  - 对于 POST 请求，每个方法自带的参数不进行签名认证，并且需要放在 body 中。
- 签名：签名计算得出的值，用于确保签名有效和未被篡改。

### 签名步骤

规范要计算签名的请求 因为使用 HMAC 进行签名计算时，使用不同内容计算得到的结果会完全不同。所以在进行签名计算前，请先对请求进行规范化处理。下面以查询某订单详情请求为例进行说明：

查询某订单详情时完整的请求URL

`https://api.huobi.pro/v1/order/orders?`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`&SignatureMethod=HmacSHA256`

`&SignatureVersion=2`

`&Timestamp=2017-05-11T15:19:30`

`&order-id=1234567890`

**1. 请求方法（GET 或 POST，WebSocket用GET），后面添加换行符 “\n”**

例如：
`GET\n`

**2. 添加小写的访问域名，后面添加换行符 “\n”**

例如：
`
api.huobi.pro\n
`

**3. 访问方法的路径，后面添加换行符 “\n”**

例如查询订单：<BR>
`
/v1/order/orders\n
`

例如WebSocket v2<BR>
`
/ws/v2
`

**4. 对参数进行URL编码，并且按照ASCII码顺序进行排序**

例如，下面是请求参数的原始顺序，且进行URL编码后


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`order-id=1234567890`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

<aside class="notice">
使用 UTF-8 编码，且进行了 URL 编码，十六进制字符必须大写，如 “:” 会被编码为 “%3A” ，空格被编码为 “%20”。
</aside>
<aside class="notice">
时间戳（Timestamp）需要以YYYY-MM-DDThh:mm:ss格式添加并且进行 URL 编码。
</aside>

经过排序之后

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

`order-id=1234567890`

**5. 按照以上顺序，将各参数使用字符 “&” 连接**


`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&order-id=1234567890`

**6. 组成最终的要进行签名计算的字符串如下**

`GET\n`

`api.huobi.pro\n`

`/v1/order/orders\n`

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&order-id=1234567890`


**7. 用上一步里生成的 “请求字符串” 和你的密钥 (Secret Key) 生成一个数字签名**


1. 将上一步得到的请求字符串和 API 私钥作为两个参数，调用HmacSHA256哈希函数来获得哈希值。
2. 将此哈希值用base-64编码，得到的值作为此次接口调用的数字签名。

`4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o=`

**8. 将生成的数字签名加入到请求里**

对于Rest接口：

1. 把所有必须的认证参数添加到接口调用的路径参数里
2. 把数字签名在URL编码后加入到路径参数里，参数名为“Signature”。

最终，发送到服务器的 API 请求应该为

`https://api.huobi.pro/v1/order/orders?AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&order-id=1234567890&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&Signature=4F65x5A2bLyMWVQj3Aqp%2BB4w%2BivaA7n5Oi2SuYtCJ9o%3D`

对于WebSocket接口：

1. 按照要求的JSON格式，填入参数和签名。
2. JSON请求中的参数不需要URL编码

例如：

`
{
    "action": "req", 
    "ch": "auth",
    "params": { 
        "authType":"api",
        "accessKey": "e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx",
        "signatureMethod": "HmacSHA256",
        "signatureVersion": "2.1",
        "timestamp": "2019-09-01T18:16:16",
        "signature": "4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o="
    }
}
`

## 子用户

子用户可以用来隔离资产与交易，资产可以在母子用户之间划转；子用户只能在子用户内进行交易，并且子用户之间资产不能直接划转，只有母用户有划转权限。  

子用户拥有独立的登录账号密码和 API Key，均由母用户在网页端进行管理。 

每个母用户可创建200个子用户，每个子用户可创建5组Api Key，每个Api Key可对应设置读取、交易两种权限。

子用户的 API Key 也可绑定 IP 地址, 有效期的限制与母用户的API Key一致。

您可以点击 <a href='https://account.hbg.com/zh-cn/subaccount/management/'>这里 </a> 创建子用户并管理。  

子用户可以访问所有公共接口，包括基本信息和市场行情，子用户可以访问的私有接口如下：

| 接口                                                         | 说明                            |      |
| ------------------------------------------------------------ | ------------------------------- | ---- |
| [POST /v1/order/orders/place](#fd6ce2a756)                   | 创建并执行订单                  |      |
| [POST /v1/order/orders/{order-id}/submitcancel](#4e53c0fccd) | 撤销一个订单                    |      |
| [POST /v1/order/orders/submitCancelClientOrder](#client-order-id) | 撤销订单（基于client order ID） |      |
| [POST /v1/order/orders/batchcancel](#ad00632ed5)             | 批量撤销订单                    |      |
| [POST /v1/order/orders/batchCancelOpenOrders](#open-orders)  | 撤销当前委托订单                |      |
| [GET /v1/order/orders/{order-id}](#92d59b6aad)               | 查询一个订单详情                |      |
| [GET /v1/order/orders](#d72a5b49e7)                          | 查询当前委托、历史委托          |      |
| [GET /v1/order/openOrders](#95f2078356)                      | 查询当前委托订单                |      |
| [GET /v1/order/matchresults](#0fa6055598)                    | 查询成交                        |      |
| [GET /v1/order/orders/{order-id}/matchresults](#56c6c47284)  | 查询某个订单的成交明细          |      |
| [GET /v1/account/accounts](#bd9157656f)                      | 查询当前用户的所有账户          |      |
| [GET /v1/account/accounts/{account-id}/balance](#870c0ab88b) | 查询指定账户的余额              |      |
| [POST /v1/futures/transfer](#e227a2a3e8)                     | 币币与合约账户间的资产划转      |      |
| [POST /v1/dw/transfer-in/margin](#0d3c2e7382)                | 从币币交易账户划转至杠杆账户    |      |
| [POST /v1/dw/transfer-out/margin](#0d3c2e7382)               | 从杠杆账户划转至币币交易账户    |      |
| [POST /v1/margin/orders](#48cca1ce88)                        | 申请借币                        |      |
| [POST /v1/margin/orders/{order-id}/repay](#48aa7c8199)       | 归还借币                        |      |
| [GET /v1/margin/loan-orders](#e52396720a)                    | 查询借币记录                    |      |
| [GET /v1/margin/accounts/balance](#6e79ba8e80)               | 查询杠杆账户余额                |      |
| [GET /v1/account/history](#84f1b5486d)                       | 查询账户流水                    |      |
| [POST /v1/cross-margin/transfer-in](#0d3c2e7382-2)           | 资产划转                        |      |
| [POST /v1/cross-margin/transfer-out](#0d3c2e7382-2)          | 资产划转                        |      |
| [GET /v1/cross-margin/loan-info](#e257b9b6a0-2)              | 查询借币币息率及额度            |      |
| [POST /v1/cross-margin/orders](#0ef2de08fa-2)                | 申请借币                        |      |
| [POST /v1/cross-margin/orders/{order-id}/repay](#097277f9fc-2) | 归还借币                        |      |
| [GET /v1/cross-margin/loan-orders](#1e90599f7f-2)            | 查询借币订单                    |      |
| [GET /v1/cross-margin/accounts/balance](#bf3a643133-2)       | 借币账户详情                    |      |
| [GET /v2/account/ledger](#2f6797c498)                        | 查询财务流水                    |      |
| [POST /v1/account/transfer](#0d3c2e7382)                     | 资产划转                        |      |
| [GET /v2/point/account](#0d7f115f63)                         | 查询点卡余额                    |      |
| [POST /v2/point/transfer](#c71521e5d9)                       | 点卡划转                        |      |
| [GET /v2/etp/reference](#8bb7c6b75e)                         | 杠杆ETP基础参考信息             |      |
| [POST /v2/etp/creation](#etp-4)                              | 杠杆ETP换入                     |      |
| [POST /v2/etp/redemption](#etp-5)                            | 杠杆ETP换出                     |      |
| [GET /v2/etp/transactions](#etp-6)                           | 获取杠杆ETP换入换出记录         |      |
| [GET /v2/etp/transaction](#etp-7)                            | 获取特定杠杆ETP换入换出记录     |      |
| [GET /v2/etp/rebalance](#etp-8)                              | 获取杠杆ETP调仓记录             |      |

<aside class="notice">
其他接口子用户不可访问，如果尝试访问，系统会返回 “error-code 403”。
</aside>

## 业务字典

### 交易对

交易对由基础币种和报价币种组成。以交易对 BTC/USDT 为例，BTC 为基础币种，USDT 为报价币种。  

基础币种对应字段为 base-currency 。  

报价币种对应字段为 quote-currency 。 

### 账户

不同业务对应需要不同的账户，account-id为不同业务账户的唯一标识ID。  

account-id可通过/v1/account/accounts接口获取，并根据account-type区分具体账户。  

账户类型包括：   

* spot：现货账户  
* otc：OTC账户  
* margin：逐仓杠杆账户，该账户类型以subType区分具体币种对账户  
* super-margin（或cross-margin）：全仓杠杆账户  
* point：点卡账户  
* minepool：矿池账户  
* etf：ETF账户 
* 抵押借贷：crypto-loans

### 订单、成交相关ID说明  
* order-id : 订单的唯一编号  
* client-order-id : 客户自定义ID，该ID在下单时传入，与下单成功后返回的order-id对应，该ID 24小时内有效。  允许的字符包括字母(大小写敏感)、数字、下划线 (_)和横线(-)，最长64位
* match-id : 订单在撮合中的顺序编号  
* trade-id : 成交的唯一编号  

### 订单类型
当前火币的订单类型是由买卖方向以及订单操作类型组成，例如：buy-market，buy为买卖方向，market为操作类型。    

买卖方向：  

* buy : 买  
* sell: 卖   

订单种类:  

* limit : 限价单，该类型订单需指定下单价格，下单数量。  
* market : 市价单，该类型订单仅需指定下单金额或下单数量，不需要指定价格，订单在进入撮合时，会直接与对手方进行成交，直至金额或数量低于最小成交金额或成交数量为止。  
* limit-maker : 限价挂单，该订单在进入撮合时，只能作为maker进入市场深度,若订单会被成交，则撮合会直接拒绝该订单。  
* ioc : 立即成交或取消（immediately or cancel），该订单在进入撮合后，若不能直接成交，则会被直接取消（部分成交后，剩余部分也会被取消）。  
* stop-limit : 止盈止损单，设置高于或低于市场价格的订单，当订单到达触发价格后，才会正式的进入撮合队列。  
* fok : 立即完全成交否则完全取消（fill or kill），该订单在进入撮合后，若不能立即完全成交，则会被完全取消。  

### 订单状态
* submitted : 等待成交，该状态订单已进入撮合队列当中。  
* partial-filled : 部分成交，该状态订单在撮合队列当中，订单的部分数量已经被市场成交，等待剩余部分成交。  
* filled : 已成交。该状态订单不在撮合队列中，订单的全部数量已经被市场成交。  
* partial-canceled : 部分成交撤销。该状态订单不在撮合队列中，此状态由partial-filled转化而来，订单数量有部分被成交，但是被撤销。  
* canceled : 已撤销。该状态订单不在撮合订单中，此状态订单没有任何成交数量，且被成功撤销。  
* canceling : 撤销中。该状态订单正在被撤销的过程中，因订单最终需在撮合队列中剔除才会被真正撤销，所以此状态为中间过渡态。  

更多信息，可以点击<a href='https://www.huobi.com/zh-cn/guide/'>火币成长学院</a> 进行了解。  

# 接入说明

## 接口概览

| 接口分类       | 分类链接                     | 概述                                             |
| -------------- | ---------------------------- | ------------------------------------------------ |
| 基础类         | /v1/common/*                 | 基础类接口，包括币种、币种对、时间戳等接口       |
| 行情类         | /market/*                    | 公共行情类接口，包括成交、深度、行情等           |
| 账户类         | /v1/account/*  /v1/subuser/* | 账户类接口，包括账户信息，子用户等               |
| 订单类         | /v1/order/*                  | 订单类接口，包括下单、撤单、订单查询、成交查询等 |
| 逐仓杠杆类     | /v1/margin/*                 | 逐仓杠杆类接口，包括借币、还币、查询等           |
| 全仓杠杆类接口 | /v1/cross-margin/*           | 全仓杠杆类接口，包括借币、还币、查询等           |

该分类为大类整理，部分接口未遵循此规则，请根据需求查看有关接口文档。

## 新限频规则

- 当前，新限频规则正在逐步上线中，已单独标注限频值的接口且该限频值被标注为NEW的接口适用新限频规则。

- 新限频规则采用基于UID的限频机制，即，同一UID下各API Key同时对某单个节点请求的频率不能超出单位时间内该节点最大允许访问次数的限制。

- 用户可根据Http Header中的"X-HB-RateLimit-Requests-Remain"（限频剩余次数）及"X-HB-RateLimit-Requests-Expire"（窗口过期时间）查看当前限频使用情况，以及所在时间窗口的过期时间，根据该数值动态调整您的请求频率。

## 限频规则

除已单独标注限频值为NEW的接口外 -<br>
* 每个API Key 在1秒之内限制10次<br>
* 若接口不需要API Key，则每个IP在1秒内限制10次<br>

比如：

* 资产订单类接口调用根据API Key进行限频：1秒10次
* 行情类接口调用根据IP进行限频：1秒10次

## 请求格式

所有的API请求都是restful，目前只有两种方法：GET和POST

* GET请求：所有的参数都在路径参数里
* POST请求，所有参数以JSON格式发送在请求主体（body）里

## 返回格式

所有的接口都是JSON格式。其中v1和v2接口的JSON定义略有区别。

**v1接口返回格式**：最上层有四个字段：`status`, `ch`,  `ts` 和 `data`。前三个字段表示请求状态和属性，实际的业务数据在`data`字段里。

以下是一个返回格式的样例：

```json
{
  "status": "ok",
  "ch": "market.btcusdt.kline.1day",
  "ts": 1499223904680,
  "data": // per API response data in nested JSON object
}
```

| 参数名称 | 数据类型 | 描述                                                         |
| -------- | -------- | ------------------------------------------------------------ |
| status   | string   | API接口返回状态                                              |
| ch       | string   | 接口数据对应的数据流。部分接口没有对应数据流因此不返回此字段 |
| ts       | long     | 接口返回的UTC时间的时间戳，单位毫秒                          |
| data     | object   | 接口返回数据主体                                             |

**v2接口返回格式**：最上层有三个字段：`code`, `message` 和 `data`。前两个字段表示返回码和错误消息，实际的业务数据在`data`字段里。

以下是一个返回格式的样例：

```json
{
  "code": 200,
  "message": "",
  "data": // per API response data in nested JSON object
}
```

| 参数名称 | 数据类型 | 描述               |
| -------- | -------- | ------------------ |
| code     | int      | API接口返回码      |
| message  | string   | 错误消息（如果有） |
| data     | object   | 接口返回数据主体   |

## 数据类型

本文档对JSON格式中数据类型的描述做如下约定：

- `string`: 字符串类型，用双引号（"）引用
- `int`: 32位整数，主要涉及到状态码、大小、次数等
- `long`: 64位整数，主要涉及到Id和时间戳
- `float`: 浮点数，主要涉及到金额和价格，建议程序中使用高精度浮点型
- `object`: 对象，包含一个子对象{}
- `array`: 数组，包含多个对象

## 最佳实践

###安全类
- 强烈建议：在申请API Key时，请绑定您的IP地址，以此来保证您的API Key仅能在您自己的IP上使用。另外，在API Key未绑定IP时，有效期为90天，绑定IP后，则永远不会过期。
- 强烈建议：不要将API Key暴露给任何人（包括第三方软件或机构），API Key代表了您的账户权限，API Key的暴露可能会对您的信息、资金造成损失，若API Key泄露，请尽快删除并重新创建。

###公共类
**API访问建议**

- 不建议在中国大陆境内使用临时域名以及代理的方式访问Huobi API，此类方式访问API连接的稳定性很难保证。
- 建议使用日本AWS云服务器进行访问。
- 官方域名api.huobi.pro, api-aws.huobi.pro，若您使用了AWS云服务，建议使用api-aws.huobi.pro域名，该域名为AWS用户做了链路上的优化，链路延迟相对更低。

**新限频规则**

- 当前最新限频规则正在逐步上线中，已单独标注限频值的接口适用新限频规则。

- 用户可根据Http Header中“X-HB-RateLimit-Requests-Remain（限频剩余次数）”，“X-HB-RateLimit-Requests-Expire（窗口过期时间）”查看当前限频使用情况，以及所在时间窗口的过期时间，根据该数值动态调整您的请求频率。

- 同一UID下各API Key同时对某单个节点请求的频率不能超出单位时间内该节点最大允许访问次数的限制。

###行情类
**行情类数据的获取**

- 行情类数据推荐使用WebSocket方式实时接收数据变化的推送，并在程序中进行数据的缓存，WebSocket方式实时性更高，且不受限频的影响。
- 建议用户不要在同一条WebSocket连接中订阅过多的主题和币种对，否则可能会因为上游数据量过大，导致网络阻塞，以至于连接断连。

**最新成交价格的获取**

- 推荐使用WebSocket的方式订阅`market.$symbol.trade.detail`主题，该主题为逐笔成交信息推送，该数据中成交的Price即为最新成交价格，且实时性更高。

**盘口深度的获取**

- 若对盘口数据的要求仅为买一卖一，可使用WebSocket订阅`market.$symbol.bbo`主题，该主题会在买一卖一变更时进行推送。
- 若需要多档数据，且对数据的实时性要求不高的情况下，可使用WebSocket订阅`market.$symbol.depth.$type`主题，该主题推送周期为1秒。
- 若需要多档数据，且对数据的实时性要求较高的情况下，可使用WebSocket订阅`market.$symbol.mbp.$levels`主题，并使用该主题发送req请求，构建本地深度，并增量跟新，该主题增量消息推送最快周期为100ms。
- 建议使用Rest（`/market/depth`）、WebSocket全量推送（`market.$symbol.depth.$type`）获取深度时，根据version字段对数据进行去重（舍弃较小的version）；使用WebSocket增量推送（`market.$symbol.mbp.$levels`）时，根据seqNum字段进行去重（舍弃较小的seqNum）。

**最新成交的获取**

- 建议订阅WebSocket成交明细（`market.$symbol.trade.detail`）主题时，可根据tradeId字段对数据进行去重。

###订单类
**下单接口（/v1/order/orders/place）**

- 建议用户下单前根据`/v1/common/symbols`接口中返回的币种对参数数据对下单价格、下单数量等参进行校验，避免产生无效的下单请求。
- 推荐下单时携带`client-order-id`参数，且能够保证该参数的唯一性（每次发送请求时都不同，且唯一），该参数能够防止在发起下单请求时由于网络或其他原因造成接口超时或没有返回的情况，在此情况下，可根据`client-order-id`对WebSocket中推送过来的数据进行验证，或使用`/v1/order/orders/getClientOrder`接口查询该订单信息。

**搜索历史订单（/v1/order/orders）**

- 推荐使用`start-time`、`end-time`参数进行查询，该参数传入值为13位时间戳（精确至毫秒），使用该参数查询时最大查询窗口为48小时（2天），推荐按照小时进行查询，您搜索的时间范围越小，时间戳准确性越高，查询的效率会更高，可以根据上次查询的时间戳进行迭代查询。

**订单状态变化的通知**

- 建议使用WebSocket订阅`orders.$symbol.update`主题，该主题拥有更低的数据延迟以及更准确的消息顺序。
- 不建议使用WebSocket订阅`orders.$symbol`主题，该主题已由`orders.$symbol.update`取代，会在后续停止服务，请尽早更换使用。

###账户类
**资产变更**

- 使用WebSocket的方式，同时订阅`orders.$symbol.update`、`accounts.update#${mode}`主题，`orders.$symbol.update`用于接收订单的状态变化（创建、成交、撤销以及相关成交价格、数量信息），由于该主题在推送数据时，未经过清算，所以时效性更快，可根据`accounts.update#${mode}`主题接收相关资产的变更信息，以此来维护账户内的资金情况。
- 不建议WebSocket订阅`accounts`主题，该主题已由`accounts.update#${mode}`取代，会在后续停止服务，请尽早更换使用。

# 常见问题

## API信息通知
关于API新增、更新、下线等信息火币会提前发布公告进行通知，建议您关注和订阅我们的公告，及时获取相关信息。  

公告订阅流程：点击“[API公告](https://huobiglobal.zendesk.com/hc/zh-cn/sections/360000070201-API-%E5%85%AC%E5%91%8A)”右上角“关注”按钮，用账号登录成功后，再次点击“关注”按钮，并选择需要关注的内容类型，按钮变为“正在关注”，即表示订阅成功。若无账号，点击弹窗左下角“注册”按钮，进行注册。 

## 接入、验签相关

### Q1：一个用户可以申请多少个Api Key？
A:  每个母用户可创建5组Api Key，每个Api Key可对应设置读取、交易、提币三种权限。 
每个母用户还可创建200个子用户，每个子用户可创建5组Api Key，每个Api Key可对应设置读取、交易两种权限。   

以下是三种权限的说明：  

- 读取权限：读取权限用于对数据的查询接口，例如：订单查询、成交查询等。  
- 交易权限：交易权限用于下单、撤单、划转类接口。  
- 提币权限：提币权限用于创建提币订单、取消提币订单操作。  

### Q2：为什么经常出现断线、超时的情况？
A：请检查是否属于以下情况：

1. 客户端服务器如在中国大陆境内，连接的稳定性很难保证，建议使用日本AWS云服务器进行访问。  

2. 域名建议使用api.huobi.pro或api-aws.huobi.pro，其他不建议使用。

### Q3：为什么WebSocket总是断开连接？
A：常见原因有：

1. 未回复Pong，WebSocket连接需在接收到服务端发送的Ping信息后回复Pong，保证连接的稳定。

2. 网络原因造成客户端发送了Pong消息，但服务端并未接收到。

3. 网络原因造成连接断开。

4. 建议用户做好WebSocket连接断连重连机制，在确保心跳（Ping/Pong）消息正确回复后若连接意外断开，程序能够自动进行重新连接。

### Q4：api.huobi.pro 与 api-aws.huobi.pro有什么区别？
A：api-aws.huobi.pro域名对使用aws云服务的用户做了链路延迟优化，请求时延更低。

### Q5：为什么签名认证总返回失败？
A：请对比使用Secret Key签名前的字符串与以下字符串的区别

`GET\n`

`api.huobi.pro\n` 

`/v1/account/accounts\n`

`AccessKeyId=rfhxxxxx-950000847-boooooo3-432c0&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2019-10-28T07%3A28%3A38`

对比时请注意一下几点：

1、签名参数应该按照ASCII码排序。比如下面是原始的参数：

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`order-id=1234567890`

`SignatureMethod=HmacSHA256` 

`SignatureVersion=2`  

`Timestamp=2017-05-11T15%3A19%3A30` 

排序之后应该为：

`AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`SignatureMethod=HmacSHA256`

`SignatureVersion=2`

`Timestamp=2017-05-11T15%3A19%3A30`

`order-id=1234567890`

2、签名串需进行URL编码。比如：

- 冒号 `:`会被编码为`%3A`，空格会被编码为 `%20`
- 时间戳需要格式化为 `YYYY-MM-DDThh:mm:ss` ，经过URL编码之后为 `2017-05-11T15%3A19%3A30`  

3、签名需进行 base64 编码

4、Get请求参数需在签名串中

5、时间为UTC时间转换为YYYY-MM-DDTHH:mm:ss

6、检查本机时间与标准时间是否存在偏差（偏差应小于1分钟）

7、WebSocket发送验签认证消息时，消息体不需要URL编码

8、签名时所带Host应与请求接口时Host相同

如果您使用了代理，代理可能会改变请求Host，可以尝试去掉代理；

您使用的网络连接库可能会把端口包含在Host内，可以尝试在签名用到的Host中包含端口，如“api.huobi.pro:443"

9、Api Key 与 Secret Key中是否存在隐藏特殊字符，影响签名

当前官方已支持多种语言的[SDK](https://github.com/HuobiRDCenter)，可以参考SDK的签名实现，或者以下三种语言的签名样例代码

<a href='https://github.com/HuobiRDCenter/huobi_Java/blob/master/java_signature_demo.md'>JAVA签名样例代码</a> | <a href='https://github.com/HuobiRDCenter/huobi_Python/blob/master/example/python_signature_demo.md'>Python签名样例代码</a>   | <a href='https://github.com/HuobiRDCenter/huobi_Cpp/blob/master/examples/cpp_signature_demo.md'>C++签名样例代码 </a>  

### Q6：调用接口返回gateway-internal-error错误是什么原因？
A：请检查是否属于以下情况：

1. account-id 是否正确，需要由 GET /v1/account/accounts 接口返回的数据。

2. 可能为网络原因，请稍后进行重试。

3. 发送数据格式是否正确(需要标准JSON格式)。

4. POST请求头header需要声明为`Content-Type:application/json` 。

### Q7：调用接口返回 login-required错误是什么原因？
A：请检查是否属于以下情况：

1. 应该将AccessKey参数带入URL中。
2. 应该将Signature参数带入URL中。
3. account-id 是否正确，是由 `GET /v1/account/accounts` 接口返回的数据。
4. 限频发生后再次请求时可能引发该错误。

### Q8: 调用Rest接口返回HTTP 405错误 method-not-allowed是什么原因？

A：该错误表明调用了不存在的Rest接口，请检查Rest接口路径是否准确。由于Nginx的设置，请求路径(Path)是大小写敏感的，请严格按照文档声明的大小写。

## 交易相关
### Q1：account-id是什么？
A： account-id对应用户不同业务账户的ID，可通过/v1/account/accounts接口获取，并根据account-type区分具体账户。

账户类型包括：

- spot 现货账户  
- otc OTC账户  
- margin 逐仓杠杆账户，该账户类型以subType区分具体币种对账户  
- super-margin（或cross-margin） 全仓杠杆账户 
- investment C2C杠杆借出账户
- borrow C2C杠杆借入账户
- point 点卡账户  
- minepool 矿池账户 
- etf ETF账户  

### Q2：client-order-id是什么？
A： client-order-id作为下单请求标识的一个参数，类型为字符串，长度为64。 此id为用户自己生成，24小时内有效。

### Q3：如何获取下单数量、金额、小数限制、精度的信息？
A： 可使用 Rest API `GET /v1/common/symbols` 获取相关币对信息， 下单时注意最小下单数量和最小下单金额的区别。 

常见返回错误如下：  

- order-value-min-error: 下单金额小于最小交易额  
- order-orderprice-precision-error : 限价单价格精度错误  
- order-orderamount-precision-error : 下单数量精度错误  
- order-limitorder-price-max-error : 限价单价格高于限价阈值  
- order-limitorder-price-min-error : 限价单价格低于限价阈值  
- order-limitorder-amount-max-error : 限价单数量高于限价阈值  
- order-limitorder-amount-min-error : 限价单数量低于限价阈值  

### Q4：WebSocket 订单更新推送主题orders.\$symbol 和 orders.$symbol.update的区别？
A： 区别如下：

1. order.\$symbol 主题作为老的推送主题，会在一段时间后停止主题的维护和使用， 推荐使用order.$symbol.update主题。

2. 新主题orders.$symbol.update具有严格的时序性，保证数据严格按照撮合成交顺序进行推送，且具有更快的时效性以及更低的时延。

3. 为减少重复数据推送量以及更快的速度，在orders.$symbol.update推送中并未携带原始订单数量，价格信息，若需要此信息，建议可在下单时在本地维护订单信息，或在接收到推送消息后，使用Rest接口进行查询。

### Q5： 为什么收到订单成功成交的消息后再次进行下单，返回余额不足？
A：为保证订单的及时送达以及低延时， 订单推送的结果是在撮合后直接推送，此时订单可能并未完成资产的清算。  

建议使用以下方式保证资金可以正确下单：

1. 结合资产推送主题`accounts`同步接收资产变更的消息，确保资金已经完成清算。

2. 收到订单推送消息时，使用Rest接口调用账户余额，验证账户资金是否足够。

3. 账户中保留相对充足的资金余额。

### Q6: 撮合结果里的filled-fees和filled-points有什么区别？
A: 撮合成交中的成交手续费分为普通手续费以及抵扣手续费两种类型，两种类型不会同时存在。

1. 普通手续费表示，在成交时，未开启HT抵扣、点卡抵扣，使用原币进行手续费扣除。例如：在BTCUSDT币种对下购买BTC，filled-fees字段不为空，表示扣除了普通手续费，单位是BTC。

2. 抵扣手续费表示，在成交时，开启了HT抵扣或点卡抵扣，使用HT或点卡进行手续费的抵扣。例如BTCUSDT币种对下购买BTC，HT\点卡充足时，filled-fees为空，filled-points不为空，表示扣除了HT或点卡作为手续费，扣除单位需参考fee-deduct-currency字段

### Q7: 撮合结果中match-id和trade-id有什么区别？
A: match-id表示订单在撮合中的顺序号，trade-id表示成交时的序号， 一个match-id可能有多个trade-id（成交时），也可能没有trade-id(创建订单、撤销订单)

### Q8: 为什么基于当前盘口买一或者卖一价格进行下单触发了下单限价错误？
A: 当前火币有基于最新成交价上下一定幅度的限价保护，对流动性不好的币，基于盘口数据下单可能会触发限价保护。建议基于ws推送的成交价+盘口数据信息进行下单

### Q9: 如何获取杠杆类交易的币种对？
A: 您可以根据` GET /v1/common/symbols`接口返回数据中的字段区分。leverage-ratio代表逐仓杠杆倍数。super-magin-leverage-ratio代表支持全仓杠杆倍数。如果值为0，表明不支持杠杆交易。

## 杠杆借贷相关
### Q1: 逐仓和全仓借币时我查询到可借余额有值，而且我申请借币的额度小于可借余额，为什么借币时却提示可借币不足错误，无法借币成功？

A: 用户可借额度不仅取决于用户账户的可借额度，也取决于系统可借总额度。按照风险控制要求系统每天有一个借币的总额度，为所有用户共享。如果超过了这个额度，即使账户自己的额度够也无法借币。系统当天总额度用尽时，只有当天有用户还币之后，才可以继续借币。我们目前正在实现对用户更友好的解决方案，尝试将更准确的信息通过API提供给用户。



# 基础信息

## 简介

基础信息Rest接口提供了系统状态、市场状态、交易对信息、币种信息、币链信息、服务器时间戳等公共参考信息。

## 获取当前系统状态

此接口返回当前的系统状态，包含当前系统维护计划和故障进度等。

如您需要通过邮件、短信、Webhook、RSS/Atom feed接收以上信息，可点击<a href='https://status.huobigroup.com/'>这里</a>进入页面进行订阅。当前订阅依赖Google服务，订阅前请确保您可正常访问Google的服务，否则将订阅失败。

```shell
curl "https://status.huobigroup.com/api/v2/summary.json"
```

### HTTP 请求

- GET `https://status.huobigroup.com/api/v2/summary.json`

### 请求参数

此接口不接受任何参数。

> Response:

```json
{
  "page": {  // 火币现货页面基本信息
    "id": "p0qjfl24znv5",  // 页面id
    "name": "Huobi",  // 页面名称
    "url": "https://status.huobigroup.com", // 页面地址
    "time_zone": "Etc/UTC", // 时区
    "updated_at": "2020-02-07T10:25:14.717Z" // 页面最新一次更新时间
  },
  "components": [  // 系统组件及状态
    {
      "id": "h028tnzw1n5l",  // 组件id
      "name": "Deposit", // 组件名称
      "status": "operational", // 组件状态
      "created_at": "2019-12-05T02:07:12.372Z",  // 组件创建时间
      "updated_at": "2020-02-07T09:27:15.563Z", // 组件更新时间
      "position": 1,
      "description": null,
      "showcase": true,
      "group_id": "gtd0nyr3pf0k",  
      "page_id": "p0qjfl24znv5", 
      "group": false,
      "only_show_if_degraded": false
    }
  ],
  "incidents": [ // 系统故障事件及状态
        {
            "id": "rclfxz2g21ly",  // 事件id
            "name": "Market data is delayed",  // 事件名称
            "status": "investigating",  // 事件状态
            "created_at": "2020-02-11T03:15:01.913Z",  // 事件创建时间
            "updated_at": "2020-02-11T03:15:02.003Z",   // 事件更新时间
            "monitoring_at": null,
            "resolved_at": null,
            "impact": "minor",  // 事件影响程度
            "shortlink": "http://stspg.io/pkvbwp8jppf9",
            "started_at": "2020-02-11T03:15:01.906Z",
            "page_id": "p0qjfl24znv5",
            "incident_updates": [ 
                {
                    "id": "dwfsk5ttyvtb",  
                    "status": "investigating",  
                    "body": "Market data is delayed",  
                    "incident_id": "rclfxz2g21ly",   
                    "created_at": "2020-02-11T03:15:02.000Z",    
                    "updated_at": "2020-02-11T03:15:02.000Z",   
                    "display_at": "2020-02-11T03:15:02.000Z",    
                    "affected_components": [  
                        {
                            "code": "nctwm9tghxh6",  
                            "name": "Market data",  
                            "old_status": "operational",  
                            "new_status": "degraded_performance"   
                        }
                    ],
                    "deliver_notifications": true,
                    "custom_tweet": null,
                    "tweet_id": null
                }
            ],
            "components": [  
                {
                    "id": "nctwm9tghxh6",    
                    "name": "Market data", 
                    "status": "degraded_performance", 
                    "created_at": "2020-01-13T09:34:48.284Z", 
                    "updated_at": "2020-02-11T03:15:01.951Z", 
                    "position": 8,
                    "description": null,
                    "showcase": false,
                    "group_id": null,
                    "page_id": "p0qjfl24znv5",
                    "group": false,
                    "only_show_if_degraded": false
                }
            ]
        }
    ],
      "scheduled_maintenances": [  // 系统计划维护事件及状态
        {
            "id": "k7g299zl765l", // 事件id
            "name": "Schedule maintenance", // 事件名称
            "status": "scheduled", // 事件状态
            "created_at": "2020-02-11T03:16:31.481Z",  // 事件创建时间
            "updated_at": "2020-02-11T03:16:31.530Z",  // 事件更新时间
            "monitoring_at": null,
            "resolved_at": null,
            "impact": "maintenance", // 事件影响
            "shortlink": "http://stspg.io/md4t4ym7nytd",
            "started_at": "2020-02-11T03:16:31.474Z",
            "page_id": "p0qjfl24znv5",
            "incident_updates": [  
                {
                    "id": "8whgr3rlbld8",  
                    "status": "scheduled", 
                    "body": "We will be undergoing scheduled maintenance during this time.", 
                    "incident_id": "k7g299zl765l", 
                    "created_at": "2020-02-11T03:16:31.527Z",  
                    "updated_at": "2020-02-11T03:16:31.527Z",  
                    "display_at": "2020-02-11T03:16:31.527Z",  
                    "affected_components": [  
                        {
                            "code": "h028tnzw1n5l",  
                            "name": "Deposit And Withdraw - Deposit",  
                            "old_status": "operational",  
                            "new_status": "operational"  
                        }
                    ],
                    "deliver_notifications": true,
                    "custom_tweet": null,
                    "tweet_id": null
                }
            ],
            "components": [ 
                {
                    "id": "h028tnzw1n5l",  
                    "name": "Deposit", 
                    "status": "operational", 
                    "created_at": "2019-12-05T02:07:12.372Z",  
                    "updated_at": "2020-02-10T12:34:52.970Z",  
                    "position": 1,
                    "description": null,
                    "showcase": false,
                    "group_id": "gtd0nyr3pf0k",
                    "page_id": "p0qjfl24znv5",
                    "group": false,
                    "only_show_if_degraded": false
                }
            ],
            "scheduled_for": "2020-02-15T00:00:00.000Z",  // 计划维护开始时间
            "scheduled_until": "2020-02-15T01:00:00.000Z"  // 计划维护结束时间
        }
    ],
    "status": {  // 系统整体状态
        "indicator": "minor",   // 系统状态指标
        "description": "Partially Degraded Service"  // 系统状态描述
    }
}
```

### 返回字段

|字段名称 | 数据类型 | 描述
|--------- |  -----------|  -----------
|page    |                     | 火币现货status page页面基本信息
|{id        |  string                   | 页面id
|name      |      string                | 页面名称
|url     |    string                  | 页面地址
|time_zone     |     string                 | 时区
|updated_at}     |    string                  | 页面更新时间
|components  |                      | 系统组件及状态
|[{id        |  string                    | 组件id
|name        |    string                  | 组件名称，如Order submission、Order cancellation、Deposit等
|status        |    string                  | 组件状态，取值范围为：operational，degraded_performance，partial_outage，major_outage，under maintenance
|created_at        |    string                  | 组件创建时间
|updated_at        |    string                  | 组件更新时间
|.......}]        |                     | 其他字段明细，请参考返回示例
|incidents  |           | 系统故障事件及状态，若当前无故障则返回为空
|[{id        |       string               | 事件id
|name        |      string                | 事件名称
|status        |     string                 | 事件状态，取值范围为：investigating，identified，monitoring，resolved
|created_at        |       string               | 事件创建时间
|updated_at        |      string                | 事件更新时间
|.......}]        |                     | 其他字段明细，请参考返回示例
|scheduled_maintenances|                     | 系统计划维护事件及状态，若当前无计划维护则返回为空
|[{id        |     string                 | 事件id
|name        |      string                | 事件名称
|status        |       string               | 事件状态，取值范围为：scheduled，in progress，verifying，completed
|created_at        |     string                 | 事件创建时间
|updated_at        |     string                 | 事件更新时间
|scheduled_for       |      string                | 计划维护开始时间
|scheduled_until       |     string                 | 计划维护结束时间
|.......}]        |                     | 其他字段明细，请参考返回示例
|status   |                       | 系统整体状态
|{indicator        |    string                  | 系统状态指标，取值范围为：none，minor，major，critical，maintenance
|description}     |      string                | 系统状态描述，取值范围为：All Systems Operational，Minor Service Outager，Partial System Outage，Partially Degraded Service，Service Under Maintenance

## 获取当前市场状态

此节点返回当前最新市场状态。<br>
状态枚举值包括: 1 - 正常（可下单可撤单），2 - 挂起（不可下单不可撤单），3 - 仅撤单（不可下单可撤单）。<br>
挂起原因枚举值包括: 2 - 紧急维护，3 - 计划维护。<br>

```shell
curl "https://api.huobi.pro/v2/market-status"
```


### HTTP 请求

- GET `/v2/market-status`

### 请求参数

此接口不接受任何参数。

> Responds:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "marketStatus": 1
    }
}
```

### 返回字段

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	---------	|	--------	|	-----------	|
|	code	|	integer	|	TRUE	|	状态码	|
|	message	|	string	|	FALSE	|	错误描述（如有）	|
|	data	|	object	|	TRUE	|		|
|	{ marketStatus	|	integer	|	TRUE	|	市场状态（1=normal, 2=halted, 3=cancel-only）	|
|	haltStartTime	|	long	|	FALSE	|	市场暂停开始时间（unix time in millisecond），仅对marketStatus=halted或cancel-only有效	|
|	haltEndTime	|	long	|	FALSE	|	市场暂停预计结束时间（unix time in millisecond），仅对marketStatus=halted或cancel-only有效；如在marketStatus=halted或cancel-only时未返回此字段，意味着市场暂停结束时间暂时无法预计	|
|	haltReason	|	integer	|	FALSE	|	市场暂停原因（2=emergency-maintenance, 3=scheduled-maintenance），仅对marketStatus=halted或cancel-only有效	|
|	affectedSymbols }	|	string	|	FALSE	|	市场暂停影响的交易对列表，以逗号分隔，如影响所有交易对返回"all"，仅对marketStatus=halted或cancel-only有效	|

## 获取所有交易对

此接口返回所有火币全球站支持的交易对。

```shell
curl "https://api.huobi.pro/v1/common/symbols"
```


### HTTP 请求

- GET `/v1/common/symbols`

### 请求参数

此接口不接受任何参数。

> Responds:

```json
{
    "status": "ok",
    "data": [
        {
            "base-currency": "btc",
            "quote-currency": "usdt",
            "price-precision": 2,
            "amount-precision": 6,
            "symbol-partition": "main",
            "symbol": "btcusdt",
            "state": "online",
            "value-precision": 8,
            "min-order-amt": 0.0001,
            "max-order-amt": 1000,
            "min-order-value": 5,
            "limit-order-min-order-amt": 0.0001,
            "limit-order-max-order-amt": 1000,
            "sell-market-min-order-amt": 0.0001,
            "sell-market-max-order-amt": 100,
            "buy-market-max-order-value": 1000000,
            "leverage-ratio": 5,
            "super-margin-leverage-ratio": 3,
            "funding-leverage-ratio": 3,
            "api-trading": "enabled"
        },
    ......
    ]
}
```

### 返回字段

| 字段名称                   | 是否必须 | 数据类型 | 描述                                                         |
| -------------------------- | -------- | -------- | ------------------------------------------------------------ |
| base-currency              | true     | string   | 交易对中的基础币种                                           |
| quote-currency             | true     | string   | 交易对中的报价币种                                           |
| price-precision            | true     | integer  | 交易对报价的精度（小数点后位数）                             |
| amount-precision           | true     | integer  | 交易对基础币种计数精度（小数点后位数）                       |
| symbol-partition           | true     | string   | 交易区，可能值: [main，innovation]                           |
| symbol                     | true     | string   | 交易对                                                       |
| state                      | true     | string   | 交易对状态；可能值: [online，offline,suspend] online - 已上线；offline - 交易对已下线，不可交易；suspend -- 交易暂停；pre-online - 即将上线 |
| value-precision            | true     | integer  | 交易对交易金额的精度（小数点后位数）                         |
| min-order-amt              | true     | float    | 交易对限价单最小下单量 ，以基础币种为单位（即将废弃）        |
| max-order-amt              | true     | float    | 交易对限价单最大下单量 ，以基础币种为单位（即将废弃）        |
| limit-order-min-order-amt  | true     | float    | 交易对限价单最小下单量 ，以基础币种为单位（NEW）             |
| limit-order-max-order-amt  | true     | float    | 交易对限价单最大下单量 ，以基础币种为单位（NEW）             |
| sell-market-min-order-amt  | true     | float    | 交易对市价卖单最小下单量，以基础币种为单位（NEW）            |
| sell-market-max-order-amt  | true     | float    | 交易对市价卖单最大下单量，以基础币种为单位（NEW）            |
| buy-market-max-order-value | true     | float    | 交易对市价买单最大下单金额，以计价币种为单位（NEW）          |
| min-order-value            | true     | float    | 交易对限价单和市价买单最小下单金额 ，以计价币种为单位        |
| max-order-value            | false    | float    | 交易对限价单和市价买单最大下单金额 ，以折算后的USDT为单位（NEW） |
| leverage-ratio             | true     | float    | 交易对杠杆最大倍数(仅对逐仓杠杆交易对、全仓杠杆交易对、杠杆ETP交易对有效） |
| underlying                 | false    | string   | 标的交易代码 (仅对杠杆ETP交易对有效)                         |
| mgmt-fee-rate              | false    | float    | 持仓管理费费率 (仅对杠杆ETP交易对有效)                       |
| charge-time                | false    | string   | 持仓管理费收取时间 (24小时制，GMT+8，格式：HH:MM:SS，仅对杠杆ETP交易对有效) |
| rebal-time                 | false    | string   | 每日调仓时间 (24小时制，GMT+8，格式：HH:MM:SS，仅对杠杆ETP交易对有效) |
| rebal-threshold            | false    | float    | 临时调仓阈值 (以实际杠杆率计，仅对杠杆ETP交易对有效)         |
| init-nav                   | false    | float    | 初始净值（仅对杠杆ETP交易对有效）                            |
| api-trading                | true     | string   | API交易使能标记（有效值：enabled, disabled）                 |

## 获取所有币种

此接口返回所有火币全球站支持的币种。


```shell
curl "https://api.huobi.pro/v1/common/currencys"
```

### HTTP 请求

- GET `/v1/common/currencys`


### 请求参数

此接口不接受任何参数。


> Response:

```json
  "data": [
    "usdt",
    "eth",
    "etc"
  ]
```

### 返回字段


<aside class="notice">返回的“data”对象是一个字符串数组，每一个字符串代表一个支持的币种。</aside>
## APIv2 币链参考信息

此节点用于查询各币种及其所在区块链的静态参考信息（公共数据）

### HTTP 请求

- GET `/v2/reference/currencies`

```shell
curl "https://api.huobi.pro/v2/reference/currencies?currency=usdt"
```

### 请求参数

| 字段名称       | 是否必需 | 类型    | 字段描述   | 取值范围                                                     |
| -------------- | -------- | ------- | ---------- | ------------------------------------------------------------ |
| currency       | false    | string  | 币种       | btc, ltc, bch, eth, etc ...(取值参考`GET /v1/common/currencys`) |
| authorizedUser | false    | boolean | 已认证用户 | true or false (如不填，缺省为true)                           |

> Response:

```json
{
    "code":200,
    "data":[
        {
            "chains":[
                {
                    "chain":"trc20usdt",
                    "displayName":"",
                    "baseChain": "TRX",
                    "baseChainProtocol": "TRC20",
                    "isDynamic": false,
                    "depositStatus":"allowed",
                    "maxTransactFeeWithdraw":"1.00000000",
                    "maxWithdrawAmt":"280000.00000000",
                    "minDepositAmt":"100",
                    "minTransactFeeWithdraw":"0.10000000",
                    "minWithdrawAmt":"0.01",
                    "numOfConfirmations":999,
                    "numOfFastConfirmations":999,
                    "withdrawFeeType":"circulated",
                    "withdrawPrecision":5,
                    "withdrawQuotaPerDay":"280000.00000000",
                    "withdrawQuotaPerYear":"2800000.00000000",
                    "withdrawQuotaTotal":"2800000.00000000",
                    "withdrawStatus":"allowed"
                },
                {
                    "chain":"usdt",
                    "displayName":"",
                    "baseChain": "BTC",
                    "baseChainProtocol": "OMNI",
                    "isDynamic": false,
                    "depositStatus":"allowed",
                    "maxWithdrawAmt":"19000.00000000",
                    "minDepositAmt":"0.0001",
                    "minWithdrawAmt":"2",
                    "numOfConfirmations":30,
                    "numOfFastConfirmations":15,
                    "transactFeeRateWithdraw":"0.00100000",
                    "withdrawFeeType":"ratio",
                    "withdrawPrecision":7,
                    "withdrawQuotaPerDay":"90000.00000000",
                    "withdrawQuotaPerYear":"111000.00000000",
                    "withdrawQuotaTotal":"1110000.00000000",
                    "withdrawStatus":"allowed"
                },
                {
                    "chain":"usdterc20",
                    "displayName":"",
                    "baseChain": "ETH",
                    "baseChainProtocol": "ERC20",
                    "isDynamic": false,
                    "depositStatus":"allowed",
                    "maxWithdrawAmt":"18000.00000000",
                    "minDepositAmt":"100",
                    "minWithdrawAmt":"1",
                    "numOfConfirmations":999,
                    "numOfFastConfirmations":999,
                    "transactFeeWithdraw":"0.10000000",
                    "withdrawFeeType":"fixed",
                    "withdrawPrecision":6,
                    "withdrawQuotaPerDay":"180000.00000000",
                    "withdrawQuotaPerYear":"200000.00000000",
                    "withdrawQuotaTotal":"300000.00000000",
                    "withdrawStatus":"allowed"
                }
            ],
            "currency":"usdt",
            "instStatus":"normal"
        }
        ]
}

```

### 响应数据


| 字段名称                | 是否必需 | 数据类型 | 字段描述                                                     | 取值范围               |
| ----------------------- | -------- | -------- | ------------------------------------------------------------ | ---------------------- |
| code                    | true     | int      | 状态码                                                       |                        |
| message                 | false    | string   | 错误描述（如有）                                             |                        |
| data                    | true     | object   |                                                              |                        |
| { currency              | true     | string   | 币种                                                         |                        |
| { chains                | true     | object   |                                                              |                        |
| chain                   | true     | string   | 链名称                                                       |                        |
| displayName             | true     | string   | 链显示名称                                                   |                        |
| baseChain               | false    | string   | 底层链名称                                                   |                        |
| baseChainProtocol       | false    | string   | 底层链协议                                                   |                        |
| isDynamic               | false    | boolean  | 是否动态手续费（仅对固定类型有效，withdrawFeeType=fixed）    | true,false             |
| numOfConfirmations      | true     | int      | 安全上账所需确认次数（达到确认次数后允许提币）               |                        |
| numOfFastConfirmations  | true     | int      | 快速上账所需确认次数（达到确认次数后允许交易但不允许提币）   |                        |
| minDepositAmt           | true     | string   | 单次最小充币金额                                             |                        |
| depositStatus           | true     | string   | 充币状态                                                     | allowed,prohibited     |
| minWithdrawAmt          | true     | string   | 单次最小提币金额                                             |                        |
| maxWithdrawAmt          | true     | string   | 单次最大提币金额                                             |                        |
| withdrawQuotaPerDay     | true     | string   | 当日提币额度（新加坡时区）                                   |                        |
| withdrawQuotaPerYear    | true     | string   | 当年提币额度                                                 |                        |
| withdrawQuotaTotal      | true     | string   | 总提币额度                                                   |                        |
| withdrawPrecision       | true     | int      | 提币精度                                                     |                        |
| withdrawFeeType         | true     | string   | 提币手续费类型（特定币种在特定链上的提币手续费类型唯一）     | fixed,circulated,ratio |
| transactFeeWithdraw     | false    | string   | 单次提币手续费（仅对固定类型有效，withdrawFeeType=fixed）    |                        |
| minTransactFeeWithdraw  | false    | string   | 最小单次提币手续费（仅对区间类型和有下限的比例类型有效，withdrawFeeType=circulated or ratio） |                        |
| maxTransactFeeWithdraw  | false    | string   | 最大单次提币手续费（仅对区间类型和有上限的比例类型有效，withdrawFeeType=circulated or ratio） |                        |
| transactFeeRateWithdraw | false    | string   | 单次提币手续费率（仅对比例类型有效，withdrawFeeType=ratio）  |                        |
| withdrawStatus}         | true     | string   | 提币状态                                                     | allowed,prohibited     |
| instStatus }            | true     | string   | 币种状态                                                     | normal,delisted        |

### 状态码

| 状态码 | 错误信息                            | 错误场景描述 |
| ------ | ----------------------------------- | ------------ |
| 200    | success                             | 请求成功     |
| 500    | error                               | 系统错误     |
| 2002   | invalid field value in "field name" | 非法字段取值 |

## 获取当前系统时间戳

此接口返回当前的系统时间戳，即从 **UTC** 1970年1月1日0时0分0秒0毫秒到现在的总**毫秒**数。

```shell
curl "https://api.huobi.pro/v1/common/timestamp"
```

### HTTP 请求

- GET `/v1/common/timestamp`

### 请求参数

此接口不接受任何参数。

> Response:

```json
  "data": 1494900087029
```

# 行情数据

## 简介

行情数据接口提供了多种K线、深度以及最新成交记录等行情数据。

行情接口提供的数据每1分钟更新一次


## K 线数据（蜡烛图）

此接口返回历史K线数据。K线周期以新加坡时间为基准开始计算，例如日K线的起始周期为新加坡时间0时至新加坡时间次日0时。

<aside class="notice">当前 REST API 不支持自定义时间区间，如需要历史固定时间范围的数据，请参考 Websocket API 中的 K 线接口。</aside>
<aside class="notice">获取 hb10 净值时， symbol 请填写 “hb10”。</aside>

```shell
curl "https://api.huobi.pro/market/history/kline?period=1day&size=200&symbol=btcusdt"
```

### HTTP 请求

- GET `/market/history/kline`

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述                                       | 取值范围                                                     |
| ------ | -------- | -------- | ------ | ------------------------------------------ | ------------------------------------------------------------ |
| symbol | string   | true     | NA     | 交易对                                     | btcusdt, ethbtc等（如需获取杠杆ETP净值K线，净值symbol = 杠杆ETP交易对symbol + 后缀‘nav’，例如：btc3lusdtnav） |
| period | string   | true     | NA     | 返回数据时间粒度，也就是每根蜡烛的时间区间 | 1min, 5min, 15min, 30min, 60min, 4hour, 1day, 1mon, 1week, 1year |
| size   | integer  | false    | 150    | 返回 K 线数据条数                          | [1, 2000]                                                    |

> Response:

```json
[
  {
    "id": 1499184000,
    "amount": 37593.0266,
    "count": 0,
    "open": 1935.2000,
    "close": 1879.0000,
    "low": 1856.0000,
    "high": 1940.0000,
    "vol": 71031537.97866500
  }
]
```

### 响应数据

| 字段名称 | 数据类型 | 描述                                                    |
| -------- | -------- | ------------------------------------------------------- |
| id       | long     | 调整为新加坡时间的时间戳，单位秒，并以此作为此K线柱的id |
| amount   | float    | 以基础币种计量的交易量                                  |
| count    | integer  | 交易次数                                                |
| open     | float    | 本阶段开盘价                                            |
| close    | float    | 本阶段收盘价                                            |
| low      | float    | 本阶段最低价                                            |
| high     | float    | 本阶段最高价                                            |
| vol      | float    | 以报价币种计量的交易量                                  |



## 聚合行情（Ticker）

此接口获取ticker信息同时提供最近24小时的交易聚合信息。

```shell
curl "https://api.huobi.pro/market/detail/merged?symbol=ethusdt"
```
### HTTP 请求

- GET `/market/detail/merged`

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述   | 取值范围                                               |
| ------ | -------- | -------- | ------ | ------ | ------------------------------------------------------ |
| symbol | string   | true     | NA     | 交易对 | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |

> Response:

```json
{
  "id":1499225271,
  "ts":1499225271000,
  "close":1885.0000,
  "open":1960.0000,
  "high":1985.0000,
  "low":1856.0000,
  "amount":81486.2926,
  "count":42122,
  "vol":157052744.85708200,
  "ask":[1885.0000,21.8804],
  "bid":[1884.0000,1.6702]
}
```

### 响应数据

| 字段名称 | 数据类型 | 描述                                     |
| -------- | -------- | ---------------------------------------- |
| id       | long     | NA                                       |
| amount   | float    | 以基础币种计量的交易量（以滚动24小时计） |
| count    | integer  | 交易次数（以滚动24小时计）               |
| open     | float    | 本阶段开盘价（以滚动24小时计）           |
| close    | float    | 本阶段最新价（以滚动24小时计）           |
| low      | float    | 本阶段最低价（以滚动24小时计）           |
| high     | float    | 本阶段最高价（以滚动24小时计）           |
| vol      | float    | 以报价币种计量的交易量（以滚动24小时计） |
| bid      | object   | 当前的最高买价 [price, size]             |
| ask      | object   | 当前的最低卖价 [price, size]             |

## 所有交易对的最新 Tickers

获得所有交易对的 tickers。
```shell
curl "https://api.huobi.pro/market/tickers"
```
<aside class="notice">此接口返回所有交易对的 ticker，因此数据量较大。</aside>
### HTTP 请求

- GET `/market/tickers`

### 请求参数

此接口不接受任何参数。

> Response:

```json
[  
    {  
        "open":0.044297,      // 开盘价
        "close":0.042178,     // 收盘价
        "low":0.040110,       // 最低价
        "high":0.045255,      // 最高价
        "amount":12880.8510,  
        "count":12838,
        "vol":563.0388715740,
        "symbol":"ethbtc",
        "bid":0.007545,
        "bidSize":0.008,
        "ask":0.008088,
        "askSize":0.009
    },
    {  
        "open":0.008545,
        "close":0.008656,
        "low":0.008088,
        "high":0.009388,
        "amount":88056.1860,
        "count":16077,
        "vol":771.7975953754,
        "symbol":"ltcbtc",
        "bid":0.007545,
        "bidSize":0.008,
        "ask":0.008088,
        "askSize":0.009
    }
]
```

### 响应数据

核心响应数据为一个对象列，每个对象包含下面的字段

| 字段名称 | 数据类型 | 描述                                     |
| -------- | -------- | ---------------------------------------- |
| amount   | float    | 以基础币种计量的交易量（以滚动24小时计） |
| count    | integer  | 交易笔数（以滚动24小时计）               |
| open     | float    | 开盘价（以新加坡时间自然日计）           |
| close    | float    | 最新价（以新加坡时间自然日计）           |
| low      | float    | 最低价（以新加坡时间自然日计）           |
| high     | float    | 最高价（以新加坡时间自然日计）           |
| vol      | float    | 以报价币种计量的交易量（以滚动24小时计） |
| symbol   | string   | 交易对，例如btcusdt, ethbtc              |
| bid      | float    | 买一价                                   |
| bidSize  | float    | 买一量                                   |
| ask      | float    | 卖一价                                   |
| askSize  | float    | 卖一量                                   |

## 市场深度数据

此接口返回指定交易对的当前市场深度数据。

```shell
curl "https://api.huobi.pro/market/depth?symbol=btcusdt&type=step2"
```

### HTTP 请求

- GET `/market/depth`

### 请求参数

| 参数   | 数据类型 | 必须  | 默认值 | 描述                             | 取值范围                                               |      |
| ------ | -------- | ----- | ------ | -------------------------------- | ------------------------------------------------------ | ---- |
| symbol | string   | true  | NA     | 交易对                           | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |      |
| depth  | integer  | false | 20     | 返回深度的数量                   | 5，10，20                                              |      |
| type   | string   | true  | step0  | 深度的价格聚合度，具体说明见下方 | step0，step1，step2，step3，step4，step5               |      |

<aside class="notice">当type值为‘step0’时，‘depth’的默认值为150而非20。 </aside>
**参数type的各值说明**

| 取值  | 说明                    |
| ----- | ----------------------- |
| step0 | 无聚合                  |
| step1 | 聚合度为报价精度*10     |
| step2 | 聚合度为报价精度*100    |
| step3 | 聚合度为报价精度*1000   |
| step4 | 聚合度为报价精度*10000  |
| step5 | 聚合度为报价精度*100000 |

> Response:

```json
{
    "version": 31615842081,
    "ts": 1489464585407,
    "bids": [
      [7964, 0.0678], // [price, size]
      [7963, 0.9162],
      [7961, 0.1],
      [7960, 12.8898],
      [7958, 1.2],
      ...
    ],
    "asks": [
      [7979, 0.0736],
      [7980, 1.0292],
      [7981, 5.5652],
      [7986, 0.2416],
      [7990, 1.9970],
      ...
    ]
  }
```

### 响应数据

<aside class="notice">返回的JSON顶级数据对象名为'tick'而不是通常的'data'。</aside>
| 字段名称 | 数据类型 | 描述                               |
| -------- | -------- | ---------------------------------- |
| ts       | integer  | 调整为新加坡时间的时间戳，单位毫秒 |
| version  | integer  | 内部字段                           |
| bids     | object   | 当前的所有买单 [price, size]       |
| asks     | object   | 当前的所有卖单 [price, size]       |

## 最近市场成交记录

此接口返回指定交易对最新的一个交易记录。

```shell
curl "https://api.huobi.pro/market/trade?symbol=ethusdt"
```
### HTTP 请求

- GET `/market/trade`

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述                                                   |
| ------ | -------- | -------- | ------ | ------------------------------------------------------ |
| symbol | string   | true     | NA     | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |

> Response:

```json
{
    "id": 600848670,
    "ts": 1489464451000,
    "data": [
      {
        "id": 600848670,
        "trade-id": 102043494568,
        "price": 7962.62,
        "amount": 0.0122,
        "direction": "buy",
        "ts": 1489464451000
      }
    ]
}
```

### 响应数据

<aside class="notice">返回的JSON顶级数据对象名为'tick'而不是通常的'data'。</aside>
| 字段名称  | 数据类型 | 描述                                               |
| --------- | -------- | -------------------------------------------------- |
| id        | integer  | 唯一交易id（将被废弃）                             |
| trade-id  | integer  | 唯一成交ID（NEW）                                  |
| amount    | float    | 以基础币种为单位的交易量                           |
| price     | float    | 以报价币种为单位的成交价格                         |
| ts        | integer  | 调整为新加坡时间的时间戳，单位毫秒                 |
| direction | string   | 交易方向：“buy” 或 “sell”, “buy” 即买，“sell” 即卖 |

## 获得近期交易记录

此接口返回指定交易对近期的所有交易记录。

```shell
curl "https://api.huobi.pro/market/history/trade?symbol=ethusdt&size=2"
```
### HTTP 请求

- GET `/market/history/trade`

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述                                                   |
| ------ | -------- | -------- | ------ | ------------------------------------------------------ |
| symbol | string   | true     | NA     | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |
| size   | integer  | false    | 1      | 返回的交易记录数量，最大值2000                         |

> Response:

```json
[  
   {  
      "id":31618787514,
      "ts":1544390317905,
      "data":[  
         {  
            "amount":9.000000000000000000,
            "ts":1544390317905,
            "trade-id": 102043483472,
            "id":3161878751418918529341,
            "price":94.690000000000000000,
            "direction":"sell"
         },
         {  
            "amount":73.771000000000000000,
            "ts":1544390317905,
            "trade-id": 102043483473
            "id":3161878751418918532514,
            "price":94.660000000000000000,
            "direction":"sell"
         }
      ]
   },
   {  
      "id":31618776989,
      "ts":1544390311353,
      "data":[  
         {  
            "amount":1.000000000000000000,
            "ts":1544390311353,
            "trade-id": 102043494568,
            "id":3161877698918918522622,
            "price":94.710000000000000000,
            "direction":"buy"
         }
      ]
   }
]
```

### 响应数据

<aside class="notice">返回的数据对象是一个对象数组，每个数组元素为一个调整为新加坡时间的时间戳（单位毫秒）下的所有交易记录，这些交易记录以数组形式呈现。</aside>
| 参数      | 数据类型 | 描述                                               |
| --------- | -------- | -------------------------------------------------- |
| id        | integer  | 唯一交易id（将被废弃）                             |
| trade-id  | integer  | 唯一成交ID（NEW）                                  |
| amount    | float    | 以基础币种为单位的交易量                           |
| price     | float    | 以报价币种为单位的成交价格                         |
| ts        | integer  | 调整为新加坡时间的时间戳，单位毫秒                 |
| direction | string   | 交易方向：“buy” 或 “sell”, “buy” 即买，“sell” 即卖 |

## 最近24小时行情数据

此接口返回最近24小时的行情数据汇总。

<aside class="notice">此接口返回的成交量、成交金额为24小时滚动数据（平移窗口大小24小时），有可能会出现后一个窗口内的累计成交量、累计成交额小于前一窗口的情况。</aside>

```shell
curl "https://api.huobi.pro/market/detail?symbol=ethusdt"
```

### HTTP 请求

- GET `/market/detail`

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述                                                   |
| ------ | -------- | -------- | ------ | ------------------------------------------------------ |
| symbol | string   | true     | NA     | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |

> Response:

```json
{  
   "amount":613071.438479561,
   "open":86.21,
   "close":94.35,
   "high":98.7,
   "id":31619471534,
   "count":138909,
   "low":84.63,
   "version":31619471534,
   "vol":5.6617373443873316E7
}
```

### 响应数据

<aside class="notice">返回的JSON顶级数据对象名为'tick'而不是通常的'data'。</aside>
| 字段名称 | 数据类型 | 描述                                     |
| -------- | -------- | ---------------------------------------- |
| id       | integer  | 响应id                                   |
| amount   | float    | 以基础币种计量的交易量（以滚动24小时计） |
| count    | integer  | 交易次数（以滚动24小时计）               |
| open     | float    | 本阶段开盘价（以滚动24小时计）           |
| close    | float    | 本阶段收盘价（以滚动24小时计）           |
| low      | float    | 本阶段最低价（以滚动24小时计）           |
| high     | float    | 本阶段最高价（以滚动24小时计）           |
| vol      | float    | 以报价币种计量的交易量（以滚动24小时计） |
| version  | integer  | 内部数据                                 |

## 获取杠杆ETP实时净值

此接口返回杠杆ETP的最新净值。

```shell
curl "https://api.huobi.pro/market/etp?symbol=btc3lusdt"
```

### HTTP 请求

- GET `/market/etp`

### 请求参数

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述          |
| ------ | -------- | -------- | ------ | ------------- |
| symbol | string   | true     | NA     | 杠杆ETP交易对 |

> Response

```json
{
    "ch":"market.btc3lusdt.etp",
    "status":"ok",
    "ts":1597890198849,
    "tick":{
        "actualLeverage":2.988538205272293,
        "nav":17.463067985747816,
        "outstanding":98338.57818006596,
        "symbol":"btc3lusdt",
        "navTime":1597890198525,
        "basket":[
            {
                "amount":0.004438693860243208,
                "currency":"btc"
            },
            {
                "amount":-34.725977870927,
                "currency":"usdt"
            }
        ]
    }
}
```

### 响应数据

<aside class="notice">返回的JSON顶级数据对象名为'tick'而不是通常的'data'。</aside>

| 字段名称       | 数据类型 | 描述                                        |
| -------------- | -------- | -----------------------------------------|
| symbol         | string   | 杠杆ETP交易代码                             |
| nav            | float    | 最新净值                                  |
| navTime        | long     | 最新净值更新时间 (unix time in millisecond) |
| outstanding    | float    | ETP总份额                                  |
| basket         | object   | 篮子                                     |
| { currency     | float    | 币种                                      |
| amount }       | float    | 金额                                      |
| actualLeverage | float    | 实际杠杆率                                |

## 常见错误码

以下是行情数据接口返回的错误码、错误消息以及说明。

| 错误码            | 错误消息                            | 说明                    |
| ----------------- | ----------------------------------- | ----------------------- |
| invalid-parameter | invalid symbol                      | 无效的交易对            |
| invalid-parameter | invalid period                      | 请求K线，period参数错误 |
| invalid-parameter | invalid depth                       | 深度depth参数错误       |
| invalid-parameter | invalid type                        | 深度type 参数错误       |
| invalid-parameter | invalid size                        | size参数错误            |
| invalid-parameter | invalid size,valid range: [1, 2000] | size参数错误            |
| invalid-parameter | request timeout                     | 请求超时                |

# 账户相关

## 简介

账户相关接口提供了账户、余额、历史、点卡等查询以及资产划转等功能。

<aside class="notice">访问账户相关的接口需要进行签名认证。</aside>

以下是账户相关接口返回的错误码、错误消息以及说明。

| 错误码 | 错误消息  | 说明  |
| ------ | ------ | ------ |
| 500    | system error  | 调用内部服务异常 |
| 1002   | forbidden   | 禁止操作，如用户入参中accountId与UID不一致 |
| 2002   | "invalid field value in `currency`"  | currency不符合正则规则^[a-z0-9]{2,10}$  |
| 2002   | "invalid field value in `transactTypes`"    | 变动类型transactTypes不是“transfer”   |
| 2002   | "invalid field value in `sort`"    | 分页请求参数不是合法的"asc或desc"    |
| 2002   | "value in `fromId` is not found in record” | 未找到fromId  |
| 2002  | "invalid field value in `accountId`"  | 查询参数中accountId为空 |
| 2002   | "value in `startTime` exceeded valid range" | 入参查询时间大于当前时间，或者距离当前时间超过180天 |
| 2002   | "value in `endTime` exceeded valid range")  | 查询结束时间小于开始时间，或者查询时间跨度大于10天  |

## 账户信息 

API Key 权限：读取<br>
限频值（NEW）：100次/2s

查询当前用户的所有账户 ID `account-id` 及其相关信息

### HTTP 请求

- GET `/v1/account/accounts`

### 请求参数

无

> Response:

```json
{
  "data": [
    {
      "id": 100001,
      "type": "spot",
      "subtype": "",
      "state": "working"
    }
    {
      "id": 100002,
      "type": "margin",
      "subtype": "btcusdt",
      "state": "working"
    },
    {
      "id": 100003,
      "type": "otc",
      "subtype": "",
      "state": "working"
    }
  ]
}
```

### 响应数据

| 参数名称 | 是否必须 | 数据类型 | 描述                               | 取值范围                                                     |
| -------- | -------- | -------- | ---------------------------------- | ------------------------------------------------------------ |
| id       | true     | long     | account-id                         |                                                              |
| state    | true     | string   | 账户状态                           | working：正常, lock：账户被锁定                              |
| type     | true     | string   | 账户类型                           | spot：现货账户, margin：逐仓杠杆账户, otc：OTC 账户, point：点卡账户, super-margin：全仓杠杆账户, investment: C2C杠杆借出账户, borrow: C2C杠杆借入账户，矿池账户: minepool, ETF账户: etf, 抵押借贷账户: crypto-loans |
| subtype  | false    | string   | 子账户类型（仅对逐仓杠杆账户有效） | 逐仓杠杆交易标的，例如btcusdt                                |

<aside class="notice">逐仓/全仓/C2C杠杆账户（margin/super-margin/borrow）会在第一次划转资产时创建，如果未划转过资产则不会有杠杆账户。</aside>


## 账户余额

API Key 权限：读取<br>
限频值（NEW）：100次/2s

查询指定账户的余额，支持以下账户：

spot：现货账户， margin：逐仓杠杆账户，otc：OTC 账户，point：点卡账户，super-margin：全仓杠杆账户, investment: C2C杠杆借出账户, borrow: C2C杠杆借入账户

### HTTP 请求

- GET `/v1/account/accounts/{account-id}/balance`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                                                         | 默认值 | 取值范围 |
| ---------- | -------- | ------ | ------------------------------------------------------------ | ------ | -------- |
| account-id | true     | string | account-id，填在 path 中，取值参考 `GET /v1/account/accounts` |        |          |

> Response:

```json
{
  "data": {
    "id": 100009,
    "type": "spot",
    "state": "working",
    "list": [
      {
        "currency": "usdt",
        "type": "trade",
        "balance": "5007.4362872650"
      },
      {
        "currency": "usdt",
        "type": "frozen",
        "balance": "348.1199920000"
      }
    ]
  }
}
```

### 响应数据

| 参数名称 | 是否必须 | 数据类型 | 描述     | 取值范围                                                     |
| -------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| id       | true     | long     | 账户 ID  |                                                              |
| state    | true     | string   | 账户状态 | working：正常  lock：账户被锁定                              |
| type     | true     | string   | 账户类型 | spot：现货账户, margin：逐仓杠杆账户, otc：OTC 账户, point：点卡账户, super-margin：全仓杠杆账户, investment: C2C杠杆借出账户, borrow: C2C杠杆借入账户，矿池账户: minepool, ETF账户: etf, 抵押借贷账户: crypto-loans |
| list     | false    | Array    |          |                                                              |

list字段说明

| 参数名称 | 是否必须 | 数据类型 | 描述 | 取值范围                                                     |
| -------- | -------- | -------- | ---- | ------------------------------------------------------------ |
| balance  | true     | string   | 余额 |                                                              |
| currency | true     | string   | 币种 |                                                              |
| type     | true     | string   | 类型 | trade: 交易余额，frozen: 冻结余额, loan: 待还借贷本金, interest: 待还借贷利息, lock: 锁仓, bank: 储蓄 |

## 获取账户资产估值

API Key 权限：读取

限频值（NEW）：100次/2s

按照BTC或法币计价单位，获取指定账户的总资产估值。

### HTTP 请求

- GET `/v2/account/asset-valuation`

### 请求参数

| 参数              | 是否必填 | 数据类型 | 描述                                                      | 默认值 | 取值范围                                                     |
| ----------------- | -------- | -------- | --------------------------------------------------------- | ------ | ------------------------------------------------------------ |
| accountType       | true     | string   | 账户类型                                                  | NA     | spot：现货账户， margin：逐仓杠杆账户，otc：OTC 账户，super-margin：全仓杠杆账户 |
| valuationCurrency | false    | string   | 资产估值法币，即资产按哪个法币为单位进行估值。            | BTC    | 可选法币有：BTC、CNY、USD、JPY、KRW、GBP、TRY、EUR、RUB、VND、HKD、TWD、MYR、SGD、AED、SAR （大小写敏感） |
| subUid            | false    | long     | 子用户的 UID，若不填，则返回API key所属用户的账户资产估值 | NA     |                                                              |

> Responds:

```json
{
    "code": 200,
    "data": {
        "balance": "34.75",
        "timestamp": 1594901254363
    },
    "ok": true
}
```

### 返回字段
| 参数      | 是否必须 | 数据类型 | 说明                                     |
| --------- | -------- | -------- | ---------------------------------------- |
| balance   | true     | string   | 按照某一个法币为单位的总资产估值         |
| timestamp | true     | long     | 数据返回时间，为unix time in millisecond |


## 资产划转

API Key 权限：交易<br>

该节点为母用户和子用户进行资产划转的通用接口。<br>

母用户和子用户均支持的功能包括：<br>
1、币币账户与逐仓杠杠账户之间的划转；<br>
2、逐仓杠杠不同账户间相同币种的直接划转，如逐仓杠杠BTC/USDT账户和ETH/USDT账户，相同币种USDT可直接划转；<br>

仅母用户支持的功能包括：<br>
1、母用户币币账户与子用户币币账户间的划转；<br>
2、不同子用户币币账户间划转；<br>

仅子用户支持的功能包括：<br>
1、子用户币币账户向母用户下的其他子用户币币账户划转，此权限默认关闭，需母用户授权。授权接口为 `POST /v2/sub-user/transferability`；<br>
2、子用户币币账户向母用户币币账户划转；<br>

其他划转功能将逐步上线，敬请期待。<br>

### HTTP 请求

- POST `/v1/account/transfer`

### 请求参数

| 参数              | 是否必填 | 数据类型 | 说明                                | 取值范围                         |
| ----------------- | -------- | -------- | ----------------------------------- | -------------------------------- |
| from-user         | true     | long     | 转出用户uid                         | 母用户uid,子用户uid              |
| from-account-type | true     | string   | 转出账户类型                        | spot,margin                      |
| from-account      | true     | long     | 转出账户id                          |                                  |
| to-user           | true     | long     | 转入用户uid                         | 母用户uid,子用户uid              |
| to-account-type   | true     | string   | 转入账户类型                        | spot,margin                      |
| to-account        | true     | long     | 转入账户id                          |                                  |
| currency          | true     | string   | 币种，即btc, ltc, bch, eth, etc ... | 取值参考GET /v1/common/currencys |
| amount            | true     | string   | 划转金额                            |                                  |


> Response:

```json
{
    "status": "ok",
    "data": {
        "transact-id": 220521190,
        "transact-time": 1590662591832
    }
}
```

### 响应数据
| 参数            | 是否必须 | 数据类型 | 说明       | 取值范围        |
| --------------- | -------- | -------- | ---------- | --------------- |
| status          | true     | string   | 状态       | "ok" or "error" |
| data            | true     | list     |            |                 |
| { transact-id   | true     | int      | 交易流水号 |                 |
| transact-time } | true     | long     | 交易时间   |                 |


## 账户流水

API Key 权限：读取<br>
限频值（NEW）：5次/2s

该节点基于用户账户ID返回账户流水。

### HTTP Request

- GET `/v1/account/history`

### 请求参数

| 参数名称       | 是否必需 | 数据类型 | 描述                                                         | 缺省值               | 取值范围                                                     |
| -------------- | -------- | -------- | ------------------------------------------------------------ | -------------------- | ------------------------------------------------------------ |
| account-id     | true     | string   | 账户编号,取值参考 `GET /v1/account/accounts`                 |                      |                                                              |
| currency       | false    | string   | 币种,即btc, ltc, bch, eth, etc ...(取值参考`GET /v1/common/currencys`) |                      |                                                              |
| transact-types | false    | string   | 变动类型，可多选，以逗号分隔                                 | all                  | trade (交易),etf（ETF申购）, transact-fee（交易手续费）, fee-deduction（手续费抵扣）, transfer（划转）, credit（借币）, liquidation（清仓）, interest（币息）, deposit（充币），withdraw（提币）, withdraw-fee（提币手续费）, exchange（兑换）, other-types（其他）,rebate（交易返佣） |
| start-time     | false    | long     | 远点时间 unix time in millisecond. 以transact-time为key进行检索. 查询窗口最大为1小时. 窗口平移范围为最近30天. | ((end-time) – 1hour) | [((end-time) – 1hour), (end-time)]                           |
| end-time       | false    | long     | 近点时间unix time in millisecond. 以transact-time为key进行检索. 查询窗口最大为1小时. 窗口平移范围为最近30天. | current-time         | [(current-time) – 29days,(current-time)]                     |
| sort           | false    | string   | 检索方向                                                     | asc                  | asc or desc                                                  |
| size           | false    | int      | 最大条目数量                                                 | 100                  | [1,500]                                                      |
| from-id        | false    | long     | 起始编号（仅在下页查询时有效，见注2）                        |                      |                                                              |

> Response:

```json
{
    "status": "ok",
    "data": [
        {
            "account-id": 5260185,
            "currency": "btc",
            "transact-amt": "0.002393000000000000",
            "transact-type": "transfer",
            "record-id": 89373333576,
            "avail-balance": "0.002393000000000000",
            "acct-balance": "0.002393000000000000",
            "transact-time": 1571393524526
        },
        {
            "account-id": 5260185,
            "currency": "btc",
            "transact-amt": "-0.002393000000000000",
            "transact-type": "transfer",
            "record-id": 89373382631,
            "avail-balance": "0E-18",
            "acct-balance": "0E-18",
            "transact-time": 1571393578496
        }
    ]
}
```

### 响应数据

| 字段名称      | 数据类型 | 描述                                                        | 取值范围 |
| ------------- | -------- | ----------------------------------------------------------- | -------- |
| status        | string   | 状态码                                                      |          |
| data          | object   |                                                             |          |
| { account-id  | long     | 账户编号                                                    |          |
| currency      | string   | 币种                                                        |          |
| transact-amt  | string   | 变动金额（入账为正 or 出账为负）                            |          |
| transact-type | string   | 变动类型                                                    |          |
| avail-balance | string   | 可用余额                                                    |          |
| acct-balance  | string   | 账户余额                                                    |          |
| transact-time | long     | 交易时间（数据库记录时间）                                  |          |
| record-id }   | long     | 数据库记录编号（全局唯一）                                  |          |
| next-id       | long     | 下页起始编号（仅在查询结果需要分页返回时包含此字段，见注2） |          |

注1：<br>
账户流水中返回的交易返佣为到账金额，多笔成交产生的多笔返佣可能会合并到帐，成为一笔流水。<br>

注2：<br>
仅当用户请求查询的时间范围内的数据条目超出单页限制（由“size“字段设定）时，服务器才返回”next-id“字段。用户收到服务器返
回的”next-id“后 –<br>
1） 须知晓后续仍有数据未能在本页返回；<br>
2） 如需继续查询下页数据，应再次请求查询并将服务器返回的“next-id”作为“from-id“，其它请求参数不变。<br>
3） 作为数据库记录ID，“next-id”和“from-id”除了用来翻页查询外，无其它业务含义。<br>

## 财务流水

API Key 权限：读取

该节点基于用户账户ID返回财务流水。<br>
一期上线暂时仅支持划转流水的查询（“transactType” = “transfer”）。<br>
通过“startTime”/“endTime”框定的查询窗口最大为10天，意即，通过单次查询可检索的范围最大为10天。<br>
该查询窗口可在最近180天范围内平移，意即，通过多次平移窗口查询，最多可检索到过往180天的记录。<br>

### HTTP Request

- GET `/v2/account/ledger`

### 请求参数

| 参数名称      | 数据类型 | 是否必需 | 描述                                                |
| ------------- | -------- | -------- | --------------------------------------------------- |
| accountId     | string   | TRUE     | 账户编号                                            |
| currency      | string   | FALSE    | 币种 （缺省值所有币种）                             |
| transactTypes | string   | FALSE    | 变动类型，可多填 （缺省值all） 枚举值： transfer    |
| startTime     | long     | FALSE    | 远点时间（取值范围及缺省值见注1）                   |
| endTime       | long     | FALSE    | 近点时间（取值范围及缺省值见注2）                   |
| sort          | string   | FALSE    | 检索方向（asc 由远及近, desc 由近及远，缺省值desc） |
| limit         | int      | FALSE    | 单页最大返回条目数量 [1,500] （缺省值100）          |
| fromId        | long     | FALSE    | 起始编号（仅在下页查询时有效，见注3）               |

注1：<br>
startTime取值范围：[(endTime - 10天), endTime], unix time in millisecond<br>
startTime缺省值：(endTime - 10天)

注2：<br>
endTime取值范围：[(当前时间 - 180天), 当前时间], unix time in millisecond<br>
endTime缺省值：当前时间

> Response:

```json
{
"code": 200,
"message": "success",
"data": [
    {
        "accountId": 5260185,
        "currency": "btc",
        "transactAmt": 1.000000000000000000,
        "transactType": "transfer",
        "transferType": "margin-transfer-out",
        "transactId": 0,
        "transactTime": 1585573286913,
        "transferer": 5463409,
        "transferee": 5260185
    },
    {
        "accountId": 5260185,
        "currency": "btc",
        "transactAmt": -1.000000000000000000,
        "transactType": "transfer",
        "transferType": "margin-transfer-in",
        "transactId": 0,
        "transactTime": 1585573281160,
        "transferer": 5260185,
        "transferee": 5463409
    }
]
}
```

### 响应数据

| 字段名称     | 数据类型 | 是否必需 | 描述                                                         | 取值范围                                                     |
| ------------ | -------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| code         | integer  | TRUE     | 状态码                                                       |                                                              |
| message      | string   | FALSE    | 错误描述（如有）                                             |                                                              |
| data         | object   | TRUE     | 按用户请求参数sort中定义的顺序排列                           |                                                              |
| { accountId  | integer  | TRUE     | 账户编号                                                     |                                                              |
| currency     | string   | TRUE     | 币种                                                         |                                                              |
| transactAmt  | number   | TRUE     | 变动金额（入账为正 or 出账为负）                             |                                                              |
| transactType | string   | TRUE     | 变动类型                                                     | transfer（划转）                                             |
| transferType | string   | FALSE    | 划转类型（仅对transactType=transfer有效）                    | otc-to-pro（otc到现货）, pro-to-otc（现货到otc）, futures-to-pro（交割合约到现货）, pro-to-futures（现货到交割合约）, dm-swap-to-pro（币本位永续合约到现货）, dm-pro-to-swap（现货到币本位永续合约）, margin-transfer-in（转入到逐仓杠杆）, margin-transfer-out（从逐仓杠杆转出）, pro-to-super-margin（现货到全仓杠杆）, super-margin-to-pro（全仓杠杆到现货）, master-transfer-in（转入到母用户）, master-transfer-out（从母用户转出）, sub-transfer-in（转入到子用户）, sub-transfer-out（从子用户转出） |
| transactId   | integer  | TRUE     | 交易流水号                                                   |                                                              |
| transactTime | integer  | TRUE     | 交易时间                                                     |                                                              |
| transferer   | integer  | FALSE    | 付款方账户ID                                                 |                                                              |
| transferee } | integer  | FALSE    | 收款方账户ID                                                 |                                                              |
| nextId       | integer  | FALSE    | 下页起始编号（仅在查询结果需要分页返回时包含此字段，见注3。） |                                                              |

注3：<br>
仅当用户请求查询的时间范围内的数据条目超出单页限制（由“limit“字段设定）时，服务器才返回”nextId“字段。用户收到服务器返回的”nextId“后 –<br>
1）	须知晓后续仍有数据未能在本页返回；<br>
2）	如需继续查询下页数据，应再次请求查询并将服务器返回的“nextId”作为“fromId“，其它请求参数不变。<br>
3）	作为数据库记录ID，“nextId”和“fromId”除了用来翻页查询外，无其它业务含义。<br>


## 币币现货账户与合约账户划转

API Key 权限：交易<br>

此接口用户币币现货账户与合约账户之间的资产划转。

从现货现货账户转至合约账户，类型为`pro-to-futures`; 从合约账户转至现货账户，类型为`futures-to-pro`


### HTTP 请求

- POST ` /v1/futures/transfer`

> Request

```json
{
  "currency": "btc",
  "amount": "0.001",
  "type": "pro-to-futures"
}
```

### 请求参数

|参数名称 | 数据类型 | 是否必需 | 默认值 | 描述|取值范围
|---------  | --------- | -------- | ------- | -----------|---------|
|currency     | string    | true     | NA      | 币种, e.g. btc||
|amount   | decimal    | true     | NA      | 划转数量||
|type     | string    | true     | NA      | 划转类型| 从合约账户到现货账户：“futures-to-pro”，从现货账户到合约账户： “pro-to-futures”|


> Response:

```json
{  
  "data": 12345
  "status": "ok"
}
```

### 响应数据

| 参数名称 | 数据类型 | 描述                         |
| -------- | -------- | ---------------------------- |
| data     | Long     | Transfer id                  |
| status   | string   | "ok" or "error"              |
| err-code | string   | 错误码，具体错误码请见列表   |
| err-msg  | string   | 错误消息，具体消息内容请列表 |

### 错误码

| 错误码 | 错误消息(中文）   | 错误消息(英文） |
| -------- | ------- | ------- |
| base-msg    | （具体内容参见之后的列表说明） |         |
| base-currency-error    | 币种无效   | The currency is invalid   |
| frequent-invoke   | 操作过于频繁，请稍后重试。（如果超过1分钟10次，系统返回该error-code） | the operation is too frequent. Please try again later |
| banned-by-blacklist   | 黑名单限制 | Blacklist restriction  |
| dw-insufficient-balance   | 可划转余额不足，最大可划转 {0}。（币币账户的余额不足。）     | Insufficient balance. You can only transfer {0} at most. |
| dw-account-transfer-unavailable   | 转账暂时不可用  | account transfer unavailable   |
| dw-account-transfer-error     | 由于其他服务不可用导致的划转失败  | account transfer error  |
| dw-account-transfer-failed   | 划转失败。请稍后重试或联系客服  | Failed to transfer. Please try again later.  |
| dw-account-transfer-failed-account-abnormality | 账户异常，划转失败。请稍后重试或联系客服                     | Account abnormality, failed to transfer。Please try again later. |

### base-msg对应的err-msg列表
| 错误码 | 错误消息(中文） | 错误消息(英文） |
| ---------- | --------------- | --------------- |
| base-msg   | 用户没有入金权限  | Unable to transfer in currently. Please contact customer service. |
| base-msg   | 用户没有出金权限   | Unable to transfer out currently. Please contact customer service. |
| base-msg   | 合约状态异常，无法出入金   | Abnormal contracts status. Can’t transfer.   |
| base-msg  | 子账号没有入金权限，请联系客服    | Sub-account doesn't own the permissions to transfer in. Please contact customer service. |
| base-msg  | 子账号没有出金权限，请联系客服   | Sub-account doesn't own the permissions to transfer out. Please contact customer service. |
| base-msg  | 子账号没有划转权限，请登录主账号授权   | The sub-account does not have transfer permissions. Please login main account to authorize. |
| base-msg  | 可划转余额不足     | Insufficient amount available. |
| base-msg  | 单笔转出的数量不能低于{0}{1}  | The single transfer-out amount must be no less than {0}{1}.  |
| base-msg  | 单笔转出的数量不能高于{0}{1}   | The single transfer-out amount must be no more than {0}{1}.  |
| base-msg  | 单笔转入的数量不能低于{0}{1} | The single transfer-in amount must be no less than {0}{1}.   |
| base-msg  | 单笔转入的数量不能高于{0}{1}  | The single transfer-in amount must be no more than {0}{1}.   |
| base-msg  | 您当日累计转出量超过{0}{1}，暂无法转出  | Your accumulative transfer-out amount is over the daily maximum, {0}{1}. You can't transfer out for the time being. |
| base-msg       | 您当日累计转入量超过{0}{1}，暂无法转入       | Your accumulative transfer-in amount is over the daily maximum, {0}{1}. You can't transfer in for the time being. |
| base-msg       | 您当日累计净转出量超过{0}{1}，暂无法转出     | Your accumulative net transfer-out amount is over the daily maximum, {0}{1}. You can't transfer out for the time being. |
| base-msg       | 您当日累计净转入量超过{0}{1}，暂无法转入     | Your accumulative net transfer-in amount is over the daily maximum, {0}{1}. You can't transfer in for the time being. |
| base-msg       | 超过平台当日累计最大转出量限制，暂无法转出   | The platform's accumulative transfer-out amount is over the daily maximum. You can't transfer out for the time being. |
| base-msg       | 超过平台当日累计最大转入量限制，暂无法转入   | The platform's accumulative transfer-in amount is over the daily maximum. You can't transfer in for the time being. |
| base-msg       | 超过平台当日累计最大净转出量限制，暂无法转出 | The platform's accumulative net transfer-out amount is over the daily maximum. You can't transfer out for the time being. |
| base-msg       | 超过平台当日累计最大净转入量限制，暂无法转入 | The platform's accumulative net transfer-in amount is over the daily maximum. You can't transfer in for the time being. |
| base-msg       | 划转失败，请稍后重试或联系客服   | Transfer failed. Please try again later or contact customer service. |
| base-msg       | 服务异常，划转失败，请稍后再试  | Abnormal service, transfer failed. Please try again later.   |
| base-msg       | 您尚未开通合约交易，无访问权限   | You don’t have access permission as you have not opened contracts trading. |
| base-msg       | 合约品种不存在  | This contract type doesn't exist. |

## 点卡余额查询

此节点既可查询到“不限时”点卡的余额，也可查询到“限时”点卡的余额、分组ID、及各组有效期。<br>
此节点仅可查询到限时/不限时点卡的余额，不可查询到其它币种余额。<br>
母用户可查询母用户或子用户点卡余额。<br>
点卡兑换仅可通过官网页面或APP完成。<br>

API Key 权限：读取<br>
限频值：2次/秒<br>
子用户可调用<br>

### HTTP 请求

- GET `/v2/point/account`

### 请求参数

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	---------	|	-----	|
|	subUid |	string	|	FALSE	|子用户UID（仅对母用户查询子用户点卡余额场景有效）	|

> Response:

```json
{
    "code": 200,
    "data": {
        "accountId": "14403739",
        "groupIds": [
            {
                "groupId": 26,
                "expiryDate": 1594396800000,
                "remainAmt": "0.3"
            }
        ],
        "acctBalance": "0.30000000",
        "accountStatus": "working"
    },
    "success": true
}
```

### 响应数据

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	---------	|	-----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|	|
|	{ accountId	|	string	|	TRUE	|账户ID	|
|	accountStatus	|	string	|	TRUE	| 账户状态（working 正常, lock 锁定, fl-sys 系统自动爆仓, fl-mgt 手动爆仓, fl-end 爆仓结束, fl-negative 穿仓）	|
|	acctBalance	|	string	|	TRUE	|账户余额	|
|	groupIds	|	object	|	TRUE	| 点卡分组ID列表	|
|	{ groupId	|	long	|	TRUE	| 点卡分组ID	|
|	expiryDate	|	long	|	TRUE	| 点卡到期日（unix time in millisecond）	|
|	remainAmt  }}	|	string	|	TRUE	|剩余数量	|

注：<br>
- 限时点卡分组ID = 母用户兑换该组限时点卡时的交易ID<br>
- 不限时点卡分组ID = 0<br>
- 不限时点卡到期日 = 空<br>

## 点卡划转

此节点既可划转“不限时”点卡，也可划转“限时”点卡。<br>
此节点仅支持不限时/限时点卡的划转，不支持其它币种的划转。<br>
此节点仅支持母子用户点卡（point）账户间划转。<br>
如果登录用户为母用户，该节点支持双向划转，即母向子划转和子向母划转。<br>
如果登录用户为子用户，该节点仅支持单向划转，即子向母划转。<br>
母用户将限时点卡从子用户转回时应先行查询子用户点卡的groupId。<br>

API Key 权限：交易<br>
限频值：2次/秒<br>
子用户可调用<br>

### HTTP 请求

- POST `/v2/point/transfer`

### 请求参数

| 名称    | 类型   | 是否必需 | 描述                          |
| ------- | ------ | -------- | ----------------------------- |
| fromUid | string | TRUE     | 转出方UID                     |
| toUid   | string | TRUE     | 转入方UID                     |
| groupId | long   | TRUE     | 点卡分组ID                    |
| amount  | string | TRUE     | 划转数量（最高精度: 8位小数） |

注：<br>
- 如传参点卡分组ID=0，意味着该笔划转为不限时点卡划转。<br>

> Response:

```json
{
    "code": 200,
    "data": {
        "transactId": "74",
        "transactTime": 1594370136458
    },
    "success": true
}
```

### 响应数据

| 名称           | 类型    | 是否必需 | 描述                                     |
| -------------- | ------- | -------- | ---------------------------------------- |
| code           | integer | TRUE     | 状态码                                   |
| message        | string  | FALSE    | 错误描述（如有）                         |
| data           | object  | TRUE     |                                          |
| { transactId   | string  | TRUE     | 划转交易ID                               |
| transactTime } | long    | TRUE     | 划转交易时间（unix time in millisecond） |

# 钱包（充提相关）

## 简介

充提相关接口提供了充币地址、提币地址、提币额度、充提记录等查询，以及提币、取消提币等功能。

<aside class="notice">访问充提相关的接口需要进行签名认证。</aside>

## 充币地址查询

此节点用于查询特定币种（IOTA除外）在其所在区块链中的充币地址，母子用户均可用

API Key 权限：读取<br>
限频值（NEW）：20次/2s

<aside class="notice"> 充币地址查询暂不支持IOTA币 </aside>

```shell
curl "https://api.huobi.pro/v2/account/deposit/address?currency=btc"
```

### HTTP 请求

- GET ` /v2/account/deposit/address`

### 请求参数

| 字段名称 | 是否必需 | 类型   | 字段描述 | 取值范围                                                     |
| -------- | -------- | ------ | -------- | ------------------------------------------------------------ |
| currency | true     | string | 币种     | btc, ltc, bch, eth, etc ...(取值参考`GET /v1/common/currencys`) |

> Response:

```json
{
    "code": 200,
    "data": [
        {
            "currency": "btc",
            "address": "1PSRjPg53cX7hMRYAXGJnL8mqHtzmQgPUs",
            "addressTag": "",
            "chain": "btc"
        }
    ]
}
```

### 响应数据


| 字段名称   | 是否必需 | 数据类型 | 字段描述         | 取值范围 |
| ---------- | -------- | -------- | ---------------- | -------- |
| code       | true     | int      | 状态码           |          |
| message    | false    | string   | 错误描述（如有） |          |
| data       | true     | object   |                  |          |
| {currency  | true     | string   | 币种             |          |
| address    | true     | string   | 充币地址         |          |
| addressTag | true     | string   | 充币地址标签     |          |
| chain }    | true     | string   | 链名称           |          |

### 状态码

| 状态码 | 错误信息                             | 错误场景描述 |
| ------ | ------------------------------------ | ------------ |
| 200    | success                              | 请求成功     |
| 500    | error                                | 系统错误     |
| 1002   | unauthorized                         | 未授权       |
| 1003   | invalid signature                    | 验签失败     |
| 2002   | invalid field value in "field name"  | 非法字段取值 |
| 2003   | missing mandatory field "field name" | 强制字段缺失 |

## 提币额度查询

此节点用于查询各币种提币额度，限母用户可用

API Key 权限：读取<br>
限频值（NEW）：20次/2s

```shell
curl "https://api.huobi.pro/v2/account/withdraw/quota?currency=btc"
```

### HTTP 请求

- GET ` /v2/account/withdraw/quota`

### 请求参数

| 字段名称 | 是否必需 | 类型   | 字段描述 | 取值范围                                                     |
| -------- | -------- | ------ | -------- | ------------------------------------------------------------ |
| currency | true     | string | 币种     | btc, ltc, bch, eth, etc ...(取值参考`GET /v1/common/currencys`) |

> Response:

```json
{
    "code": 200,
    "data": 
        {
            "currency": "btc",
            "chains": [
                {
                    "chain": "btc",
                    "maxWithdrawAmt": "200.00000000",
                    "withdrawQuotaPerDay": "200.00000000",
                    "remainWithdrawQuotaPerDay": "200.000000000000000000"
                }
        }
    ]
}
```

### 响应数据

| 字段名称                   | 是否必需 | 数据类型 | 字段描述         | 取值范围 |
| -------------------------- | -------- | -------- | ---------------- | -------- |
| code                       | true     | int      | 状态码           |          |
| message                    | false    | string   | 错误描述（如有） |          |
| data                       | true     | object   |                  |          |
| currency                   | true     | string   | 币种             |          |
| chains                     | true     | object   |                  |          |
| { chain                    | true     | string   | 链名称           |          |
| maxWithdrawAmt             | true     | string   | 单次最大提币金额 |          |
| withdrawQuotaPerDay        | true     | string   | 当日提币额度     |          |
| remainWithdrawQuotaPerDay  | true     | string   | 当日提币剩余额度 |          |

### 状态码

| 状态码 | 错误信息                            | 错误场景描述 |
| ------ | ----------------------------------- | ------------ |
| 200    | success                             | 请求成功     |
| 500    | error                               | 系统错误     |
| 1002   | unauthorized                        | 未授权       |
| 1003   | invalid signature                   | 验签失败     |
| 2002   | invalid field value in "field name" | 非法字段取值 |

## 提币地址查询

API Key 权限：读取<br>

该节点用于查询API key可用的提币地址，限母用户可用。<br>

### HTTP 请求

- GET `/v2/account/withdraw/address`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述                                                   | 默认值                         | 取值范围                                                     |
| -------- | -------- | ------ | ------------------------------------------------------ | ------------------------------ | ------------------------------------------------------------ |
| currency | true     | string | 币种                                                   |                                | btc, ltc, bch, eth, etc ...(取值参考`GET /v1/common/currencys`) |
| chain    | false    | string | 链名称                                                 | 如不填，返回所有链的提币地址   |                                                              |
| note     | false    | string | 地址备注                                               | 如不填，返回所有备注的提币地址 |                                                              |
| limit    | false    | int    | 单页最大返回条目数量                                   | 100                            | [1,500]                                                      |
| fromId   | false    | long   | 起始编号（提币地址ID，仅在下页查询时有效，详细见备注） | NA                             |                                                              |
> Response:

```json
{
    "code": 200,
    "data": [
        {
            "currency": "usdt",
            "chain": "usdt",
            "note": "币安",
            "addressTag": "",
            "address": "15PrEcqTJRn4haLeby3gJJebtyf4KgWmSd"
        }
    ]
}
```

### 响应数据
| 参数名称   | 是否必须 | 数据类型 | 描述                                                         | 取值范围 |
| ---------- | -------- | -------- | ------------------------------------------------------------ | -------- |
| code       | true     | int      | 状态码                                                       |          |
| message    | false    | string   | 错误描述（如有）                                             |          |
| data       | true     | object   |                                                              |          |
| { currency | true     | string   | 币种                                                         |          |
| chain      | true     | string   | 链名称                                                       |          |
| note       | true     | string   | 地址备注                                                     |          |
| addressTag | false    | string   | 地址标签，如有                                               |          |
| address }  | true     | string   | 地址                                                         |          |
| nextId     | false    | long     | 下页起始编号（提币地址ID，仅在查询结果需要分页返回时，包含此字段，详细见备注） |          |

备注：<br>
仅当用户请求查询的数据条目超出单页限制（由“limit“字段设定）时，服务器才返回”nextId“字段。用户收到服务器返回的”nextId“后 –<br>
1）须知晓后续仍有数据未能在本页返回；<br>
2）如需继续查询下页数据，应再次请求查询并将服务器返回的“nextId”作为“fromId“，其它请求参数不变。<br>
3）作为数据库记录ID，“nextId”和“fromId”除了用来翻页查询外，无其它业务含义。<br>


## 虚拟币提币

此节点用于将现货账户的数字币提取到区块链地址（已存在于提币地址列表）而不需要多重（短信、邮件）验证，限母用户可用

API Key 权限：提币<br>
限频值（NEW）：20次/2s

<aside class="notice">如果用户在 <a href='https://www.hbg.com/zh-cn/user_center/uc_setting/'>个人设置 </a> 里设置了优先使用快速提币，通过API发起的提币也会优先选择快速提币通道。快速提币是指当提币目标地址是火币用户地址时，提币将通过火币平台内部快速通道，不通过区块链。</aside>
<aside class="notice">API提币仅支持用户 <a href='https://www.hbg.com/zh-cn/withdraw_address/'>提币地址列表</a> 中的地址。IOTA一次性提币地址无法被设置为常用地址，因此不支持通过API方式提币IOTA。 </aside>

### HTTP 请求

- POST ` /v1/dw/withdraw/api/create`

> Request:

```json
{
  "address": "0xde709f2102306220921060314715629080e2fb77",
  "amount": "0.05",
  "currency": "eth",
  "fee": "0.01"
}
```

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述                                                         | 取值范围                                                     |
| -------- | -------- | ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| address  | true     | string | 提币地址                                                     | 仅支持在官网上相应币种[地址列表](https://www.hbg.com/zh-cn/withdraw_address/) 中的地址 |
| amount   | true     | string | 提币数量                                                     |                                                              |
| currency | true     | string | 资产类型                                                     | btc, ltc, bch, eth, etc ...(取值参考`GET /v1/common/currencys`) |
| fee      | true     | string | 转账手续费                                                   |                                                              |
| chain    | false    | string | 取值参考`GET /v2/reference/currencies`,例如提USDT至OMNI时须设置此参数为"usdt"，提USDT至TRX时须设置此参数为"trc20usdt"，其他币种提币无须设置此参数 |                                                              |
| addr-tag | false    | string | 虚拟币共享地址tag，适用于xrp，xem，bts，steem，eos，xmr      | 格式, "123"类的整数字符串                                    |

> Response:

```json
{
  "data": 700
}
```

### 响应数据


| 参数名称 | 是否必须 | 数据类型 | 描述    | 取值范围 |
| -------- | -------- | -------- | ------- | -------- |
| data     | false    | long     | 提币 ID |          |


## 取消提币

此节点用于取消已提交的提币请求，限母用户可用

API Key 权限：提币<br>
限频值（NEW）：20次/2s

### HTTP 请求

- POST ` /v1/dw/withdraw-virtual/{withdraw-id}/cancel`

### 请求参数

| 参数名称    | 是否必须 | 类型 | 描述                  | 默认值 | 取值范围 |
| ----------- | -------- | ---- | --------------------- | ------ | -------- |
| withdraw-id | true     | long | 提币 ID，填在 path 中 |        |          |


> Response:

```json
{
  "data": 700
}
```

### 响应数据


| 参数名称 | 是否必须 | 数据类型 | 描述    | 取值范围 |
| -------- | -------- | -------- | ------- | -------- |
| data     | false    | long     | 提币 ID |          |

## 充提记录

此节点用于查询充提记录，母子用户均可用

API Key 权限：读取<br>
限频值（NEW）：20次/2s

### HTTP 请求

- GET `/v1/query/deposit-withdraw`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述             | 默认值                                                       | 取值范围                                                     |
| -------- | -------- | ------ | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| currency | false    | string | 币种             |                                                              | btc, ltc, bch, eth, etc ...(取值参考`GET /v1/common/currencys`) |
| type     | true     | string | 充值或提币       |                                                              | deposit 或 withdraw,子用户仅可用deposit                      |
| from     | false    | string | 查询起始 ID      | 缺省时，默认值direct相关。当direct为‘prev’时，from 为1 ，从旧到新升序返回；当direct为’next‘时，from为最新的一条记录的ID，从新到旧降序返回 |                                                              |
| size     | false    | string | 查询记录大小     | 100                                                          | 1-500                                                        |
| direct   | false    | string | 返回记录排序方向 | 缺省时，默认为“prev” （升序）                                | “prev” （升序）or “next” （降序）                            |

> Response:

```json
{
  "data":
    [
      {
        "id": 1171,
        "type": "deposit",
        "currency": "xrp",
        "tx-hash": "ed03094b84eafbe4bc16e7ef766ee959885ee5bcb265872baaa9c64e1cf86c2b",
        "amount": 7.457467,
        "address": "rae93V8d2mdoUQHwBDBdM4NHCMehRJAsbm",
        "address-tag": "100040",
        "fee": 0,
        "state": "safe",
        "created-at": 1510912472199,
        "updated-at": 1511145876575
      },
      ...
    ]
}
```

### 响应数据

| 参数名称    | 是否必须 | 数据类型 | 描述                                                         | 取值范围                                 |
| ----------- | -------- | -------- | ------------------------------------------------------------ | ---------------------------------------- |
| id          | true     | long     | 充币或者提币订单id，翻页查询时from参数取自此值               |                                          |
| type        | true     | string   | 类型                                                         | 'deposit', 'withdraw', 子用户仅有deposit |
| currency    | true     | string   | 币种                                                         |                                          |
| tx-hash     | true     | string   | 交易哈希                                                     |                                          |
| chain       | true     | string   | 链名称                                                       |                                          |
| amount      | true     | float    | 个数                                                         |                                          |
| address     | true     | string   | 目的地址                                                     |                                          |
| address-tag | true     | string   | 地址标签                                                     |                                          |
| fee         | true     | float    | 手续费                                                       |                                          |
| state       | true     | string   | 状态                                                         | 状态参见下表                             |
| error-code  | false    | string   | 提币失败错误码，仅type为”withdraw“，且state为”reject“、”wallet-reject“和”failed“时有。 |                                          |
| error-msg   | false    | string   | 提币失败错误描述，仅type为”withdraw“，且state为”reject“、”wallet-reject“和”failed“时有。 |                                          |
| created-at  | true     | long     | 发起时间                                                     |                                          |
| updated-at  | true     | long     | 最后更新时间                                                 |                                          |


- 虚拟币充值状态定义：

| 状态       | 描述     |
| ---------- | -------- |
| unknown    | 状态未知 |
| confirming | 确认中   |
| confirmed  | 已确认   |
| safe       | 已完成   |
| orphan     | 待确认   |

- 虚拟币提币状态定义：

| 状态            | 描述         |
| --------------- | ------------ |
| verifying       | 待验证       |
| failed          | 验证失败     |
| submitted       | 已提交       |
| reexamine       | 审核中       |
| canceled        | 已撤销       |
| pass            | 审批通过     |
| reject          | 审批拒绝     |
| pre-transfer    | 处理中       |
| wallet-transfer | 已汇出       |
| wallet-reject   | 钱包拒绝     |
| confirmed       | 区块已确认   |
| confirm-error   | 区块确认错误 |
| repealed        | 已撤销       |

## 常见错误码

以下是充提相关接口返回的返回码、返回消息以及说明。

| 返回码 | 返回消息                             | 说明         |
| ------ | ------------------------------------ | ------------ |
| 200    | success                              | 请求成功     |
| 500    | error                                | 系统错误     |
| 1002   | unauthorized                         | 未授权       |
| 1003   | invalid signature                    | 验签失败     |
| 2002   | invalid field value in "field name"  | 非法字段取值 |
| 2003   | missing mandatory field "field name" | 强制字段缺失 |

## 常见问题

### Q1：为什么创建提币时返回api-not-support-temp-addr错误？
A：因安全考虑，API创建提币时仅支持已在提币地址列表中的地址，暂不支持使用API添加地址至提币地址列表中，需在网页端或APP端添加地址后才可在API中进行提币操作。

### Q2：为什么USDT提币时返回Invaild-Address错误？
A：USDT币种为典型的一币多链币种， 创建提币订单时应填写chain参数对应地址类型。以下表格展示了链和chain参数的对应关系：

| 链             | chain 参数 |
| -------------- | ---------- |
| ERC20 （默认） | usdterc20  |
| OMNI           | usdt       |
| TRX            | trc20usdt  |

如果chain参数为空，则默认的链为ERC20，或者也可以显示将参数赋值为`usdterc20`。

如果要提币到OMNI或者TRX，则chain参数应该填写usdt或者trc20usdt。chain参数可使用值请参考 `GET /v2/reference/currencies` 接口。

### Q3：创建提币时fee字段应该怎么填？
A：请参考 GET /v2/reference/currencies接口返回值，返回信息中withdrawFeeType为提币手续费类型，根据类型选择对应字段设置提币手续费。 

提币手续费类型包含：  

- transactFeeWithdraw : 单次提币手续费（仅对固定类型有效，withdrawFeeType=fixed）  
- minTransactFeeWithdraw : 最小单次提币手续费（仅对区间类型有效，withdrawFeeType=circulated or ratio） 
- maxTransactFeeWithdraw : 最大单次提币手续费（仅对区间类型和有上限的比例类型有效，withdrawFeeType=circulated or ratio
- transactFeeRateWithdraw :  单次提币手续费率（仅对比例类型有效，withdrawFeeType=ratio）

### Q4：如何查看我的提币额度？
A：请参考/v2/account/withdraw/quota接口返回值，返回信息中包含您查询币种的单次、当日、当前、总提币额度以及剩余额度的信息。 

若您有大额提币需求，且提币数额超出相关限额，可联系官方客服进行沟通。  

# 子用户管理

## 简介

子用户管理接口了子用户的创建、查询、权限设置、转账，子用户API Key的创建、修改、查询、删除，子用户充提地址、余额的查询等功能。

<aside class="notice">访问子用户管理的相关接口需要进行签名认证。</aside>

以下是子用户相关接口返回的返回码、返回消息以及说明。

| 错误码 | 返回消息                                                  | 说明                               |
| ------ | --------------------------------------------------------- | ---------------------------------- |
| 1002   | "forbidden"                                               | 禁止操作，如该账户不允许创建子用户 |
| 1003   | "unauthorized”                                            | 未认证                             |
| 2002   | invalid field value                                       | 参数错误                           |
| 2014   | number of sub account in the request exceeded valid range | 子账户数量达到限制                 |
| 2014   | number of api key in the request exceeded valid range     | API Key数量超过限制                |
| 2016   | invalid request while value specified in sub user states  | 冻结/解冻失败                      |

## 母子用户API key信息查询

此接口用于母用户查询自身的API key信息，以及母用户查询子用户的API key信息

API Key 权限：读取

### HTTP 请求

- GET `/v2/user/api-key`

### 请求参数
| 参数名称  | 是否必须 | 类型   | 描述                                                        | 默认值 | 取值范围 |
| --------- | -------- | ------ | ----------------------------------------------------------- | ------ | -------- |
| uid       | true     | long   | 母用户UID，子用户UID                                        | NA     |          |
| accessKey | false    | string | API key的access key，若缺省，则返回UID对应用户的所有API key | NA     |          |

> Response:

```json
{
    "code": 200,
    "message": "success",
    "data": [
        {
            "accessKey": "4ba5cdf2-4a92c5da-718ba144-dbuqg6hkte",
            "status": "normal",
            "note": "62924133",
            "permission": "readOnly,trade",
            "ipAddresses": "1.1.1.1,1.1.1.2",
            "validDays": -1,
            "createTime": 1591348751000,
            "updateTime": 1591348751000
        }
    ]
}
```

### 响应数据
| 参数名称      | 是否必须 | 数据类型 | 描述                    | 取值范围                      |
| ------------- | -------- | -------- | ----------------------- | ----------------------------- |
| code          | true     | int      | 状态码                  |                               |
| message       | false    | string   | 错误描述（如有）        |                               |
| data          | true     | object   |                         |                               |
| [{ accessKey  | true     | string   | access key              |                               |
| note          | true     | string   | API key备注             |                               |
| permission    | true     | string   | API key权限             |                               |
| ipAddresses   | false    | string   | API key绑定的IP地址     |                               |
| validDays     | true     | int      | API key剩余有效天数     | 若为-1，则表示永久有效        |
| status        | true     | string   | API key当前状态         | normal(正常)，expired(已过期) |
| createTime    | true     | long     | API key创建时间         |                               |
| updateTime }] | true     | long     | API key最近一次修改时间 |                               |

## 母子用户获取用户UID

此接口用于母子用户查询本用户UID

API Key 权限：读取

### HTTP 请求

- GET `/v2/user/uid`

### 请求参数
无


> Response:

```json
{
    "code": 200,
    "data": 63628520
}
```

### 响应数据
| 参数名称      | 是否必须 | 数据类型 | 描述   | 取值范围          |
| ------------- | -------- | -------- | ------------ | ------------- |
| code          | true     | int      | 状态码                  |        |
| message       | false    | string   | 错误描述（如有）        |         |
| data          | true     | long    |        用户UID       |     |




## 子用户创建

此接口用于母用户进行子用户创建，单次最多50个

API Key 权限：交易

### HTTP 请求

- POST `/v2/sub-user/creation`

> Request:

```json
{
"userList":
  [
    {
      "userName":"test123",
      "note":"huobi"
    },
    {
      "userName":"test456",
      "note":"huobi"
    }
  ]
}
```

### 请求参数
| 参数名称    | 是否必须 | 类型   | 描述                                               | 默认值 | 取值范围                                                     |
| ----------- | -------- | ------ | -------------------------------------------------- | ------ | ------------------------------------------------------------ |
| userList    | true     | object |                                                    |        |                                                              |
| [{ userName | true     | string | 子用户名，子用户身份的重要标识，要求火币平台内唯一 | NA     | 6至20位字母和数字的组合，可为纯字母；若字母和数字的组合，需以字母开头；字母不区分大小写； |
| note }]     | false    | string | 子用户备注，无唯一性要求                           | NA     | 最多20位字符，字符类型不限                                   |

> Response:

```json
{
    "code": 200,
    "data": [
        {
    "userName": "test123",
    "note": "huobi",
    "uid": 123
      },
        {
    "userName": "test456",
    "note": "huobi",
    "errCode": "2002",
    "errMessage": "value in user name duplicated with existing record"
      }
    ]
}
```

### 响应数据
| 参数名称      | 是否必须 | 数据类型 | 描述                                         | 取值范围 |
| ------------- | -------- | -------- | -------------------------------------------- | -------- |
| code          | true     | int      | 状态码                                       |          |
| message       | false    | string   | 错误描述（如有）                             |          |
| data          | true     | object   |                                              |          |
| [{ userName   | true     | string   | 子用户名                                     |          |
| note          | false    | string   | 子用户备注（仅对有备注的子用户有效）         |          |
| uid           | false    | long     | 子用户UID（仅对创建成功的子用户有效）        |          |
| errCode       | false    | string   | 创建失败错误码（仅对创建失败的子用户有效）   |          |
| errMessage }] | false    | string   | 创建失败错误原因（仅对创建失败的子用户有效） |          |

## 获取子用户列表

母用户通过此接口可获取所有子用户的UID列表及各用户状态

API Key 权限：读取

### HTTP 请求

- GET `/v2/sub-user/user-list`

### 请求参数

| 参数名称 | 是否必须 | 类型 | 描述                             | 默认值 | 取值范围 |
| -------- | -------- | ---- | -------------------------------- | ------ | -------- |
| fromId   | FALSE    | long | 查询起始编号（仅对翻页查询有效） |        |          |

> Response:

```json
{
    "code": 200,
    "data": [
        {
            "uid": 63628520,
            "userState": "normal"
        },
        {
            "uid": 132208121,
            "userState": "normal"
        }
    ]
}
```

### 响应数据

| 参数名称    | 是否必须 | 数据类型 | 描述                                       | 取值范围     |
| ----------- | -------- | -------- | ------------------------------------------ | ------------ |
| code        | TRUE     | int      | 状态码                                     |              |
| message     | FALSE    | string   | 错误描述（如有）                           |              |
| data        | TRUE     | object   |                                            |              |
| { uid       | TRUE     | long     | 子用户UID                                  |              |
| userState } | TRUE     | string   | 子用户状态                                 | lock, normal |
| nextId      | FALSE    | long     | 下页查询起始编号（仅在存在下页数据时返回） |              |

##冻结/解冻子用户

API Key 权限：交易<br>
限频值（NEW）：20次/2s

此接口用于母用户对其下一个子用户进行冻结和解冻操作

###HTTP 请求

- POST `/v2/sub-user/management`

### 请求参数

| 参数   | 是否必填 | 数据类型 | 长度 | 说明        | 取值范围                 |
| ------ | -------- | -------- | ---- | ----------- | ------------------------ |
| subUid | true     | long     | -    | 子用户的UID | -                        |
| action | true     | string   | -    | 操作类型    | lock(冻结)，unlock(解冻) |

> Response:

```json
{
  "code": 200,
	"data": {
     "subUid": 12902150,
     "userState":"lock"}
}
```

### 响应数据

| 参数      | 是否必填 | 数据类型 | 长度 | 说明       | 取值范围                   |
| --------- | -------- | -------- | ---- | ---------- | -------------------------- |
| subUid    | true     | long     | -    | 子用户UID  | -                          |
| userState | true     | string   | -    | 子用户状态 | lock(已冻结)，normal(正常) |


## 获取特定子用户的用户状态

母用户通过此接口可获取特定子用户的用户状态

API Key 权限：读取

### HTTP 请求

- GET `/v2/sub-user/user-state`

### 请求参数

| 参数名称 | 是否必须 | 类型 | 描述      | 默认值 | 取值范围 |
| -------- | -------- | ---- | --------- | ------ | -------- |
| subUid   | TRUE     | long | 子用户UID |        |          |

> Response:

```json
{
    "code": 200,
    "data": {
        "uid": 132208121,
        "userState": "normal"
    }
}
```

### 响应数据

| 参数名称    | 是否必须 | 数据类型 | 描述             | 取值范围     |
| ----------- | -------- | -------- | ---------------- | ------------ |
| code        | TRUE     | int      | 状态码           |              |
| message     | FALSE    | string   | 错误描述（如有） |              |
| data        | TRUE     | object   |                  |              |
| { uid       | TRUE     | long     | 子用户UID        |              |
| userState } | TRUE     | string   | 子用户状态       | lock, normal |

##设置子用户交易权限

API Key 权限：交易

此接口用于母用户批量设置子用户的交易权限。
子用户的现货交易权限默认开通无须设置。

###HTTP 请求

- POST `/v2/sub-user/tradable-market`

### 请求参数

| 参数        | 是否必填 | 数据类型 | 长度 | 说明                                          | 取值范围                     |
| ----------- | -------- | -------- | ---- | --------------------------------------------- | ---------------------------- |
| subUids     | true     | string   | -    | 子用户UID列表（支持多填，最多50个，逗号分隔） | -                            |
| accountType | true     | string   | -    | 账户类型                                      | isolated-margin,cross-margin |
| activation  | true     | string   | -    | 账户激活状态                                  | activated,deactivated        |

> Response:

```json
{
    "code": 200,
    "data": [
        {
            "subUid": "132208121",
            "accountType": "isolated-margin",
            "activation": "activated"
        }
    ]
}
```

### 响应数据

| 参数        | 是否必填 | 数据类型 | 长度 | 说明                                                       | 取值范围                     |
| ----------- | -------- | -------- | ---- | ---------------------------------------------------------- | ---------------------------- |
| code        | true     | int      | -    | 状态码                                                     |                              |
| message     | false    | string   | -    | 错误描述（如有）                                           |                              |
| data        | true     | object   |      |                                                            |                              |
| {subUid     | true     | string   | -    | 子用户UID                                                  | -                            |
| accountType | true     | string   | -    | 账户类型                                                   | isolated-margin,cross-margin |
| activation  | true     | string   | -    | 账户激活状态                                               | activated,deactivated        |
| errCode     | false    | int      | -    | 请求被拒错误码（仅在设置该subUid市场准入权限错误时返回）   |                              |
| errMessage} | false    | string   | -    | 请求被拒错误消息（仅在设置该subUid市场准入权限错误时返回） |                              |

## 设置子用户资产转出权限

API Key 权限：交易

此接口用于母用户批量设置子用户的资产转出权限。
子用户的资金转出权限包括：
-	由子用户现货（spot）账户转出至同一母用户下另一子用户的现货（spot）账户；
-	由子用户现货（spot）账户转出至母用户现货（spot）账户（无须设置，默认开通）。

###HTTP 请求

- POST `/v2/sub-user/transferability`

### 请求参数

| 参数          | 是否必填 | 数据类型 | 长度 | 说明                                          | 取值范围   |
| ------------- | -------- | -------- | ---- | --------------------------------------------- | ---------- |
| subUids       | true     | string   | -    | 子用户UID列表（支持多填，最多50个，逗号分隔） | -          |
| accountType   | false    | string   | -    | 账户类型（如不填，缺省值spot）                | spot       |
| transferrable | true     | bool     | -    | 可划转权限                                    | true,false |

> Response:

```json
{
    "code": 200,
    "data": [
        {
            "accountType": "spot",
            "transferrable": true,
            "subUid": 13220823
        }
    ]
}
```

### 响应数据

| 参数          | 是否必填 | 数据类型 | 长度 | 说明                                                       | 取值范围   |
| ------------- | -------- | -------- | ---- | ---------------------------------------------------------- | ---------- |
| code          | true     | int      | -    | 状态码                                                     |            |
| message       | false    | string   | -    | 错误描述（如有）                                           |            |
| data          | true     | object   |      |                                                            |            |
| {subUid       | true     | long     | -    | 子用户UID                                                  | -          |
| accountType   | true     | string   | -    | 账户类型                                                   | spot       |
| transferrable | true     | bool     | -    | 可划转权限                                                 | true,false |
| errCode       | false    | int      | -    | 请求被拒错误码（仅在设置该subUid市场准入权限错误时返回）   |            |
| errMessage}   | false    | string   | -    | 请求被拒错误消息（仅在设置该subUid市场准入权限错误时返回） |            |

## 获取特定子用户的账户列表

母用户通过此接口可获取特定子用户的Account ID列表及各账户状态

API Key 权限：读取

### HTTP 请求

- GET `/v2/sub-user/account-list`

### 请求参数

| 参数名称 | 是否必须 | 类型 | 描述      | 默认值 | 取值范围 |
| -------- | -------- | ---- | --------- | ------ | -------- |
| subUid   | TRUE     | long | 子用户UID |        |          |

> Response:

```json
{
    "code": 200,
    "data": {
        "uid": 132208121,
        "list": [
            {
                "accountType": "isolated-margin",
                "activation": "activated"
            },
            {
                "accountType": "cross-margin",
                "activation": "deactivated"
            },
            {
                "accountType": "spot",
                "activation": "activated",
                "transferrable": true,
                "accountIds": [
                    {
                        "accountId": 12255180,
                        "accountStatus": "normal"
                    }
                ]
            }
        ]
    }
}
```

### 响应数据

| 参数名称          | 是否必须 | 数据类型 | 描述                                              | 取值范围                                          |
| ----------------- | -------- | -------- | ------------------------------------------------- | ------------------------------------------------- |
| code              | TRUE     | int      | 状态码                                            |                                                   |
| message           | FALSE    | string   | 错误描述（如有）                                  |                                                   |
| data              | TRUE     | object   |                                                   |                                                   |
| { uid             | TRUE     | long     | 子用户UID                                         |                                                   |
| list              | TRUE     | object   |                                                   |                                                   |
| { accountType     | TRUE     | string   | 账户类型                                          | spot, isolated-margin, cross-margin, futures,swap |
| activation        | TRUE     | string   | 账户激活状态                                      | activated, deactivated                            |
| transferrable     | FALSE    | bool     | 可划转权限（仅对accountType=spot有效）            | true, false                                       |
| accountIds        | FALSE    | object   |                                                   |                                                   |
| { accountId       | TRUE     | string   | 账户ID                                            |                                                   |
| subType           | FALSE    | string   | 账户子类型（仅对accountType=isolated-margin有效） |                                                   |
| accountStatus }}} | TRUE     | string   | 账户状态                                          | normal, locked                                    |

## 子用户API key创建

此接口用于母用户创建子用户的API key

API Key 权限：交易

### HTTP 请求

- POST `/v2/sub-user/api-key-generation`

### 请求参数
| 参数名称    | 是否必须 | 类型   | 描述                                                 | 默认值 | 取值范围                                                     |
| ----------- | -------- | ------ | ---------------------------------------------------- | ------ | ------------------------------------------------------------ |
| otpToken    | true     | string | 母用户的谷歌验证码，母用户须在官网页面启用GA二次验证 | NA     | 6个字符，纯数字                                              |
| subUid      | true     | long   | 子用户UID                                            | NA     |                                                              |
| note        | ture     | string | API key备注                                          | NA     | 最多255位字符，字符类型不限                                  |
| permission  | true     | string | API key权限                                          | NA     | 取值范围：readOnly、trade，其中readOnly必传，trade选传，两个间用半角逗号分隔。 |
| ipAddresses | false    | string | API key绑定的IPv4/IPv6主机地址或IPv4网络地址         | NA     | 最多绑定20个，多个IP地址用半角逗号分隔，如：192.168.1.1,202.106.96.0/24。如果未绑定任何IP地址，API key有效期仅为90天。 |

> Response:

```json
{
    "code": 200,
    "data": {
        "accessKey": "2b55df29-vf25treb80-1535713d-8aea2",
        "secretKey": "c405c550-6fa0583b-fb4bc38e-d317e",
        "note": "62924133",
        "permission": "trade,readOnly",
        "ipAddresses": "1.1.1.1,1.1.1.2"
    }
}
```

### 响应数据
| 参数名称      | 是否必须 | 数据类型 | 描述                | 取值范围 |
| ------------- | -------- | -------- | ------------------- | -------- |
| code          | true     | int      | 状态码              |          |
| message       | false    | string   | 错误描述（如有）    |          |
| data          | true     | object   |                     |          |
| { note        | true     | string   | API key备注         |          |
| accessKey     | true     | string   | access key          |          |
| secretKey     | true     | string   | secret key          |          |
| permission    | true     | string   | API key权限         |          |
| ipAddresses } | false    | string   | API key绑定的IP地址 |          |


## 修改子用户API key

此接口用于母用户修改子用户的API key

API Key 权限：交易

### HTTP 请求

- POST `/v2/sub-user/api-key-modification`

### 请求参数
| 参数名称    | 是否必须 | 类型   | 描述                      | 默认值 | 取值范围                                                     |
| ----------- | -------- | ------ | ------------------------- | ------ | ------------------------------------------------------------ |
| subUid      | true     | long   | 子用户的uid               | NA     |                                                              |
| accessKey   | true     | string | 子用户API key的access key | NA     |                                                              |
| note        | false    | string | API key备注               | NA     | 最多255位字符                                                |
| permission  | false    | string | API key权限               | NA     | 取值范围：readOnly、trade，其中readOnly必传，trade选传，两个间用半角逗号分隔。 |
| ipAddresses | false    | string | API key绑定的IP地址       | NA     | IPv4/IPv6主机地址或IPv4网络地址，最多绑定20个，多个IP地址用半角逗号分隔，如：192.168.1.1,202.106.96.0/24。如果未绑定任何IP地址，API key有效期仅为90天。 |

> Response:

```json
{
    "code": 200,
    "data": {
        "note": "test",
        "permission": "readOnly",
        "ipAddresses": "1.1.1.3"
    }
}
```

### 响应数据
| 参数名称      | 是否必须 | 数据类型 | 描述                | 取值范围 |
| ------------- | -------- | -------- | ------------------- | -------- |
| code          | true     | int      | 状态码              |          |
| message       | false    | string   | 错误描述（如有）    |          |
| data          | true     | object   |                     |          |
| { note        | false    | string   | API key备注         |          |
| permission    | false    | string   | API key权限         |          |
| ipAddresses } | false    | string   | API key绑定的IP地址 |          |


## 删除子用户API key

此接口用于母用户删除子用户的API key

API Key 权限：交易

### HTTP 请求

- POST `/v2/sub-user/api-key-deletion`

### 请求参数
| 参数名称  | 是否必须 | 类型   | 描述                      | 默认值 | 取值范围 |
| --------- | -------- | ------ | ------------------------- | ------ | -------- |
| subUid    | true     | long   | 子用户的uid               | NA     |          |
| accessKey | true     | string | 子用户API key的access key | NA     |          |

> Response:

```json
{
    "code": 200,
    "data": null
}
```

### 响应数据
| 参数名称 | 是否必须 | 数据类型 | 描述             | 取值范围 |
| -------- | -------- | -------- | ---------------- | -------- |
| code     | true     | int      | 状态码           |          |
| message  | false    | string   | 错误描述（如有） |          |


## 资产划转（母子用户之间）

API Key 权限：交易<br>
限频值（NEW）：2次/2s

母用户执行母子用户之间的划转

### HTTP 请求

- POST ` /v1/subuser/transfer`

### 请求参数

| 参数     | 是否必填 | 数据类型 | 说明                                                         | 取值范围                                                     |      |
| -------- | -------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| sub-uid  | true     | long     | 子用户uid                                                    | -                                                            |      |
| currency | true     | string   | 币种，即btc, ltc, bch, eth, etc ...(取值参考`GET /v1/common/currencys`) | -                                                            |      |
| amount   | true     | decimal  | 划转金额                                                     | -                                                            |      |
| type     | true     | string   | 划转类型                                                     | master-transfer-in（子用户划转给母用户虚拟币）/ master-transfer-out （母用户划转给子用户虚拟币）/master-point-transfer-in （子用户划转给母用户点卡）/master-point-transfer-out（母用户划转给子用户点卡） |      |

> Response:

```json
{
  "data":123456,
  "status":"ok"
}
```

### 响应数据

| 参数   | 是否必填 | 数据类型 | 长度 | 说明       | 取值范围        |      |
| ------ | -------- | -------- | ---- | ---------- | --------------- | ---- |
| data   | true     | int      | -    | 划转订单id | -               |      |
| status | true     |          | -    | 状态       | "OK" or "Error" |      |

### 错误码

| error_code                                  | 说明                             | 类型   |      |
| ------------------------------------------- | -------------------------------- | ------ | ---- |
| account-transfer-balance-insufficient-error | 账户余额不足                     | string |      |
| base-operation-forbidden                    | 禁止操作（母子用户关系错误时报） | string |      |

## 子用户充币地址查询

此节点用于母用户查询子用户特定币种（IOTA除外）在其所在区块链中的充币地址，限母用户可用

API Key 权限：读取

### HTTP 请求

- GET  `/v2/sub-user/deposit-address`

### 请求参数

| 字段名称 | 是否必需 | 类型   | 描述      | 默认值 | 取值范围                                                     |
| -------- | -------- | ------ | --------- | ------ | ------------------------------------------------------------ |
| subUid   | true     | long   | 子用户UID | NA     | 限填1个                                                      |
| currency | true     | string | 币种      | NA     | btc, ltc, bch, eth, etc ...(取值参考`GET /v1/common/currencys`) |

> Response:

```json
{
    "code": 200,
    "data": [
        {
            "currency": "btc",
            "address": "1PSRjPg53cX7hMRYAXGJnL8mqHtzmQgPUs",
            "addressTag": "",
            "chain": "btc"
        }
    ]
}
```

### 响应数据

| 字段名称   | 是否必需 | 数据类型 | 字段描述         | 取值范围 |
| ---------- | -------- | -------- | ---------------- | -------- |
| code       | true     | int      | 状态码           |          |
| message    | false    | string   | 错误描述（如有） |          |
| data       | true     | object   |                  |          |
| { currency | true     | string   | 币种             |          |
| address    | true     | string   | 充币地址         |          |
| addressTag | true     | string   | 充币地址标签     |          |
| chain }    | true     | string   | 链名称           |          |


## 子用户充币记录查询

此节点用于母用户查询子用户充值记录，限母用户可用

API Key 权限：读取

### HTTP 请求

- GET `/v2/sub-user/query-deposit`

### 请求参数

| 参数名称  | 数据类型 | 是否必需 | 描述                                                  |
| --------- | -------- | -------- | ----------------------------------------------------- |
| subUid    | long     | TRUE     | 子用户UID，限填1个                                    |
| currency  | string   | FALSE    | 币种，缺省值所有币种                                  |
| startTime | long     | FALSE    | 远点时间，以createTime进行检索，取值范围及缺省值见注1 |
| endTime   | long     | FALSE    | 近点时间，以createTime进行检索，取值范围及缺省值见注2 |
| sort      | string   | FALSE    | 检索方向，asc 由远及近, desc 由近及远，缺省值desc     |
| limit     | int      | FALSE    | 单页最大返回条目数量 [1,500] （缺省值100）            |
| fromId    | long     | FALSE    | 起始充币订单ID，仅在下页查询时有效见注3               |

注1：<br>
startTime取值范围：[(endTime - 30天), endTime]<br>
startTime缺省值：(endTime - 30天)<br>

注2：<br>
endTime取值范围：不限<br>
endTime缺省值：当前时间<br>

注3：<br>
仅当用户请求查询的时间范围内的数据条目超出单页限制（由“limit“字段设定）时，服务器才返回”nextId“字段。用户收到服务器返回的”nextId“后 –<br>
1）须知晓后续仍有数据未能在本页返回；<br>
2）如需继续查询下页数据，应再次请求查询并将服务器返回的“nextId”作为“fromId“，其它请求参数不变。<br>
3）作为数据库记录ID，“nextId”和“fromId”除了用来翻页查询外，无其它业务含义。<br>


> Response:

```json
{
    "code": 200,
    "data": [
        {
            "id": 33419472,
            "currency": "ltc",
            "chain": "ltc",
            "amount": 0.001000000000000000,
            "address": "LUuuPs5C5Ph3cZz76ZLN1AMLSstqG5PbAz",
            "state": "safe",
            "txHash": "847601d249861da56022323514870ddb96456ec9579526233d53e690264605a7",
            "addressTag": "",
            "createTime": 1587033225787,
            "updateTime": 1587033716616
        }
    ]
}
```

### 响应数据

| 参数名称     | 是否必须 | 数据类型   | 描述                                                         | 取值范围     |
| ------------ | -------- | ---------- | ------------------------------------------------------------ | ------------ |
| code         | true     | int        | 状态码                                                       |              |
| message      | false    | string     | 错误描述（如有）                                             |              |
| data         | true     | object     |                                                              |              |
| {  id        | true     | long       | 充币订单id                                                   |              |
| currency     | true     | string     | 币种                                                         |              |
| txHash       | true     | string     | 交易哈希                                                     |              |
| chain        | true     | string     | 链名称                                                       |              |
| amount       | true     | bigdecimal | 个数                                                         |              |
| address      | true     | string     | 地址                                                         |              |
| addressTag   | true     | string     | 地址标签                                                     |              |
| state        | true     | string     | 状态                                                         | 状态参见下表 |
| createTime   | true     | long       | 发起时间                                                     |              |
| updateTime } | true     | long       | 最后更新时间                                                 |              |
| nextId       | false    | long       | 下页起始编号（充币订单ID，仅在查询结果需要分页返回时，包含此字段） |              |

- 虚拟币充值状态定义：

| 状态       | 描述     |
| ---------- | -------- |
| unknown    | 状态未知 |
| confirming | 确认中   |
| confirmed  | 已确认   |
| safe       | 已完成   |
| orphan     | 待确认   |

## 子用户余额（汇总）

API Key 权限：读取<br>
限频值（NEW）：2次/2s

母用户查询其下所有子用户的各币种汇总余额

### HTTP 请求

- GET `/v1/subuser/aggregate-balance`

### 请求参数

无

> Response:

```json
{
  "status": "ok",
  "data": [
      {
        "currency": "eos",
        "type": "spot",
        "balance": "1954559.809500000000000000"
      },
      {
        "currency": "btc",
        "type": "spot",
        "balance": "0.000000000000000000"
      },
      {
        "currency": "usdt",
        "type": "spot",
        "balance": "2925209.411300000000000000"
      },
      ...
   ]
}
```

### 响应数据

| 参数   | 是否必填 | 数据类型 | 长度 | 说明 | 取值范围        |      |
| ------ | -------- | -------- | ---- | ---- | --------------- | ---- |
| status | true     |          | -    | 状态 | "OK" or "Error" |      |
| data   | true     | list     | -    |      | -               |      |

- data 

| 参数     | 是否必填 | 数据类型 | 长度 | 说明                                 | 取值范围                                                     |      |
| -------- | -------- | -------- | ---- | ------------------------------------ | ------------------------------------------------------------ | ---- |
| currency | 是       | string   | -    | 币种                                 | -                                                            |      |
| type     | 是       | string   | -    | 账户类型                             | spot：现货账户，point：点卡账户, margin:逐仓杠杆账户，super-margin：全仓杠杆账户 |      |
| balance  | 是       | string   | -    | 账户余额（可用余额和冻结余额的总和） | -                                                            |      |

## 子用户余额

API Key 权限：读取<br>
限频值（NEW）：20次/2s

母用户查询子用户各币种账户余额

### HTTP 请求

- GET `/v1/account/accounts/{sub-uid}`

### 请求参数

| 参数    | 是否必填 | 数据类型 | 长度 | 说明         | 取值范围 |      |
| ------- | -------- | -------- | ---- | ------------ | -------- | ---- |
| sub-uid | true     | long     | -    | 子用户的 UID | -        |      |

> Response:

```json
{
  "status": "ok",
	"data": [
    {
      "id": 9910049,
      "type": "spot",
      "list": 
      [
        {
          "currency": "btc",
          "type": "trade",
          "balance": "1.00"
        },
        {
          "currency": "eth",
          "type": "trade",
          "balance": "1934.00"
        }
      ]
    },
    {
      "id": 9910050,
      "type": "point",
      "list": []
    }
	]
}
```

### 响应数据


| 参数 | 是否必填 | 数据类型 | 长度 | 说明       | 取值范围                                                     |      |
| ---- | -------- | -------- | ---- | ---------- | ------------------------------------------------------------ | ---- |
| id   | -        | long     | -    | 子用户 UID | -                                                            |      |
| type | -        | string   | -    | 账户类型   | spot：现货账户，point：点卡账户, margin:逐仓杠杆账户，super-margin：全仓杠杆账户 |      |
| list | -        | object   | -    | -          | -                                                            |      |

- list
	
| 参数     | 是否必填 | 数据类型 | 长度 | 说明     | 取值范围                          |      |
| -------- | -------- | -------- | ---- | -------- | --------------------------------- | ---- |
| currency | -        | string   | -    | 币种     | -                                 |      |
| type     | -        | string   | -    | 账户类型 | trade：交易账户，frozen：冻结账户 |      |
| balance  | -        | decimal  | -    | 账户余额 | -                                 |      |


# 现货 / 杠杆交易

## 简介

现货/杠杆交易接口提供了下单、撤单、订单查询、成交查询、手续费率查询等功能。

<aside class="notice">访问交易相关的接口需要进行签名认证。</aside>

以下是交易相关接口返回的返回码以及说明。

| 返回码                                                       | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| base-argument-unsupported                                    | 某参数不支持，请检查参数                                     |
| base-system-error                                            | 系统错误，如果是撤单：缓存中查不到订单状态，该订单无法撤单；如果是下单：订单入缓存失败，请再次尝试 |
| login-required                                               | url中没有Signature参数或找不到此用户（key与账户id不对应等情况） |
| parameter-required                                           | 止盈止损订单缺少参数 stop-price或operator                    |
| base-record-invalid                                          | 暂时未找到数据，请稍后重试                                   |
| order-amount-over-limit                                      | 订单数量超出限额                                             |
| base-symbol-trade-disabled                                   | 该交易对被禁止交易                                           |
| base-operation-forbidden                                     | 用户不在白名单内或该币种不允许OTC交易等禁止行为              |
| account-get-accounts-inexistent-error                        | 该账户在该用户下不存在                                       |
| account-account-id-inexistent                                | 该账户不存在                                                 |
| operation-forbidden-for-fl-account-state                     | 账户爆仓状态下禁止订单操作                                   |
| sub-user-auth-required                                       | 子用户未开通逐仓杠杆权限                                     |
| order-disabled                                               | 交易对暂停，无法下单                                         |
| cancel-disabled                                              | 交易对暂停，无法撤单                                         |
| order-invalid-price                                          | 下单价格非法（如市价单不能有价格，或限价单价格超过市场价10%） |
| order-accountbalance-error                                   | 账户余额不足                                                 |
| order-limitorder-price-min-error                             | 卖出价格不能低于指定价格                                     |
| order-limitorder-price-max-error                             | 买入价格不能高于指定价格                                     |
| order-limitorder-amount-min-error                            | 下单数量不能低于指定数量                                     |
| order-limitorder-amount-max-error                            | 下单数量不能高于指定数量                                     |
| order-etp-nav-price-min-error                                | 下单价格不能低于净值的指定比率                               |
| order-etp-nav-price-max-error                                | 下单价格不能高于净值等指定比率                               |
| order-orderprice-precision-error                             | 交易价格精度错误                                             |
| order-orderamount-precision-error                            | 交易数额精度错误                                             |
| order-value-min-error                                        | 订单交易额不能低于指定额度                                   |
| order-marketorder-amount-min-error                           | 卖出数量不能低于指定数量                                     |
| order-marketorder-amount-buy-max-error                       | 市价单买入额度不能高于指定额度                               |
| order-marketorder-amount-sell-max-error                      | 市价单卖出数量不能高于指定数量                               |
| order-holding-limit-failed                                   | 下单超出该币种的持仓限额                                     |
| order-type-invalid                                           | 订单类型非法                                                 |
| order-orderstate-error                                       | 订单状态错误                                                 |
| order-date-limit-error                                       | 查询时间不能超过系统限制                                     |
| order-source-invalid                                         | 订单来源非法                                                 |
| order-update-error                                           | 更新数据错误                                                 |
| order-fl-cancellation-is-disallowed                          | 禁止撤销爆仓单                                               |
| operation-forbidden-for-fl-account-state                     | 账户爆仓状态下禁止订单操作                                   |
| operation-forbidden-for-lock-account-state                   | 账户lock状态下禁止订单操作或c2c借款账户被禁止下撤单          |
| fl-order-already-existed                                     | 爆仓单已经存在 而且未成交                                    |
| order-user-cancel-forbidden                                  | 订单类型为IOC或FOK 不允许撤单                                |
| account-state-invalid                                        | 不支持的爆仓账户状态                                         |
| order-price-greater-than-limit                               | 下单价格高于开盘前下单限制价格，请重新下单                   |
| order-price-less-than-limit                                  | 下单价格低于开盘前下单限制价格，请重新下单                   |
| order-stop-order-hit-trigger                                 | 止盈止损单下单被当前价触发                                   |
| market-orders-not-support-during-limit-price-trading         | 限时下单不支持市价单                                         |
| price-exceeds-the-protective-price-during-limit-price-trading | 限价时间内价格超出保护价                                     |
| invalid-client-order-id                                      | client order id 在最近的下单或撤单参数中已被使用             |
| invalid-interval                                             | 查询起止窗口设置错误                                         |
| invalid-start-date                                           | 查询起始日期含非法取值                                       |
| invalid-end-date                                             | 查询起始日期含非法取值                                       |
| invalid-start-time                                           | 查询起始时间含非法取值                                       |
| invalid-end-time                                             | 查询起始时间含非法取值                                       |
| validation-constraints-required                              | 指定的必填参数缺失                                           |
| symbol-not-support                                           | 交易对不支持，全仓杠杆或c2c                                  |
| not-found                                                    | 撤单时订单不存在                                             |
| base-not-found                                               | 撤单时无效clientorderid撤单过多，一个小时后再重试            |

## 下单

API Key 权限：交易
限频值；100次/2s

发送一个新订单到火币以进行撮合。

### HTTP 请求

- POST ` /v1/order/orders/place`

> Request:

```json
{
  "account-id": "100009",
  "amount": "10.1",
  "price": "100.1",
  "source": "api",
  "symbol": "ethusdt",
  "type": "buy-limit",
  "client-order-id": "a0001"
}
```

### 请求参数

| 参数名称        | 数据类型 | 是否必需 | 默认值   | 描述                                                         |
| --------------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| account-id      | string   | true     | NA       | 账户 ID，取值参考 `GET /v1/account/accounts`。现货交易使用 ‘spot’ 账户的 account-id；逐仓杠杆交易，请使用 ‘margin’ 账户的 account-id；全仓杠杆交易，请使用 ‘super-margin’ 账户的 account-id |
| symbol          | string   | true     | NA       | 交易对,即btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |
| type            | string   | true     | NA       | 订单类型，包括buy-market, sell-market, buy-limit, sell-limit, buy-ioc, sell-ioc, buy-limit-maker, sell-limit-maker（说明见下文）, buy-stop-limit, sell-stop-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| amount          | string   | true     | NA       | 订单交易量（市价买单为订单交易额）                           |
| price           | string   | false    | NA       | 订单价格（对市价单无效）                                     |
| source          | string   | false    | spot-api | 现货交易填写“spot-api”，逐仓杠杆交易填写“margin-api”，全仓杠杆交易填写“super-margin-api”, C2C杠杆交易填写"c2c-margin-api" |
| client-order-id | string   | false    | NA       | 用户自编订单号（最大长度64个字符，须在24小时内保持唯一性）   |
| stop-price      | string   | false    | NA       | 止盈止损订单触发价格                                         |
| operator        | string   | false    | NA       | 止盈止损订单触发价运算符 gte – greater than and equal (>=), lte – less than and equal (<=) |


**buy-limit-maker**

当“下单价格”>=“市场最低卖出价”，订单提交后，系统将拒绝接受此订单；

当“下单价格”<“市场最低卖出价”，提交成功后，此订单将被系统接受。

**sell-limit-maker**

当“下单价格”<=“市场最高买入价”，订单提交后，系统将拒绝接受此订单；

当“下单价格”>“市场最高买入价”，提交成功后，此订单将被系统接受。

> Response:

```json
{  
  "data": "59378"
}
```

### 响应数据

返回的主数据对象是一个对应下单单号的字符串。

如client order ID（在24小时内）被复用，节点将返回错误消息invalid.client.order.id。

## 批量下单

API Key 权限：交易<br>
限频值（NEW）：50次/2s<br>

一个批量最多10张订单

### HTTP 请求

- POST ` /v1/order/batch-orders`

> Request:

```json
[
	{
    "account-id": "123456",
    "price": "7801",
    "amount": "0.001",
    "symbol": "btcusdt",
    "type": "sell-limit",
    "client-order-id": "c1"
	},
	{
    "account-id": "123456",
    "price": "7802",
    "amount": "0.001",
    "symbol": "btcusdt",
    "type": "sell-limit",
    "client-order-id": "d2"
	}
]
```

### 请求参数

| 参数名称        | 数据类型 | 是否必需 | 默认值   | 描述                                                         |
| --------------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| [{ account-id   | string   | true     | NA       | 账户 ID，取值参考 `GET /v1/account/accounts`。现货交易使用 ‘spot’ 账户的 account-id；逐仓杠杆交易，请使用 ‘margin’ 账户的 account-id；全仓杠杆交易，请使用 ‘super-margin’ 账户的 account-id; C2C杠杆交易，请使用borrow账户的account-id |
| symbol          | string   | true     | NA       | 交易对,即btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |
| type            | string   | true     | NA       | 订单类型，包括buy-market, sell-market, buy-limit, sell-limit, buy-ioc, sell-ioc, buy-limit-maker, sell-limit-maker（说明见下文）, buy-stop-limit, sell-stop-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| amount          | string   | true     | NA       | 订单交易量（市价买单为订单交易额）                           |
| price           | string   | false    | NA       | 订单价格（对市价单无效）                                     |
| source          | string   | false    | spot-api | 现货交易填写“spot-api”，逐仓杠杆交易填写“margin-api”，全仓杠杆交易填写“super-margin-api”, C2C杠杆交易填写"c2c-margin-api" |
| client-order-id | string   | false    | NA       | 用户自编订单号（最大长度64个字符，须在24小时内保持唯一性）   |
| stop-price      | string   | false    | NA       | 止盈止损订单触发价格                                         |
| operator }]     | string   | false    | NA       | 止盈止损订单触发价运算符 gte – greater than and equal (>=), lte – less than and equal (<=) |

**buy-limit-maker**

当“下单价格”>=“市场最低卖出价”，订单提交后，系统将拒绝接受此订单；

当“下单价格”<“市场最低卖出价”，提交成功后，此订单将被系统接受。

**sell-limit-maker**

当“下单价格”<=“市场最高买入价”，订单提交后，系统将拒绝接受此订单；

当“下单价格”>“市场最高买入价”，提交成功后，此订单将被系统接受。

> Response:

```json
{
    "status": "ok",
    "data": [
        {
            "order-id": 61713400772,
            "client-order-id": "c1"
        },
        {
            "order-id": 61713400940,
            "client-order-id": "d2"
        }
    ]
}
```

### 响应数据

| 字段名称        | 数据类型 | 描述                                 |
| --------------- | -------- | ------------------------------------ |
| [{ order-id     | integer  | 订单编号                             |
| client-order-id | string   | 用户自编订单号（如有）               |
| err-code        | string   | 订单被拒错误码（仅对被拒订单有效）   |
| err-msg }]      | string   | 订单被拒错误信息（仅对被拒订单有效） |

如client order ID（在24小时内）被复用，节点返回先前订单的order ID及client order ID。

## 撤销订单

API Key 权限：交易<br>
限频值（NEW）：100次/2s

此接口发送一个撤销订单的请求。

<aside class="warning">此接口只提交取消请求，实际取消结果需要通过订单状态，撮合状态等接口来确认。</aside>
### HTTP 请求

- POST ` /v1/order/orders/{order-id}/submitcancel`


### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述               | 默认值 | 取值范围 |
| -------- | -------- | ------ | ------------------ | ------ | -------- |
| order-id | true     | string | 订单ID，填在path中 |        |          |


> Success response:

```json
{  
  "data": "59378"
}
```

### 响应数据

返回的主数据对象是一个对应下单单号的字符串。

### 错误码

> Failure response:

```json
{
  "status": "error",
  "err-code": "order-orderstate-error",
  "err-msg": "订单状态错误",
  "order-state":-1 // 当前订单状态
}
```

返回字段列表中，order-state的可能取值包括 -

| order-state | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| -1          | order was already closed in the long past (order state = canceled, partial-canceled, filled, partial-filled) |
| 5           | partial-canceled                                             |
| 6           | filled                                                       |
| 7           | canceled                                                     |
| 10          | cancelling                                                   |

## 撤销订单（基于client order ID）

API Key 权限：交易<br>
限频值（NEW）：100次/2s

此接口发送一个撤销订单的请求。

<aside class="notice">撤单个订单建议通过接口/v1/order/orders/{order-id}/submitcancel，会更快更稳定</aside>
<aside class="warning">此接口只提交取消请求，实际取消结果需要通过订单状态，撮合状态等接口来确认。</aside>

### HTTP 请求

- POST ` /v1/order/orders/submitCancelClientOrder`

> Request:

```json
{
  "client-order-id": "a0001"
}
```

### 请求参数

| 参数名称        | 是否必须 | 类型   | 描述                                                         | 默认值 | 取值范围 |
| --------------- | -------- | ------ | ------------------------------------------------------------ | ------ | -------- |
| client-order-id | true     | string | 用户自编订单号，必须已有该订单存在，否则下次下单时不允许用此值 |        |          |


> Response:

```json
{  
  "data": "10"
}
```
### 响应数据

| 字段名称 | 数据类型 | 描述       |
| -------- | -------- | ---------- |
| data     | integer  | 撤单状态码 |

| Status Code | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| -1          | order was already closed in the long past (order state = canceled, partial-canceled, filled, partial-filled) |
| 0           | client-order-id not found                                    |
| 5           | partial-canceled                                             |
| 6           | filled                                                       |
| 7           | canceled                                                     |
| 10          | cancelling                                                   |


## 查询当前未成交订单

API Key 权限：读取<br>
限频值（NEW）：50次/2s

查询已提交但是仍未完全成交或未被撤销的订单。

### HTTP 请求

- GET `/v1/order/openOrders`

> Request:

```json
{
   "account-id": "100009",
   "symbol": "ethusdt",
   "side": "buy"
}
```

### 请求参数

| 参数名称   | 数据类型 | 是否必需                                         | 默认值 | 描述                                                         |
| ---------- | -------- | ------------------------------------------------ | ------ | ------------------------------------------------------------ |
| account-id | string   | true                                             | NA     | 账户 ID，取值参考 `GET /v1/account/accounts`。现货交易使用‘spot’账户的 account-id；逐仓杠杆交易，请使用 ‘margin’ 账户的 account-id；全仓杠杆交易，请使用 ‘super-margin’ 账户的 account-id；c2c杠杆交易，请使用borrow账户的account-id |
| symbol     | string   | ture                                             | NA     | 交易对,即btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |
| side       | string   | false                                            | both   | 指定只返回某一个方向的订单，可能的值有: buy, sell. 默认两个方向都返回。 |
| from       | string   | false                                            |        | 查询起始 ID，如果是向后查询，则赋值为上一次查询结果中得到的最后一条id ；如果是向前查询，则赋值为上一次查询结果中得到的第一条id |
| direct     | string   | false (如字段'from'已设定，此字段'direct'为必填) |        | 查询方向，prev 向前；next 向后                               |
| size       | int      | false                                            | 100    | 返回订单的数量，最大值500。                                  |

> Response:

```json
{  
  "data": [
    {
      "id": 5454937,
      "symbol": "ethusdt",
      "account-id": 30925,
      "amount": "1.000000000000000000",
      "price": "0.453000000000000000",
      "created-at": 1530604762277,
      "type": "sell-limit",
      "filled-amount": "0.0",
      "filled-cash-amount": "0.0",
      "filled-fees": "0.0",
      "source": "web",
      "state": "submitted"
    }
  ]
}
```

### 响应数据

| 字段名称           | 数据类型 | 描述                                                         |
| ------------------ | -------- | ------------------------------------------------------------ |
| id                 | integer  | 订单id，无大小顺序，可作为下一次翻页查询请求的from字段       |
| client-order-id    | string   | 用户自编订单号（所有open订单可返回client-order-id）          |
| symbol             | string   | 交易对, 例如btcusdt, ethbtc                                  |
| price              | string   | limit order的交易价格                                        |
| created-at         | int      | 订单创建的调整为新加坡时间的时间戳，单位毫秒                 |
| type               | string   | 订单类型                                                     |
| filled-amount      | string   | 订单中已成交部分的数量                                       |
| filled-cash-amount | string   | 订单中已成交部分的总价格                                     |
| filled-fees        | string   | 已交交易手续费总额                                           |
| source             | string   | 现货交易填写“api”                                            |
| state              | string   | 订单状态，包括submitted, partial-filled, cancelling, created |
| stop-price         | string   | 止盈止损订单触发价格                                         |
| operator           | string   | 止盈止损订单触发价运算符                                     |

## 批量撤销订单（open orders）

API Key 权限：交易<br>
限频值（NEW）：50次/2s

此接口发送批量撤销订单的请求。

<aside class="warning">此接口只提交取消请求，实际取消结果需要通过订单状态，撮合状态等接口来确认。</aside>
### HTTP 请求

- POST ` /v1/order/orders/batchCancelOpenOrders`


### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                                                         | 默认值 | 取值范围                                          |
| ---------- | -------- | ------ | ------------------------------------------------------------ | ------ | ------------------------------------------------- |
| account-id | false    | string | 账户ID，取值参考 `GET /v1/account/accounts`                  |        |                                                   |
| symbol     | false    | string | 交易代码列表（最多10 个symbols，多个交易代码间以逗号分隔），btcusdt, ethbtc...（取值参考`/v1/common/symbols`） | all    |                                                   |
| side       | false    | string | 主动交易方向                                                 |        | “buy”或“sell”，缺省将返回所有符合条件尚未成交订单 |
| size       | false    | int    | 所需返回记录数                                               | 100    | [0,100]                                           |


> Response:

```json
{
  "status": "ok",
  "data": {
    "success-count": 2,
    "failed-count": 0,
    "next-id": 5454600
  }
}
```


### 响应数据


| 参数名称      | 是否必须 | 数据类型 | 描述                       | 取值范围 |
| ------------- | -------- | -------- | -------------------------- | -------- |
| success-count | true     | int      | 成功取消的订单数           |          |
| failed-count  | true     | int      | 取消失败的订单数           |          |
| next-id       | true     | long     | 下一个符合取消条件的订单号 |          |

## 批量撤销订单

API Key 权限：交易<br>
限频值（NEW）：50次/2s

此接口同时为多个订单（基于id）发送取消请求。

### HTTP 请求

- POST ` /v1/order/orders/batchcancel`

> Request:

```json
{
  "client-order-ids": [
   "5983466", "5722939", "5721027", "5719487"
  ]
}
```

### 请求参数

| 参数名称         | 是否必须 | 类型     | 描述                                                         | 默认值 | 取值范围           |
| ---------------- | -------- | -------- | ------------------------------------------------------------ | ------ | ------------------ |
| order-ids        | false    | string[] | 订单编号列表（order-ids和client-order-ids必须且只能选一个填写，不超过50张订单），建议通过order-ids来撤单，比client-order-ids更快更稳定 |        | 单次不超过50个订单 |
| client-order-ids | false    | string[] | 用户自编订单号列表（order-ids和client-order-ids必须且只能选一个填写，不超过50张订单），必须已有该订单存在，否则下次下单时不允许用此值 |        | 单次不超过50个订单 |

> Response:

```json
{
    "status": "ok",
    "data": {
        "success": [
            "5983466"            
        ],
        "failed": [
            {
              "err-msg": "Incorrect order state",
              "order-state": 7,
              "order-id": "",
              "err-code": "order-orderstate-error",
              "client-order-id": "first"
            },
            {
              "err-msg": "Incorrect order state",
              "order-state": 7,
              "order-id": "",
              "err-code": "order-orderstate-error",
              "client-order-id": "second"
            },
            {
              "err-msg": "The record is not found.",
              "order-id": "",
              "err-code": "base-not-found",
              "client-order-id": "third"
            }
          ]
    }
}
```

### 响应数据

| 字段名称  | 数据类型 | 描述                                                         |
| --------- | -------- | ------------------------------------------------------------ |
| { success | string[] | 撤单成功订单列表（可为order-id列表或client-order-id列表，以用户请求为准） |
| failed }  | string[] | 撤单失败订单列表（可为order-id列表或client-order-id列表，以用户请求为准） |

撤单失败订单列表 -

| 字段名称        | 数据类型 | 描述                                                         |
| --------------- | -------- | ------------------------------------------------------------ |
| [{ order-id     | string   | 订单编号（如用户创建订单时包含order-id，返回中也须包含此字段） |
| client-order-id | string   | 用户自编订单号（如用户创建订单时包含client-order-id，返回中也须包含此字段） |
| err-code        | string   | 订单被拒错误码（仅对被拒订单有效）                           |
| err-msg         | string   | 订单被拒错误信息（仅对被拒订单有效）                         |
| order-state }]  | string   | 当前订单状态（若有）                                         |

返回字段列表中，order-state的可能取值包括 -

| order-state | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| -1          | order was already closed in the long past (order state = canceled, partial-canceled, filled, partial-filled) |
| 5           | partial-canceled                                             |
| 6           | filled                                                       |
| 7           | canceled                                                     |
| 10          | cancelling                                                   |

## 查询订单详情

API Key 权限：读取<br>
限频值（NEW）：50次/2s

此接口返回指定订单的最新状态和详情。通过API创建的订单，撤销超过2小时后无法查询。

### HTTP 请求

- GET `/v1/order/orders/{order-id}`


### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述               | 默认值 | 取值范围 |
| -------- | -------- | ------ | ------------------ | ------ | -------- |
| order-id | true     | string | 订单ID，填在path中 |        |          |


> Response:

```json
{  
  "data": 
  {
    "id": 59378,
    "symbol": "ethusdt",
    "account-id": 100009,
    "amount": "10.1000000000",
    "price": "100.1000000000",
    "created-at": 1494901162595,
    "type": "buy-limit",
    "field-amount": "10.1000000000",
    "field-cash-amount": "1011.0100000000",
    "field-fees": "0.0202000000",
    "finished-at": 1494901400468,
    "user-id": 1000,
    "source": "api",
    "state": "filled",
    "canceled-at": 0
  }
}
```

### 响应数据

| 字段名称          | 是否必须 | 数据类型 | 描述                                                         | 取值范围                                                     |
| ----------------- | -------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| account-id        | true     | long     | 账户 ID                                                      |                                                              |
| amount            | true     | string   | 订单数量                                                     |                                                              |
| canceled-at       | false    | long     | 订单撤销时间                                                 |                                                              |
| created-at        | true     | long     | 订单创建时间                                                 |                                                              |
| field-amount      | true     | string   | 已成交数量                                                   |                                                              |
| field-cash-amount | true     | string   | 已成交总金额                                                 |                                                              |
| field-fees        | true     | string   | 已成交手续费（买入为币，卖出为钱）                           |                                                              |
| finished-at       | false    | long     | 订单变为终结态的时间，不是成交时间，包含“已撤单”状态         |                                                              |
| id                | true     | long     | 订单ID                                                       |                                                              |
| client-order-id   | false    | string   | 用户自编订单号（所有open订单可返回client-order-id（如有）；仅7天内（基于订单创建时间）的closed订单（state <> canceled）可返回client-order-id（如有）；仅24小时内（基于订单创建时间）的closed订单（state = canceled）可返回client-order-id（如有）） |                                                              |
| price             | true     | string   | 订单价格                                                     |                                                              |
| source            | true     | string   | 订单来源                                                     | api                                                          |
| state             | true     | string   | 订单状态                                                     | submitted 已提交, partial-filled 部分成交, partial-canceled 部分成交撤销, filled 完全成交, canceled 已撤销， created |
| symbol            | true     | string   | 交易对                                                       | btcusdt, ethbtc, rcneth ...                                  |
| type              | true     | string   | 订单类型                                                     | buy-market：市价买, sell-market：市价卖, buy-limit：限价买, sell-limit：限价卖, buy-ioc：IOC买单, sell-ioc：IOC卖单， buy-limit-maker, sell-limit-maker, buy-stop-limit，sell-stop-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| stop-price        | false    | string   | 止盈止损订单触发价格                                         |                                                              |
| operator          | false    | string   | 止盈止损订单触发价运算符                                     | gte,lte                                                      |


## 查询订单详情（基于client order ID）

API Key 权限：读取<br>
限频值（NEW）：50次/2s

此接口返回指定用户自编订单号（24小时内）的订单最新状态和详情。通过API创建的订单，撤销超过2小时后无法查询。

### HTTP 请求

- GET `/v1/order/orders/getClientOrder`

### 请求参数

| 参数名称      | 是否必须 | 类型   | 描述           | 默认值 | 取值范围 |
| ------------- | -------- | ------ | -------------- | ------ | -------- |
| clientOrderId | true     | string | 用户自编订单号 |        |          |

> Response:

```json
{  
  "data": 
  {
    "id": 59378,
    "symbol": "ethusdt",
    "account-id": 100009,
    "amount": "10.1000000000",
    "price": "100.1000000000",
    "created-at": 1494901162595,
    "type": "buy-limit",
    "field-amount": "10.1000000000",
    "field-cash-amount": "1011.0100000000",
    "field-fees": "0.0202000000",
    "finished-at": 1494901400468,
    "user-id": 1000,
    "source": "api",
    "state": "filled",
    "canceled-at": 0
  }
}
```

### 响应数据

| 字段名称          | 是否必须 | 数据类型 | 描述                                                         | 取值范围                                                     |
| ----------------- | -------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| account-id        | true     | long     | 账户 ID                                                      |                                                              |
| amount            | true     | string   | 订单数量                                                     |                                                              |
| canceled-at       | false    | long     | 订单撤销时间                                                 |                                                              |
| created-at        | true     | long     | 订单创建时间                                                 |                                                              |
| field-amount      | true     | string   | 已成交数量                                                   |                                                              |
| field-cash-amount | true     | string   | 已成交总金额                                                 |                                                              |
| field-fees        | true     | string   | 已成交手续费（买入为币，卖出为钱）                           |                                                              |
| finished-at       | false    | long     | 订单变为终结态的时间，不是成交时间，包含“已撤单”状态         |                                                              |
| id                | true     | long     | 订单ID                                                       |                                                              |
| client-order-id   | false    | string   | 用户自编订单号（仅24小时内（基于订单创建时间）的订单可被查询.） |                                                              |
| price             | true     | string   | 订单价格                                                     |                                                              |
| source            | true     | string   | 订单来源                                                     | api                                                          |
| state             | true     | string   | 订单状态                                                     | submitted 已提交, partial-filled 部分成交, partial-canceled 部分成交撤销, filled 完全成交, canceled 已撤销，created |
| symbol            | true     | string   | 交易对                                                       | btcusdt, ethbtc, rcneth ...                                  |
| type              | true     | string   | 订单类型                                                     | buy-market：市价买, sell-market：市价卖, buy-limit：限价买, sell-limit：限价卖, buy-ioc：IOC买单, sell-ioc：IOC卖单， buy-limit-maker, sell-limit-maker, buy-stop-limit，sell-stop-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| stop-price        | false    | string   | 止盈止损订单触发价格                                         |                                                              |
| operator          | false    | string   | 止盈止损订单触发价运算符                                     | gte,lte                                                      |

如client order ID不存在，返回如下错误信息 
{
    "status": "error",
    "err-code": "base-record-invalid",
    "err-msg": "record invalid",
    "data": null
}

## 成交明细

API Key 权限：读取<br>
限频值（NEW）：50次/2s

此接口返回指定订单的成交明细。

### HTTP 请求

- GET `/v1/order/orders/{order-id}/matchresults`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述               | 默认值 | 取值范围 |
| -------- | -------- | ------ | ------------------ | ------ | -------- |
| order-id | true     | string | 订单ID，填在path中 |        |          |


> Response:

```json
{  
  "data": [
    {
      "id": 29553,
      "order-id": 59378,
      "match-id": 59335,
      "trade-id": 100282808529,
      "symbol": "ethusdt",
      "type": "buy-limit",
      "source": "api",
      "price": "100.1000000000",
      "filled-amount": "9.1155000000",
      "filled-fees": "0.0182310000",
      "created-at": 1494901400435,
      "role": "maker",
      "filled-points": "0.0",
      "fee-deduct-currency": ""
    }
    ...
  ]
}
```

### 响应数据

<aside class="notice">返回的主数据对象为一个对象数组，其中每一个元件代表一个交易结果。</aside>
| 字段名称            | 是否必须 | 数据类型 | 描述                                                         | 取值范围                                                     |
| ------------------- | -------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| created-at          | true     | long     | 该成交记录创建的时间戳（略晚于成交时间）                     |                                                              |
| filled-amount       | true     | string   | 成交数量                                                     |                                                              |
| filled-fees         | true     | string   | 交易手续费（正值）或交易返佣金（负值）                       |                                                              |
| fee-currency        | true     | string   | 交易手续费或交易返佣币种（买单的交易手续费币种为基础币种，卖单的交易手续费币种为计价币种；买单的交易返佣币种为计价币种，卖单的交易返佣币种为基础币种） |                                                              |
| id                  | true     | long     | 订单成交记录ID                                               |                                                              |
| match-id            | true     | long     | 撮合ID，订单在撮合中执行的顺序ID                             |                                                              |
| order-id            | true     | long     | 订单ID，成交所属订单的ID                                     |                                                              |
| trade-id            | false    | integer  | Unique trade ID (NEW)唯一成交编号，成交时产生的唯一编号ID    |                                                              |
| price               | true     | string   | 成交价格                                                     |                                                              |
| source              | true     | string   | 订单来源                                                     | api                                                          |
| symbol              | true     | string   | 交易对                                                       | btcusdt, ethbtc, rcneth ...                                  |
| type                | true     | string   | 订单类型                                                     | buy-market：市价买, sell-market：市价卖, buy-limit：限价买, sell-limit：限价卖, buy-ioc：IOC买单, sell-ioc：IOC卖单， buy-limit-maker, sell-limit-maker, buy-stop-limit，sell-stop-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| role                | true     | string   | 成交角色                                                     | maker,taker                                                  |
| filled-points       | true     | string   | 抵扣数量（可为ht或hbpoint）                                  |                                                              |
| fee-deduct-currency | true     | string   | 抵扣类型                                                     | 如果为空，代表扣除的手续费是原币；如果为"ht"，代表抵扣手续费的是HT；如果为"hbpoint"，代表抵扣手续费的是点卡 |
| fee-deduct-state | true     | string   | 抵扣状态 | 抵扣中：ongoing，抵扣完成：done  |

注：<br>
- filled-fees中的交易返佣金额可能不会实时到账。<br>

## 搜索历史订单

API Key 权限：读取<br>
限频值（NEW）：50次/2s

此接口基于搜索条件查询历史订单。通过API创建的订单，撤销超过2小时后无法查询。

用户可选择以“时间范围”查询历史订单，以替代原先的以“日期范围“查询方式。

-	如用户填写start-time AND/OR end-time查询历史订单，服务器将按照用户指定的“时间范围“查询并返回，并忽略start-date/end-date参数。此方式的查询窗口大小限定为最大48小时，窗口平移范围为最近180天。

-	如用户不填写start-time/end-time参数，而填写start-date AND/OR end-date查询历史订单，服务器将按照用户指定的“日期范围“查询并返回。此方式的查询窗口大小限定为最大2天，窗口平移范围为最近180天。

-	如用户既不填写start-time/end-time参数，也不填写start-date/end-date参数，服务器将缺省以当前时间为end-time，返回最近48小时内的历史订单。

火币Global建议用户以“时间范围“查询历史订单。未来，火币Global将下线以”日期范围“查询历史订单的方式，并另行通知。


### HTTP 请求

- GET `/v1/order/orders`

> Request:

```json
{
   "account-id": "100009",
   "amount": "10.1",
   "price": "100.1",
   "source": "api",
   "symbol": "ethusdt",
   "type": "buy-limit"
}
```


### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                                                         | 默认值                      | 取值范围                                                     |
| ---------- | -------- | ------ | ------------------------------------------------------------ | --------------------------- | ------------------------------------------------------------ |
| symbol     | true     | string | 交易对                                                       |                             | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`）       |
| types      | false    | string | 查询的订单类型组合，使用逗号分割                             |                             | buy-market：市价买, sell-market：市价卖, buy-limit：限价买, sell-limit：限价卖, buy-ioc：IOC买单, sell-ioc：IOC卖单， buy-limit-maker, sell-limit-maker, buy-stop-limit，sell-stop-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| start-time | false    | long   | 查询开始时间, 时间格式UTC time in millisecond。 以订单生成时间进行查询 | -48h 查询结束时间的前48小时 | 取值范围 [((end-time) – 48h), (end-time)] ，查询窗口最大为48小时，窗口平移范围为最近180天，已完全撤销的历史订单的查询窗口平移范围只有最近2小时(state="canceled") |
| end-time   | false    | long   | 查询结束时间, 时间格式UTC time in millisecond。 以订单生成时间进行查询 | present                     | 取值范围 [(present-179d), present] ，查询窗口最大为48小时，窗口平移范围为最近180天，已完全撤销的历史订单的查询窗口平移范围只有最近2小时(state="canceled") |
| start-date | false    | string | 查询开始日期, 日期格式yyyy-mm-dd。 以订单生成时间进行查询    | -1d 查询结束日期的前1天     | 取值范围 [((end-date) – 1), (end-date)] ，查询窗口最大为2天，窗口平移范围为最近180天，已完全撤销的历史订单的查询窗口平移范围只有最近2小时(state="canceled") |
| end-date   | false    | string | 查询结束日期, 日期格式yyyy-mm-dd。 以订单生成时间进行查询    | today                       | 取值范围 [(today-179), today] ，查询窗口最大为2天，窗口平移范围为最近180天，已完全撤销的历史订单的查询窗口平移范围只有最近2小时(state="canceled") |
| states     | true     | string | 查询的订单状态组合，使用','分割                              |                             | submitted 已提交, partial-filled 部分成交, partial-canceled 部分成交撤销, filled 完全成交, canceled 已撤销，created |
| from       | false    | string | 查询起始 ID                                                  |                             | 如果是向后查询，则赋值为上一次查询结果中得到的最后一条id ；如果是向前查询，则赋值为上一次查询结果中得到的第一条id |
| direct     | false    | string | 查询方向                                                     |                             | prev 向前；next 向后                                         |
| size       | false    | string | 查询记录大小                                                 | 100                         | [1, 100]                                                     |


> Response:

```json
{  
  "data": [
    {
      "id": 59378,
      "symbol": "ethusdt",
      "account-id": 100009,
      "amount": "10.1000000000",
      "price": "100.1000000000",
      "created-at": 1494901162595,
      "type": "buy-limit",
      "field-amount": "10.1000000000",
      "field-cash-amount": "1011.0100000000",
      "field-fees": "0.0202000000",
      "finished-at": 1494901400468,
      "user-id": 1000,
      "source": "api",
      "state": "filled",
      "canceled-at": 0
    }
    ...
  ]
}
```

### 响应数据

| 参数名称          | 是否必须 | 数据类型 | 描述                                                         | 取值范围                                                     |
| ----------------- | -------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| account-id        | true     | long     | 账户 ID                                                      |                                                              |
| amount            | true     | string   | 订单数量                                                     |                                                              |
| canceled-at       | false    | long     | 接到撤单申请的时间                                           |                                                              |
| created-at        | true     | long     | 订单创建时间                                                 |                                                              |
| field-amount      | true     | string   | 已成交数量                                                   |                                                              |
| field-cash-amount | true     | string   | 已成交总金额                                                 |                                                              |
| field-fees        | true     | string   | 已成交手续费（买入为基础币，卖出为计价币）                   |                                                              |
| finished-at       | false    | long     | 最后成交时间                                                 |                                                              |
| id                | true     | long     | 订单ID，无大小顺序，可作为下一次翻页查询请求的from字段       |                                                              |
| client-order-id   | false    | string   | 用户自编订单号（所有open订单可返回client-order-id（如有）；仅7天内（基于订单创建时间）的closed订单（state <> canceled）可返回client-order-id（如有）；仅24小时内（基于订单创建时间）的closed订单（state = canceled）可被查询） |                                                              |
| price             | true     | string   | 订单价格                                                     |                                                              |
| source            | true     | string   | 订单来源                                                     | api                                                          |
| state             | true     | string   | 订单状态                                                     | submitted 已提交, partial-filled 部分成交, partial-canceled 部分成交撤销, filled 完全成交, canceled 已撤销，created |
| symbol            | true     | string   | 交易对                                                       | btcusdt, ethbtc, rcneth ...                                  |
| type              | true     | string   | 订单类型                                                     | submit-cancel：已提交撤单申请  ,buy-market：市价买, sell-market：市价卖, buy-limit：限价买, sell-limit：限价卖, buy-ioc：IOC买单, sell-ioc：IOC卖单， buy-limit-maker, sell-limit-maker, buy-stop-limit，sell-stop-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| stop-price        | false    | string   | 止盈止损订单触发价格                                         |                                                              |
| operator          | false    | string   | 止盈止损订单触发价运算符                                     | gte,lte                                                      |

### start-date, end-date相关错误码

| 错误码             | 对应错误场景                                                 |
| ------------------ | ------------------------------------------------------------ |
| invalid_interval   | start date小于end date; 或者 start date 与end date之间的时间间隔大于2天 |
| invalid_start_date | start date是一个180天之前的日期；或者start date是一个未来的日期 |
| invalid_end_date   | end date 是一个180天之前的日期；或者end date是一个未来的日期 |

## 搜索最近48小时内历史订单

API Key 权限：读取<br>
限频值（NEW）：20次/2s

此接口基于搜索条件查询最近48小时内历史订单。通过API创建的订单，撤销超过2小时后无法查询。

### HTTP 请求

- GET `/v1/order/history`

> Request:

```json
{
   "symbol": "btcusdt",
   "start-time": "1556417645419",
   "end-time": "1556533539282",
   "direct": "prev",
   "size": "10"
}
```

### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                                                         | 默认值         | 取值范围                                               |
| ---------- | -------- | ------ | ------------------------------------------------------------ | -------------- | ------------------------------------------------------ |
| symbol     | false    | string | 交易对                                                       | all            | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |
| start-time | false    | long   | 查询起始时间（含）                                           | 48小时前的时刻 | UTC time in millisecond                                |
| end-time   | false    | long   | 查询结束时间（含）                                           | 查询时刻       | UTC time in millisecond                                |
| direct     | false    | string | 订单查询方向（注：仅在检索出的总条目数量超出size字段限定时起作用；如果检索出的总条目数量在size 字段限定内，direct 字段不起作用。） | next           | prev 向前, next 向后                                   |
| size       | false    | int    | 每次返回条目数量                                             | 100            | [10,1000]                                              |

> Response:

```json
{
    "status": "ok",
    "data": [
        {
            "id": 31215214553,
            "symbol": "btcusdt",
            "account-id": 4717043,
            "amount": "1.000000000000000000",
            "price": "1.000000000000000000",
            "created-at": 1556533539282,
            "type": "buy-limit",
            "field-amount": "0.0",
            "field-cash-amount": "0.0",
            "field-fees": "0.0",
            "finished-at": 1556533568953,
            "source": "web",
            "state": "canceled",
            "canceled-at": 1556533568911
        }
    ]
}
```

### 响应数据

| 参数名称          | 是否必须 | 数据类型 | 描述                                                         | 取值范围                                                     |
| ----------------- | -------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| {account-id       | true     | long     | 账户 ID                                                      |                                                              |
| amount            | true     | string   | 订单数量                                                     |                                                              |
| canceled-at       | false    | long     | 接到撤单申请的时间                                           |                                                              |
| created-at        | true     | long     | 订单创建时间                                                 |                                                              |
| field-amount      | true     | string   | 已成交数量                                                   |                                                              |
| field-cash-amount | true     | string   | 已成交总金额                                                 |                                                              |
| field-fees        | true     | string   | 已成交手续费（买入为基础币，卖出为计价币）                   |                                                              |
| finished-at       | false    | long     | 最后成交时间                                                 |                                                              |
| id                | true     | long     | 订单ID，无大小顺序                                           |                                                              |
| client-order-id   | false    | string   | 用户自编订单号（仅48小时内（基于订单创建时间）的closed订单（state <> canceled）可返回client-order-id（如有）；仅24小时内（基于订单创建时间）的closed订单（state = canceled）可被查询） |                                                              |
| price             | true     | string   | 订单价格                                                     |                                                              |
| source            | true     | string   | 订单来源                                                     | api                                                          |
| state             | true     | string   | 订单状态                                                     | partial-canceled 部分成交撤销, filled 完全成交, canceled 已撤销 |
| symbol            | true     | string   | 交易对                                                       | btcusdt, ethbtc, rcneth ...                                  |
| stop-price        | false    | string   | 止盈止损订单触发价格                                         |                                                              |
| operator          | false    | string   | 止盈止损订单触发价运算符                                     | gte,lte                                                      |
| type}             | true     | string   | 订单类型                                                     | buy-market：市价买, sell-market：市价卖, buy-limit：限价买, sell-limit：限价卖, buy-ioc：IOC买单, sell-ioc：IOC卖单, buy-limit-maker, sell-limit-maker, buy-limit-maker, sell-limit-maker, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| next-time         | false    | long     | 下一查询起始时间（当请求字段”direct”为”prev”时有效）, 下一查询结束时间（当请求字段”direct”为”next”时有效）。注：仅在检索出的总条目数量超出size字段限定时，此返回字段存在。 | UTC time in millisecond                                      |


## 当前和历史成交

API Key 权限：读取<br>
限频值（NEW）：20次/2s

此接口基于搜索条件查询当前和历史成交记录。

### HTTP 请求

- GET `/v1/order/matchresults`


### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                                           | 默认值                  | 取值范围                                                     |
| ---------- | -------- | ------ | ---------------------------------------------- | ----------------------- | ------------------------------------------------------------ |
| symbol     | true     | string | 交易对                                         | N/A                     | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`）       |
| types      | false    | string | 查询的订单类型组合，使用','分割                | all                     | buy-market：市价买, sell-market：市价卖, buy-limit：限价买, sell-limit：限价卖, buy-ioc：IOC买单, sell-ioc：IOC卖单, buy-limit-maker, sell-limit-maker, buy-stop-limit, sell-stop-limit |
| start-date | false    | string | 查询开始日期（新加坡时区）日期格式yyyy-mm-dd   | -1d 查询结束日期的前1天 | 取值范围 [((end-date) – 1), (end-date)] ，查询窗口最大为2天，窗口平移范围为最近61天。 |
| end-date   | false    | string | 查询结束日期（新加坡时区）, 日期格式yyyy-mm-dd | today                   | 取值范围 [(today-60), today] ，查询窗口最大为2天，窗口平移范围为最近61天 |
| from       | false    | string | 查询起始 ID                                    | N/A                     | 如果是向后查询，则赋值为上一次查询结果中得到的最后一条id（不是trade-id） ；如果是向前查询，则赋值为上一次查询结果中得到的第一条id（不是trade-id） |
| direct     | false    | string | 查询方向                                       | next                    | prev 向前；next 向后                                         |
| size       | false    | string | 查询记录大小                                   | 100                     | [1，500]                                                     |

> Response:

```json
{  
  "data": [
    {
      "id": 29553,
      "order-id": 59378,
      "match-id": 59335,
      "symbol": "ethusdt",
      "type": "buy-limit",
      "source": "api",
      "price": "100.1000000000",
      "filled-amount": "9.1155000000",
      "filled-fees": "0.0182310000",
      "created-at": 1494901400435,
      "trade-id": 100282808529,
      "role": taker,
      "filled-points": "0.0",
      "fee-deduct-currency": ""
    }
    ...
  ]
}
```

### 响应数据

<aside class="notice">返回的主数据对象为一个对象数组，其中每一个元件代表一个交易结果。</aside>
| 参数名称            | 是否必须 | 数据类型 | 描述                                                         | 取值范围                                                     |
| ------------------- | -------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| created-at          | true     | long     | 该成交记录创建的时间戳（略晚于成交时间）                     |                                                              |
| filled-amount       | true     | string   | 成交数量                                                     |                                                              |
| filled-fees         | true     | string   | 交易手续费（正值）或交易返佣（负值）                         |                                                              |
| fee-currency        | true     | string   | 交易手续费或交易返佣币种（买单的交易手续费币种为基础币种，卖单的交易手续费币种为计价币种；买单的交易返佣币种为计价币种，卖单的交易返佣币种为基础币种） |                                                              |
| id                  | true     | long     | 订单成交记录 ID，无大小顺序，可作为下一次翻页查询请求的from字段 |                                                              |
| match-id            | true     | long     | 撮合 ID                                                      |                                                              |
| order-id            | true     | long     | 订单 ID                                                      |                                                              |
| trade-id            | false    | integer  | 唯一成交编号                                                 |                                                              |
| price               | true     | string   | 成交价格                                                     |                                                              |
| source              | true     | string   | 订单来源                                                     | api                                                          |
| symbol              | true     | string   | 交易对                                                       | btcusdt, ethbtc, rcneth ...                                  |
| type                | true     | string   | 订单类型                                                     | buy-market：市价买, sell-market：市价卖, buy-limit：限价买, sell-limit：限价卖, buy-ioc：IOC买单, sell-ioc：IOC卖单， buy-limit-maker, sell-limit-maker, buy-stop-limit，sell-stop-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| role                | true     | string   | 成交角色                                                     | maker,taker                                                  |
| filled-points       | true     | string   | 抵扣数量（可为ht或hbpoint）                                  |                                                              |
| fee-deduct-currency | true     | string   | 抵扣类型                                                     | ht,hbpoint                                                   |
| fee-deduct-state | true     | string   | 抵扣状态 | 抵扣中：ongoing，抵扣完成：done  |

注：<br>
- filled-fees中的交易返佣金额可能不会实时到账；<br>

### start-date, end-date相关错误码 

| 错误码             | 对应错误场景                                                 |
| ------------------ | ------------------------------------------------------------ |
| invalid_interval   | start date小于end date; 或者 start date 与end date之间的时间间隔大于2天 |
| invalid_start_date | start date是一个61天之前的日期；或者start date是一个未来的日期 |
| invalid_end_date   | end date 是一个61天之前的日期；或者end date是一个未来的日期  |


## 获取用户当前手续费率

Api用户查询交易对费率，一次限制最多查10个交易对，子用户的费率和母用户保持一致

API Key 权限：读取

```shell
curl "https://api.huobi.pro/v2/reference/transact-fee-rate?symbols=btcusdt,ethusdt,ltcusdt"
```

### HTTP 请求

- GET `/v2/reference/transact-fee-rate`

### 请求参数

| 参数    | 数据类型 | 是否必须 | 默认值 | 描述                     | 取值范围                                                |
| ------- | -------- | -------- | ------ | ------------------------ | ------------------------------------------------------- |
| symbols | string   | true     | NA     | 交易对，可多填，逗号分隔 | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`）> |

> Response:

```json
{
  "code": "200",
  "data": [
     {
        "symbol": "btcusdt",
        "makerFeeRate":"0.002",
        "takerFeeRate":"0.002",
        "actualMakerRate": "0.002",
        "actualTakerRate":"0.002
     },
     {
        "symbol": "ethusdt",
        "makerFeeRate":"0.002",
        "takerFeeRate":"0.002",
        "actualMakerRate": "0.002",
        "actualTakerRate":"0.002
    },
     {
        "symbol": "ltcusdt",
        "makerFeeRate":"0.002",
        "takerFeeRate":"0.002",
        "actualMakerRate": "0.002",
        "actualTakerRate":"0.002
    }
  ]
}
```
### 响应数据

|      | 字段名称          | 数据类型 | 描述                                                         |      |
| ---- | ----------------- | -------- | ------------------------------------------------------------ | ---- |
|      | code              | integer  | 状态码                                                       |      |
|      | message           | string   | 错误描述（如有）                                             |      |
|      | data              | object   |                                                              |      |
|      | { symbol          | string   | 交易代码                                                     |      |
|      | makerFeeRate      | string   | 基础费率 - 被动方，如适用交易手续费返佣，返回返佣费率（负值） |      |
|      | takerFeeRate      | string   | 基础费率 - 主动方                                            |      |
|      | actualMakerRate   | string   | 抵扣后费率 - 被动方，如不适用抵扣或未启用抵扣，返回基础费率；如适用交易手续费返佣，返回返佣费率（负值） |      |
|      | actualTakerRate } | string   | 抵扣后费率 – 主动方，如不适用抵扣或未启用抵扣，返回基础费率  |      |

注：<br>
- 如makerFeeRate/actualMakerRate为正值，该字段意为交易手续费率；<br>
- 如makerFeeRate/actualMakerRate为负值，该字段意为交易返佣费率。<br>

# 策略委托

## 简介

策略委托，目前仅包括计划委托及追踪委托。与现有止盈止损订单相比，计划委托/追踪委托有以下显著不同 –<br>

1）	计划委托/追踪委托被创建后，未触发前，交易所将不会冻结委托保证金。仅当计划委托成功触发后，交易所才会冻结该委托的保证金。<br>
2）	计划委托支持限价单和市价单类型，追踪委托仅支持市价单。<br>
3）	追踪委托是一种更高级的计划委托。通常的计划委托仅可设置触发价一个条件，当市场最新价格达到触发价时，该订单即被送入撮合。追踪委托在计划委托的基础上增加了一个设定条件，即回调幅度。当市场最新价达到设定的触发价时，该追踪委托并不会被送入撮合，而是继续等待市场价格回转出现。当市场价格回转幅度达到设定的回调幅度时，该追踪委托才会被送入撮合。火币Global支持用户设定的回调幅度范围为0.1%~5%。<br>

<aside class="notice">访问策略委托相关的接口需要进行签名认证。</aside>
<aside class="notice"> 在计划委托/追踪委托上线一段时间后，火币Global可能会下线现有止盈止损订单类型。届时将另行通知。 </aside>

以下是策略委托接口返回的错误码和说明。

| 错误码 | 说明                       |
| ------ | -------------------------- |
| 2002   | 参数无效                   |
| 1001   | 无效的url                  |
| 1002   | 请重新登录后重试           |
| 1003   | API签名无效                |
| 1005   | 访问权重不足               |
| 1006   | 超出访问限制               |
| 1007   | 未查询到记录               |
| 2003   | 交易功能暂停               |
| 3002   | 订单数量精度错误           |
| 3003   | 触发价格精度错误           |
| 3004   | 低于限价单最小订单数量限制 |
| 3005   | 超出限价单最大订单数量限制 |
| 3006   | 超出限价单最高订单价格限制 |
| 3007   | 低于限价单最低订单价格限制 |
| 3008   | 低于最小订单金额限制       |
| 3009   | 低于市价单最小订单数量限制 |
| 3010   | 超出市价单最大订单数量限制 |
| 3100   | 限价交易期间不接受市价申报 |

## 策略委托下单

POST /v2/algo-orders<br>
API Key 权限：交易<br>
限频值（NEW）：20次/2秒<br>
仅可通过此节点下单策略委托，不可通过现货/杠杆交易相关接口下单策略委托<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	默认值|	描述	|	取值范围	|
|	-----	|	-----	|	------	|	----	|	------	|	----	|
|	accountId	|	integer	|	TRUE	|		|	账户编号	|当前仅支持spot账户ID、margin账户ID、super-margin账户ID，暂不支持c2c-margin账户ID		|
|	symbol	|	string	|	TRUE	|		|	交易代码	|		|
|	orderPrice	|	string	|	FALSE	|		|	订单价格（对市价单无效）	|		|
|	orderSide	|	string	|	TRUE	|		|	订单方向	|	buy,sell	|
|	orderSize	|	string	|	FALSE	|		|	订单数量（对市价买单无效）	|		|
|	orderValue	|	string	|	FALSE	|		|	订单金额（仅对市价买单有效）	|		|
|	timeInForce	|	string	|	FALSE	|	gtc for orderType=limit; ioc for orderType=market	|	订单有效期	|	gtc(对orderType=market无效),boc(对orderType=market无效),ioc,fok(对orderType=market无效)	|
|	orderType	|	string	|	TRUE	|		|	订单类型	|	limit,market	|
|	clientOrderId	|	string	|	TRUE	|		|	用户自编订单号（最长64位）	|		|
|	stopPrice	|	string	|	TRUE	|		|	触发价	|		|
|	trailingRate	|	string	|	FALSE	|		|	 回调幅度（仅对追踪委托有效）	|	[0.001,0.050]	|

注：<br>
•	orderPrice与stopPrice的偏离率不能超出交易所对该币对的价格限制（百分比），例如，当交易所限定，限价买单的订单价格不能高于市价的110%时，该限制比率也同样适用于orderPrice与stopPrice之比。<br>
•	用户须保证策略委托在触发时，其clientOrderId不与该用户的其它（24小时内）订单重复，否则，会导致触发失败。<br>
•	用户须保证相关账户（accountId）中存有足够资金作为委托保证金，否则将导致策略委托触发时校验失败。<br>
•	timeInForce字段中各枚举值含义：gtc - good till cancel (除非用户主动撤销否则一直有效)，boc - book or cancel（即post only，或称book only，除非成功挂单否则自动撤销），ioc - immediate or cancel（立即成交剩余部分自动撤销），fok - fill or kill（立即全部成交否则全部自动撤销）<br>

> Response

```json
{
    "code": 200,
    "data": {
        "clientOrderId": "a001"
    }
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|	|
|	{ clientOrderId }	|	string	|	TRUE	|用户自编订单号	|

## 策略委托（触发前）撤单

POST /v2/algo-orders/cancellation<br>
API Key 权限：交易<br>
限频值（NEW）：20次/2秒<br>
单次请求最多批量撤销50张订单<br>
如需撤销已成功触发的订单，须通过现货/杠杆交易相关接口完成<br>
如需撤销未触发的订单，仅可通过此节点撤销，不可通过现货/杠杆交易相关接口撤销<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	默认值|	描述	|	取值范围	|
|	-----	|	-----	|	------	|	----	|	------	|	----	|
|	clientOrderIds	|	string[]	|	TRUE	|		|	用户自编订单号（可多填，以逗号分隔）	|		|

> Response

```json
{
    "code": 200,
    "data": {
        "accepted": [
            "a001"
        ],
        "rejected": []
    }
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|按用户请求顺序排列	|
|	{ accepted	|	string[]	|	FALSE	|已接受订单clientOrderId列表	|
|	rejected }	|	string[]	|	TRUE	|已拒绝订单clientOrderId列表	|

## 查询未触发OPEN策略委托

GET /v2/algo-orders/opening<br>
API Key 权限：读取<br>
限频值（NEW）：20次/2秒<br>
以orderOrigTime检索<br>
未触发OPEN订单，指的是已成功下单，但尚未触发，订单状态orderStatus为created的订单<br>
未触发OPEN订单，可通过此节点查询，但不可通过现货/杠杆交易相关接口查询<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	默认值|	描述	|	取值范围	|
|	-----	|	-----	|	------	|	----	|	------	|	----	|
|	accountId	|	integer	|	FALSE	|	all	|	账户编号	|		|
|	symbol	|	string	|	FALSE	|	all	|	交易代码	|		|
|	orderSide	|	string	|	FALSE	|	all	|	订单方向	|	buy,sell	|
|	orderType	|	string	|	FALSE	|	all	|	订单类型	|	limit,market	|
|	sort	|	string	|	FALSE	|	desc	|	检索方向	|asc - 由远及近, desc - 由近及远		|
|	limit	|	integer	|	FALSE	|	100	|	单页最大返回条目数量	|[1,500]		|
|	fromId	|	long	|	FALSE	|		|	起始编号（仅在下页查询时有效）	|		|

> Response

```json
{
    "code": 200,
    "data": [
        {
            "lastActTime": 1593235832976,
            "orderOrigTime": 1593235832937,
            "symbol": "btcusdt",
            "orderSize": "0.001",
            "stopPrice": "5001",
            "accountId": 5260185,
            "source": "api",
            "clientOrderId": "a001",
            "orderSide": "buy",
            "orderType": "limit",
            "timeInForce": "gtc",
            "orderPrice": "5000",
            "orderStatus": "created"
        }
    ]
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|按用户请求参数sort指定顺序排列	|
|	{ accountId	|	integer	|	TRUE	|账户编号	|
|	source	|	string	|	TRUE	|订单来源（api,web,ios,android,mac,windows,sys）	|
|	clientOrderId	|	string	|	TRUE	|用户自编订单号	|
|	symbol	|	string	|	TRUE	|交易代码	|
|	orderPrice	|	string	|	TRUE	|订单价格（对市价单无效）	|
|	orderSize	|	string	|	FALSE	|订单数量（对市价买单无效）	|
|	orderValue	|	string	|	FALSE	|订单金额（仅对市价买单有效）	|
|	orderSide	|	string	|	TRUE	|订单方向	|
|	timeInForce	|	string	|	TRUE	|订单有效期|
|	orderType	|	string	|	TRUE	|订单类型	|
|	stopPrice	|	string	|	TRUE	|触发价	|
|	trailingRate	|	string	|	FALSE	|	回调幅度（仅对追踪委托有效）	|
|	orderOrigTime	|	long	|	TRUE	|订单创建时间	|
|	lastActTime	|	long	|	TRUE	|订单最近更新时间	|
|	orderStatus }	|	string	|	TRUE	|订单状态（created）	|
|	nextId	|	long	|	FALSE	|下页起始编号（仅在查询结果需要分页返回时传此字段）	|

## 查询策略委托历史

GET /v2/algo-orders/history<br>
API Key 权限：读取<br>
限频值（NEW）：20次/2秒<br>
以orderOrigTime检索<br>
历史终态订单包括，触发前被主动撤销的策略委托（orderStatus=canceled），触发失败的策略委托（orderStatus=rejected），触发成功的策略委托（orderStatus=triggered）。<br>
如需查询已成功触发订单的后续状态，须通过现货/杠杆交易相关接口完成<br>
触发前被主动撤销的策略委托及触发失败的策略委托，可通过此节点查询，但不可通过现货/杠杆交易相关接口查询<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	默认值|	描述	|	取值范围	|
|	-----	|	-----	|	------	|	----	|	------	|	----	|
|	accountId	|	integer	|	FALSE	|	all	|	账户编号	|		|
|	symbol	|	string	|	TRUE	|		|	交易代码	|		|
|	orderSide	|	string	|	FALSE	|	all	|	订单方向	|	buy,sell	|
|	orderType	|	string	|	FALSE	|	all	|	订单类型	|	limit,market	|
|	orderStatus	|	string	|	TRUE	|		|	订单状态	|	canceled,rejected,triggered	|
|	startTime	|	long	|	FALSE	|		|	远点时间	|
|	endTime	|	long	|	FALSE	|当前时间		|	近点时间 | |
|	sort	|	string	|	FALSE	|	desc	|	检索方向	|asc - 由远及近, desc - 由近及远		|
|	limit	|	integer	|	FALSE	|	100	|	单页最大返回条目数量	|[1,500]		|
|	fromId	|	long	|	FALSE	|		|	起始编号（仅在下页查询时有效）	|		|

> Response

```json
{
    "code": 200,
    "data": [
        {
            "orderOrigTime": 1593235832937,
            "lastActTime": 1593236344401,
            "symbol": "btcusdt",
            "source": "api",
            "orderSide": "buy",
            "orderType": "limit",
            "timeInForce": "gtc",
            "clientOrderId": "a001",
            "accountId": 5260185,
            "orderPrice": "5000",
            "orderSize": "0.001",
            "stopPrice": "5001",
            "orderStatus": "canceled"
        }
    ]
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|按用户请求参数sort指定顺序排列	|
|	{ accountId	|	integer	|	TRUE	|账户编号	|
|	source	|	string	|	TRUE	|订单来源	|
|	clientOrderId	|	string	|	TRUE	|用户自编订单号	|
|	orderId	|	string	|	FALSE	|订单编号（仅对orderStatus=triggered有效）	|
|	symbol	|	string	|	TRUE	|交易代码	|
|	orderPrice	|	string	|	TRUE	|订单价格（对市价单无效）	|
|	orderSize	|	string	|	FALSE	|订单数量（对市价买单无效）	|
|	orderValue	|	string	|	FALSE	|订单金额（仅对市价买单有效）	|
|	orderSide	|	string	|	TRUE	|订单方向	|
|	timeInForce	|	string	|	TRUE	|订单有效期|
|	orderType	|	string	|	TRUE	|订单类型	|
|	stopPrice	|	string	|	TRUE	|触发价	|
|	trailingRate	|	string	|	FALSE	|	回调幅度（仅对追踪委托有效）	|
|	orderOrigTime	|	long	|	TRUE	|订单创建时间	|
|	lastActTime	|	long	|	TRUE	|订单最近更新时间	|
|	orderCreateTime	|	long	|	FALSE	|订单触发时间（仅对orderStatus=triggered有效）	|
|	orderStatus	|	string	|	TRUE	|订单状态（triggered,canceled,rejected）	|
|	errCode	|	integer	|	FALSE	|订单被拒状态码（仅对orderStatus=rejected有效）	|
|	errMessage }	|	string	|	FALSE	|订单被拒错误消息（仅对orderStatus=rejected有效）	|
|	nextId	|	long	|	FALSE	|下页起始编号（仅在查询结果需要分页返回时传此字段）	|

## 查询特定策略委托

GET /v2/algo-orders/specific<br>
API Key 权限：读取<br>
限频值（NEW）：20次/2秒<br>
以orderOrigTime检索<br>
如需查询已成功触发订单的后续状态，须通过现货/杠杆交易相关接口完成<br>
未触发的策略委托及触发失败的策略委托，可通过此节点查询，但不可通过现货/杠杆交易相关接口查询<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	默认值|	描述	|	取值范围	|
|	-----	|	-----	|	------	|	----	|	------	|	----	|
|	clientOrderId	|	string	|	TRUE	|		| 用户自编订单号|		|

> Response

```json
{
    "code": 200,
    "data": {
        "lastActTime": 1593236344401,
        "orderOrigTime": 1593235832937,
        "symbol": "btcusdt",
        "orderSize": "0.001",
        "stopPrice": "5001",
        "accountId": 5260185,
        "source": "api",
        "clientOrderId": "a001",
        "orderSide": "buy",
        "orderType": "limit",
        "timeInForce": "gtc",
        "orderPrice": "5000",
        "orderStatus": "canceled"
    }
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|	|
|	{ accountId	|	integer	|	TRUE	|账户编号	|
|	source	|	string	|	TRUE	|订单来源	|
|	clientOrderId	|	string	|	TRUE	|用户自编订单号	|
|	orderId	|	string	|	FALSE	|订单编号（仅对orderStatus=triggered有效）	|
|	symbol	|	string	|	TRUE	|交易代码	|
|	orderPrice	|	string	|	TRUE	|订单价格（对市价单无效）	|
|	orderSize	|	string	|	FALSE	|订单数量（对市价买单无效）	|
|	orderValue	|	string	|	FALSE	|订单金额（仅对市价买单有效）	|
|	orderSide	|	string	|	TRUE	|订单方向	|
|	timeInForce	|	string	|	TRUE	|订单有效期|
|	orderType	|	string	|	TRUE	|订单类型	|
|	stopPrice	|	string	|	TRUE	|触发价	|
|	trailingRate	|	string	|	FALSE	|	回调幅度（仅对追踪委托有效）	|
|	orderOrigTime	|	long	|	TRUE	|订单创建时间	|
|	lastActTime	|	long	|	TRUE	|订单最近更新时间	|
|	orderCreateTime	|	long	|	FALSE	|订单触发时间（仅对orderStatus=triggered有效）	|
|	orderStatus	|	string	|	TRUE	|订单状态（created,triggered,canceled,rejected）	|
|	errCode	|	integer	|	FALSE	|订单被拒状态码（仅对orderStatus=rejected有效）	|
|	errMessage }	|	string	|	FALSE	|订单被拒错误消息（仅对orderStatus=rejected有效）	|

# 借币（逐仓/全仓杠杆）

## 简介

逐仓杠杆/全仓杠杆接口提供了账户借币、还币、查询、划转等功能

<aside class="notice">访问借币相关的接口需要进行签名认证。</aside>
<aside class="notice">目前逐仓杠杆交易仅支持部分以 USDT，HSUD， 和 BTC 为报价币种的交易对。</aside>

以下是逐仓杠杆接口的返回码和说明。

| 返回码                                      | 说明                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| account-transfer-balance-insufficient-error | 账户余额不足                                                 |
| account-transfer-balance-overflow-error     | 负账户余额溢出                                               |
| account-transfer-balance-insufficient_error | 账户余额不足（不区分动作类型）                               |
| base-msg                                    | 自定义错误消息                                               |
| base-system-error                           | 系统异常                                                     |
| base-currency-error                         | currency不存在                                               |
| base-symbol-error                           | symbol不存在                                                 |
| base-margin-symbol-invalid                  | 非法借贷交易对(非法交易对或者被禁止借贷的交易对)             |
| base-record-invalid                         | 记录无效                                                     |
| base-request-timeout                        | 请求超时，请稍后再试                                         |
| base_request_exceed_number_limit            | 请求人数过多，请稍后再试                                     |
| base-date-limit-error                       | 日期错误                                                     |
| base-update-error                           | 更新数据错误                                                 |
| base-operation-forbidden 禁止操作           | 非计息状态 禁止还款                                          |
| dw-insufficient-balance                     | 余额不足                                                     |
| dw-account-transfer-error                   | 转账错误                                                     |
| frequent-invoke                             | 操作过于频繁，请稍后重试                                     |
| loan-order-not-found                        | 订单未找到                                                   |
| loan-amount-scale-limit                     | 借贷&还款 金额精度限制                                       |
| loan-repay-max-limit                        | 偿还大于借贷                                                 |
| loan-insufficient-balance                   | 余额不足                                                     |
| login-required                              | 需要登录                                                     |
| margin-country-not-allow                    | 国家未开放借贷                                               |
| margin-country-auth-required                | 国家未开放借贷，需要认证                                     |
| margin-trading-is-not-available             | 暂不支持逐仓杠杆交易--禁止土耳其籍或通过土耳其KYC的用户进行逐仓杠杆借币 |
| margin-account-state-error                  | 账户状态异常(爆仓中)                                         |
| risk-verification-failed                    | 风控拦截通用错误码                                           |
| sub-user-auth-required                      | 需要母用户授权子用户                                         |

以下是全仓杆接口的返回码和说明。

| 返回码                                   | 说明                                  |
| ---------------------------------------- | ------------------------------------- |
| abnormal-users-cannot-transfer           | 非正常用户不能转出                    |
| account-explosion-in-prohibited-transfer | 账户爆仓中禁止划转操作                |
| account-is-abnormal-retry-after-refresh  | 账户异常请刷新重试                    |
| account-balance-insufficient-error       | 账户余额不足，不区分动作类型          |
| account-cannot-be-inquired               | 无法查询到全仓杠杆账户                |
| base-not-in-white-list                   | 不是白名单用户                        |
| base-currency-error                      | currency不存在                        |
| base-operation-forbidden                 | 禁止操作                              |
| base-user-request-exceed-limit           | 操作太频繁，请稍后再试                |
| base-currency-not-open                   | currency还没有开放 该保证金币种未开启 |
| beyond-maximum-number-of-rollover        | 超出最大转出数量                      |
| exceed-maximum-amount                    | 超出最大数量                          |
| start-date-cannot-greater-than-end-date  | 开始时间不能大于结束时间              |
| frequent-invoke                          | 操作过于频繁，请稍后重试              |
| loan-order-not-found                     | 订单未找到                            |
| loan-amount-scale-limit                  | 借贷&还款 金额精度限制                |
| loan-repay-max-limit                     | 偿还大于借贷                          |
| loan-insufficient-balance                | 余额不足                              |
| loan-fee-rate-compute-fail               | 系统借款利率计算异常                  |
| login-required                           | 需要登录                              |
| margin-subuser-no-permission             | 全仓杠杆子账号未开通权限              |
| normal-and-warehouse-can-transfer        | 正常用户与穿仓用户可以转入            |
| order-orderamount-precision-error        | 交易数额精度错误                      |
| require-exchange-id                      | 需要交易所id                          |
| subacount-currency-not-exit              | 该币种的子账户不存在                  |
| system-busy                              | 系统繁忙                              |
| unsupport-kyc-info                       | 不支持的kyc认证信息                   |
| uc-network-error                         | 网络错误                              |
| uncreated-currency-cannot-be-drawn       | 未创建币种子账户无法划出              |

## 资产划转（逐仓）

API Key 权限：交易<br>
限频值（NEW）：2次/2s

此接口用于现货账户与逐仓杠杆账户的资产互转。

从现货账户划转至逐仓杠杆账户 `transfer-in`，从逐仓杠杆账户划转至现货账户 `transfer-out`

### HTTP 请求

- POST ` /v1/dw/transfer-in/margin`

- POST ` /v1/dw/transfer-out/margin`

> Request:

```json
{
  "symbol": "ethusdt",
  "currency": "eth",
  "amount": "1.0"
}
```


### 请求参数

| 参数名称 | 数据类型 | 是否必需 | 默认值 | 描述                         |
| -------- | -------- | -------- | ------ | ---------------------------- |
| symbol   | string   | true     | NA     | 交易对, e.g. btcusdt, ethbtc |
| currency | string   | true     | NA     | 币种                         |
| amount   | string   | true     | NA     | 划转数量                     |


> Response:

```json
{  
  "data": 1000
}
```

### 响应数据


| 参数名称 | 数据类型 | 描述        |
| -------- | -------- | ----------- |
| data     | integer  | Transfer id |

## 查询借币币息率及额度（逐仓）

API Key 权限：读取<br>
限频值（NEW）：20次/2s

此接口返回用户级别的借币币息率及借币额度。

```shell
curl "https://api.huobi.pro/v1/margin/loan-info?symbols=btcusdt"
```

### HTTP 请求

- GET ` /v1/margin/loan-info`

### 请求参数

| 参数名称 | 数据类型 | 是否必需 | 默认值 | 描述                          |
| -------- | -------- | -------- | ------ | ----------------------------- |
| symbols  | string   | false    | all    | 交易代码 (可多选，以逗号分隔) |

> Response:

```json
{
    "status": "ok",
    "data": [
        {
            "symbol": "btcusdt",
            "currencies": [
                {
                    "currency": "btc",
                    "interest-rate": "0.00098",
                    "min-loan-amt": "0.020000000000000000",
                    "max-loan-amt": "550.000000000000000000",
                    "loanable-amt": "0.045696000000000000",
                    "actual-rate": "0.00098"
                },
                {
                    "currency": "usdt",
                    "interest-rate": "0.00098",
                    "min-loan-amt": "100.000000000000000000",
                    "max-loan-amt": "4000000.000000000000000000",
                    "loanable-amt": "400.000000000000000000"
                    "actual-rate": "0.00098"
                }
            ]
        }
    ]
}
```

### 响应数据

| 参数名称       | 数据类型 | 描述                                                         |
| -------------- | -------- | ------------------------------------------------------------ |
| { symbol       | string   | 交易代码                                                     |
| currencies     | object   |                                                              |
| { currency     | string   | 币种                                                         |
| interest-rate  | string   | 基础日币息率                                                 |
| min-loan-amt   | string   | 最小允许借币金额                                             |
| max-loan-amt   | string   | 最大允许借币金额                                             |
| loanable-amt   | string   | 最大可借金额                                                 |
| actual-rate }} | string   | 抵扣后的实际借币币息率，如不适用抵扣或未启用抵扣，返回基础日币息率 |

## 申请借币（逐仓）

API Key 权限：交易<br>
限频值（NEW）：2次/2s

此接口用于申请借币.

### HTTP 请求

- POST ` /v1/margin/orders`

> Request:

```json
{
  "symbol": "ethusdt",
  "currency": "eth",
  "amount": "1.0"
}
```

### 请求参数

| 参数名称 | 数据类型 | 是否必需 | 默认值 | 描述                      |
| -------- | -------- | -------- | ------ | ------------------------- |
| symbol   | string   | true     | NA     | 交易对                    |
| currency | string   | true     | NA     | 币种                      |
| amount   | string   | true     | NA     | 借币数量（精度：3位小数） |

> Response:

```json
{
  "status": "ok",
  "data": 1000
}
```

### 响应数据

| 字段名称 | 数据类型 | 描述   |
| -------- | -------- | ------ |
| status   | string   | 状态   |
| data     | integer  | 订单id |

## 归还借币（逐仓）

API Key 权限：交易<br>
限频值（NEW）：2次/2s

此接口用于归还借币.

### HTTP 请求

- POST ` /v1/margin/orders/{order-id}/repay`

> Request:

```json
{
  "amount": "1.0"
}
```

### 请求参数

| 参数名称 | 数据类型 | 是否必需 | 描述                          |
| -------- | -------- | -------- | ----------------------------- |
| order-id | string   | true     | 借币订单 ID，写在 url path 中 |
| amount   | string   | true     | 归还币种数量                  |

> Response:

```json
{  
  "data": 1000
}
```

### 响应数据


| 参数名称 | 数据类型 | 描述            |
| -------- | -------- | --------------- |
| data     | integer  | Margin order id |


## 查询借币订单（逐仓）

API Key 权限：读取<br>
限频值（NEW）：100次/2s

此接口基于指定搜索条件返回借币订单。

### HTTP 请求

- GET ` /v1/margin/loan-orders`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                                                 | 默认值                           | 取值范围                                                     |
| ---------- | -------- | ------ | ---------------------------------------------------- | -------------------------------- | ------------------------------------------------------------ |
| symbol     | true     | string | 交易对                                               |                                  | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`）       |
| start-date | false    | string | 查询开始日期, 日期格式yyyy-mm-dd                     |                                  |                                                              |
| end-date   | false    | string | 查询结束日期, 日期格式yyyy-mm-dd                     |                                  |                                                              |
| states     | false    | string | 状态列表，可以支持多个状态，用逗号分隔               |                                  | created 未放款，accrual 已放款，cleared 已还清，invalid 异常 |
| from       | false    | string | 查询起始 ID                                          |                                  |                                                              |
| direct     | false    | string | 查询方向                                             |                                  | prev 向前，时间（或 ID）正序；next 向后，时间（或 ID）倒序） |
| size       | false    | string | 查询记录大小                                         | 100                              | [1, 100]                                                     |
| sub-uid    | false    | int    | 子用户编号（母用户查询子用户借币订单时，此字段必填） | 如不填，缺省查询当前用户借币订单 |                                                              |

> Response:

```json
{
    "status": "ok",
    "data": [
        {
            "deduct-rate": "1",
            "created-at": 1595831651478,
            "updated-at": 1595832010845,
            "accrued-at": 1595831651478,
            "interest-amount": "0.004083000000000000",
            "loan-amount": "100.000000000000000000",
            "hour-interest-rate": "0.000040830000000000",
            "loan-balance": "0.000000000000000000",
            "interest-balance": "0.000000000000000000",
            "paid-coin": "0.004083000000000000",
            "day-interest-rate": "0.000980000000000000",
            "interest-rate": "0.000040830000000000",
            "user-id": 5574974,
            "account-id": 5463409,
            "currency": "usdt",
            "symbol": "btcusdt",
            "paid-point": "0.000000000000000000",
            "deduct-currency": "",
            "deduct-amount": "0",
            "id": 7839857,
            "state": "cleared"
        }
    ]
}
```

### 响应数据


| 字段名称           | 是否必须 | 数据类型 | 描述                       | 取值范围                                                     |
| ------------------ | -------- | -------- | -------------------------- | ------------------------------------------------------------ |
| id                 | true     | long     | 订单号                     |                                                              |
| user-id            | true     | long     | 用户ID                     |                                                              |
| account-id         | true     | long     | 账户ID                     |                                                              |
| symbol             | true     | string   | 交易对                     |                                                              |
| currency           | true     | string   | 币种                       |                                                              |
| loan-amount        | true     | string   | 借币本金总额               |                                                              |
| loan-balance       | true     | string   | 未还本金                   |                                                              |
| interest-rate      | true     | string   | 币息率                     |                                                              |
| interest-amount    | true     | string   | 币息总额                   |                                                              |
| interest-balance   | true     | string   | 未还币息                   |                                                              |
| created-at         | true     | long     | 借币发起时间               |                                                              |
| accrued-at         | true     | long     | 最近一次计息时间           |                                                              |
| state              | true     | string   | 订单状态                   | created 未放款，accrual 已放款，cleared 已还清，invalid 异常 |
| paid-point         | true     | string   | 已支付点卡金额（用于还息） |                                                              |
| paid-coin          | true     | string   | 已支付原币金额（用于还息） |                                                              |
| deduct-rate        | true     | string   | 抵扣率（用于还息）         |                                                              |
| deduct-currency    | true     | string   | 抵扣币种（用于还息）       |                                                              |
| deduct-amount      | true     | string   | 抵扣金额（用于还息）       |                                                              |
| updated-at         | true     | long     | 更新时间                   |                                                              |
| hour-interest-rate | true     | string   | 时息率                     |                                                              |
| day-interest-rate  | true     | string   | 日息率                     |                                                              |

## 借币账户详情（逐仓）

API Key 权限：读取<br>
限频值（NEW）：100次/2s

此接口返回借币账户详情。

```shell
curl "https://api.huobi.pro/v1/margin/accounts/balance?symbol=btcusdt"
```

### HTTP 请求

- GET `/v1/margin/accounts/balance`

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述                                                         | 默认值                           | 取值范围 |
| -------- | -------- | ------ | ------------------------------------------------------------ | -------------------------------- | -------- |
| symbol   | false    | string | 交易对，作为get参数<br />如果不传则不返回可转余额(transfer-out-available)和可借余额(loan-available) |                                  |          |
| sub-uid  | false    | int    | 子用户编号（母用户查询子用户借币详情时，此字段必填）         | 如不填，缺省查询当前用户借币详情 |          |

> Response:

```json
{  
  "data": [
    {
      "id": 18264,
      "type": "margin",
      "state": "working",
      "symbol": "btcusdt",
      "fl-price": "0",
      "fl-type": "safe",
      "risk-rate": "475.952571086994250554",
      "list": [
          {
              "currency": "btc",
              "type": "trade",
              "balance": "1168.533000000000000000"
          },
          {
              "currency": "btc",
              "type": "frozen",
              "balance": "0.000000000000000000"
          },
          {
              "currency": "btc",
              "type": "loan",
              "balance": "-2.433000000000000000"
          },
          {
              "currency": "btc",
              "type": "interest",
              "balance": "-0.000533000000000000"
          },
          {
              "currency": "btc",
              "type": "transfer-out-available",//可转btc,只有传入symbol才会返回
              "balance": "1163.872174670000000000"
          },
          {
              "currency": "btc",
              "type": "loan-available",//可借btc,只有传入symbol才会返回
              "balance": "8161.876538350676000000"
          }
      ]
    }
  ]
}
```

### 响应数据

| 字段名称   | 是否必须 | 数据类型 | 描述                   | 取值范围                                                     |
| ---------- | -------- | -------- | ---------------------- | ------------------------------------------------------------ |
| symbol     | true     | string   | 交易对                 |                                                              |
| state      | true     | string   | 账户状态               | working 正常,fl-sys 系统自动爆仓,fl-mgt 手动爆仓,fl-end 爆仓结束 |
| risk-rate  | true     | string   | 风险率                 |                                                              |
| fl-price   | true     | string   | 爆仓价                 |                                                              |
| list       | true     | array    | 借币账户详情列表       |                                                              |
| { currency | true     | string   | 币种                   |                                                              |
| type       | true     | string   | 类型                   | type: 交易余额, frozen: 冻结余额, loan: 待还借贷本金, interest: 待还借贷利息 |
| balance }  | true     | string   | 余额，负数表示应还金额 |                                                              |

## 资产划转（全仓）

API Key 权限：交易

此接口用于现货账户与全仓杠杆账户的资产互转。

从现货账户划转至全仓杠杆账户 `transfer-in`，从全仓杠杆账户划转至现货账户 `transfer-out`

### HTTP 请求

- POST ` /v1/cross-margin/transfer-in`
- POST ` /v1/cross-margin/transfer-out`

> Request:

```json
{
  "currency": "eth",
  "amount": "1.0"
}
```

### 请求参数

| 参数名称 | 数据类型 | 是否必需 | 默认值 | 描述     |
| -------- | -------- | -------- | ------ | -------- |
| currency | string   | true     | NA     | 币种     |
| amount   | string   | true     | NA     | 划转数量 |


> Response:

```json
{  
  "status": "ok",
  "data": 1000
}
```

### 响应数据


| 参数名称 | 数据类型 | 描述        |
| -------- | -------- | ----------- |
| data     | integer  | Transfer id |

## 查询借币币息率及额度（全仓）

API Key 权限：读取

此接口返回用户级别的借币币息率及借币额度。

### HTTP 请求

- GET ` /v1/cross-margin/loan-info`

### 请求参数

无

> Response:

```json
{
    "status": "ok",
    "data": [
        {
            "currency": "bch",
            "interest-rate": "0.00098",
            "min-loan-amt": "0.35",
            "max-loan-amt": "3500",
            "loanable-amt": "0.70405181",
            "actual-rate": "0.000343"
        },
        {
            "currency": "btc",
            "interest-rate": "0.00098",
            "min-loan-amt": "0.01",
            "max-loan-amt": "100",
            "loanable-amt": "0.02281914",
            "actual-rate": "0.000343"
        },
        {
            "currency": "eos",
            "interest-rate": "0.00098",
            "min-loan-amt": "30",
            "max-loan-amt": "300000",
            "loanable-amt": "57.69175296",
            "actual-rate": "0.000343"
        },
        {
            "currency": "eth",
            "interest-rate": "0.00098",
            "min-loan-amt": "0.5",
            "max-loan-amt": "6000",
            "loanable-amt": "1.06712197",
            "actual-rate": "0.000343"
        },
        {
            "currency": "ltc",
            "interest-rate": "0.00098",
            "min-loan-amt": "1.5",
            "max-loan-amt": "15000",
            "loanable-amt": "3.28947368",
            "actual-rate": "0.000343"
        },
        {
            "currency": "usdt",
            "interest-rate": "0.00098",
            "min-loan-amt": "100",
            "max-loan-amt": "1500000",
            "loanable-amt": "200.00000000",
            "actual-rate": "0.000343"
        },
        {
            "currency": "xrp",
            "interest-rate": "0.00098",
            "min-loan-amt": "380",
            "max-loan-amt": "4000000",
            "loanable-amt": "734.21439060",
            "actual-rate": "0.000343"
        }
    ]
}
```

### 响应数据

| 参数名称      | 数据类型 | 描述                                                         |
| ------------- | -------- | ------------------------------------------------------------ |
| { currency    | string   | 币种                                                         |
| interest-rate | string   | 基础日币息率                                                 |
| min-loan-amt  | string   | 最小允许借币金额                                             |
| max-loan-amt  | string   | 最大允许借币金额                                             |
| loanable-amt  | string   | 最大可借金额                                                 |
| actual-rate } | string   | 抵扣后的实际币息率，如不适用抵扣或未启用抵扣则返回基础日币息率 |

## 申请借币（全仓）

API Key 权限：交易

此接口用于申请借币.

### HTTP 请求

- POST ` /v1/cross-margin/orders`

> Request:

```json
{
  "currency": "eth",
  "amount": "1.0"
}
```

### 请求参数

| 参数名称 | 数据类型 | 是否必需 | 默认值 | 描述                      |
| -------- | -------- | -------- | ------ | ------------------------- |
| currency | string   | true     | NA     | 币种                      |
| amount   | string   | true     | NA     | 借币数量（精度：3位小数） |

> Response:

```json
{  
  "status": "ok",
  "data": 1000
}
```

### 响应数据

| 字段名称 | 数据类型 | 描述            |
| -------- | -------- | --------------- |
| data     | integer  | Margin order id |

## 归还借币（全仓）

API Key 权限：交易

此接口用于归还借币.

### HTTP 请求

- POST ` /v1/cross-margin/orders/{order-id}/repay`

> Request:

```json
{
  "amount": "1.0"
}
```

### 请求参数

| 参数名称 | 数据类型 | 是否必需 | 描述                          |
| -------- | -------- | -------- | ----------------------------- |
| order-id | string   | true     | 借币订单 ID，写在 url path 中 |
| amount   | string   | true     | 归还币种数量                  |

> Response:

```json
{  
  "status": "ok",
  "data": null
}
```

### 响应数据

| 参数名称 | 数据类型 | 描述 |
| -------- | -------- | ---- |
| data     | null     | -    |

## 查询借币订单（全仓）

API Key 权限：读取

此接口基于指定搜索条件返回借币订单。

### HTTP 请求

- GET ` /v1/cross-margin/loan-orders`

### 请求参数

| 参数名称   | 是否必须 | 类型   | 描述                             | 默认值 | 取值范围 |
| ---------- | -------- | ------ | -------------------------------- | ------ | -------- |
| start-date | false    | string | 查询开始日期, 日期格式yyyy-mm-dd |        |          |
| end-date   | false    | string | 查询结束日期, 日期格式yyyy-mm-dd |        |          |
| currency   | false    | string | 币种                             |        |          |
| state | false | string | 状态   |all   |created 未放款，accrual 已放款，cleared 已还清，invalid 异常
| from   | false | string | 查询起始 ID  | 0   |     |
| direct | false | string | 查询方向     |    | prev 向前，时间（或 ID）正序；next 向后，时间（或 ID）倒序） |
| size   | false | string | 查询记录大小  |  10  |[10,100]     |
|sub-uid|false|long|子用户UID|如不填，缺省查询当前用户借贷订单||

> Response:

```json
{  
  "status": "ok",
  "data": [
    {
      "loan-balance": "0.100000000000000000",
      "interest-balance": "0.000200000000000000",
      "loan-amount": "0.100000000000000000",
      "accrued-at": 1511169724531,
      "interest-amount": "0.000200000000000000",
      "filled-points" : "0.2",
      "filled-ht" : "0.2",
      "currency": "btc",
      "id": 394,
      "state": "accrual",
      "account-id": 17747,
      "user-id": 119913,
      "created-at": 1511169724531
    }
  ]
}
```

### 响应数据

| 字段名称         | 是否必须 | 数据类型 | 描述             | 取值范围                                                     |
| ---------------- | -------- | -------- | ---------------- | ------------------------------------------------------------ |
| id               | true     | long     | 订单号           |                                                              |
| user-id          | true     | long     | 用户ID           |                                                              |
| account-id       | true     | long     | 账户ID           |                                                              |
| currency         | true     | string   | 币种             |                                                              |
| loan-amount      | true     | string   | 借币本金总额     |                                                              |
| loan-balance     | true     | string   | 未还本金         |                                                              |
| interest-amount  | true     | string   | 币息总额         |                                                              |
| interest-balance | true     | string   | 未还币息         |                                                              |
| filled-points    | true     | string   | 点卡抵扣数量     |                                                              |
| filled-ht        | true     | string   | HT抵扣数量       |                                                              |
| created-at       | true     | long     | 借币发起时间     |                                                              |
| accrued-at       | true     | long     | 最近一次计息时间 |                                                              |
| state            | true     | string   | 订单状态         | created 未放款，accrual 已放款，cleared 已还清，invalid 异常 |

## 借币账户详情（全仓）

API Key 权限：读取

此接口返回借币账户详情。

### HTTP 请求

- GET `/v1/cross-margin/accounts/balance`

### 请求参数

| 参数名称 | 是否必须 | 类型 | 描述      | 默认值                           | 取值范围 |
| -------- | -------- | ---- | --------- | -------------------------------- | -------- |
| sub-uid  | false    | long | 子用户UID | 如不填，缺省查询当前用户借贷订单 |          |

> Response:

```json
{  
  "status": "ok",
  "data": 
    {
      "id": 18264,
      "type": "cross-margin",
      "state": "working",
      "risk-rate": "1000",
      "acct-balance-sum": "12312.123123",
      "debt-balance-sum": "1231.2123123",
      "list": [
          {
              "currency": "btc",
              "type": "trade",
              "balance": "1168.533000000000000000"
          },
          {
              "currency": "btc",
              "type": "frozen",
              "balance": "0.000000000000000000"
          },
          {
              "currency": "btc",
              "type": "loan",
              "balance": "-2.433000000000000000"
          },
          {
              "currency": "btc",
              "type": "interest",
              "balance": "-0.000533000000000000"
          },
          {
              "currency": "btc",
              "type": "transfer-out-available",//可转btc
              "balance": "1163.872174670000000000"
          },
          {
              "currency": "btc",
              "type": "loan-available",//可借btc
              "balance": "8161.876538350676000000"
          }
      ]
    }
}
```

### 响应数据

| 字段名称         | 是否必须 | 数据类型 | 描述                                                         | 取值范围                                                     |
| ---------------- | -------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id               | true     | integer  | Account ID 账户编号                                          |                                                              |
| type             | true     | integer  | 账户类型 (margin or cross-margin)                            | cross-margin                                                 |
| state            | true     | string   | 账户状态                                                     | working 正常,fl-sys 系统自动爆仓,fl-end 爆仓结束,fl-negative 穿仓 |
| risk-rate        | true     | string   | 风险率                                                       |                                                              |
| acct-balance-sum | true     | string   | 总持有usdt折合                                               |                                                              |
| debt-balance-sum | true     | string   | 总负债usdt折合                                               |                                                              |
| list             | true     | array    | 借币账户详情列表                                             |                                                              |
| { currency       | true     | string   | 币种                                                         |                                                              |
| type             | true     | string   | 账户类型                                                     | trade,frozen,loan,interest,transfer-out-available,loan-available |
| balance }        | true     | string   | 余额（注：当type= transfer-out-available时，如果balance=-1，意味着该币种余额可全部转出） |                                                              |

## 归还借币（全仓）

API Key 权限：交易

限频值：2次/秒

子用户可以调用

还币顺序为，（如不指定transactId）先借先还，利息先还。

### HTTP 请求

- POST /v2/account/repayment

> Request:

```json
{
    "accountid": "1266826",
    "currency": "btc",
    "amount": "0.00800334",
    "transactId": "437"
}
```

### 请求参数

| **名称**   | **类型** | **是否必需** | **描述**       |
| ---------- | -------- | ------------ | -------------- |
| accountId  | string   | TRUE         | 还币账户ID     |
| currency   | string   | TRUE         | 还币币种       |
| amount     | string   | TRUE         | 还币金额       |
| transactId | string   | FALSE        | 原始借币交易ID |

> Response:

```json
{
  "code":200,
  "Data": [
      {
          "repayId":1174424,
          "repayTime":1600747722018
      }
   ]
}
```

### 响应数据

| **名称**     | **类型** | **是否必需** | **描述**                                 |
| ------------ | -------- | ------------ | ---------------------------------------- |
| code         | integer  | TRUE         | 状态码                                   |
| message      | string   | FALSE        | 错误描述（如有）                         |
| data         | array    | TRUE         |                                          |
| [{ repayId   | string   | TRUE         | 还币交易ID                               |
| repayTime }] | long     | TRUE         | 还币交易时间（unix time in millisecond） |

注：
返回relayId不意味着该还币100%成功，用户须在还币后通过查询还币交易记录确认该还币状态。

## 还币交易记录查询（全仓）

API Key 权限：读取

限频值：2次/秒

子用户可以调用

按repayTime检索

### HTTP 请求

- GET /v2/account/repayment

### 请求参数

| **名称**  | **类型** | **是否必需** | **描述**                                                     |
| --------- | -------- | ------------ | ------------------------------------------------------------ |
| repayId   | string   | FALSE        | 还币交易ID                                                   |
| accountId | string   | FALSE        | 账户ID（缺省值：所有账户）                                   |
| currency  | string   | FALSE        | 借入/借出币种（缺省值：所有币种）                            |
| startTime | long     | FALSE        | 远点时间（unix time in millisecond；取值范围：[(endTime - x天), endTime]；缺省值：(endTime - x天)） |
| endTime   | long     | FALSE        | 近点时间（unix time in millisecond；取值范围：[(当前时间 - y天), 当前时间]；缺省值：当前时间） |
| sort      | string   | FALSE        | 检索方向（有效值：asc 由远及近, desc 由近及远；缺省值：desc） |
| limit     | integer  | FALSE        | 单页最大返回条目数量（取值范围：[1,100]；缺省值：50）        |
| fromId    | long     | FALSE        | 查询起始编号（仅对翻页查询有效）                             |

> Response:

```json
{
     "code":200,
     "data":[
         {
             "repayId": 1174413,
             "repayTime":1600747389111,
             "accountId": 1266826,
             "currency":"btc",
             "repaidAmount": "0.00200083",
             "transactIds": 
                  {
                      "transactId":502,
                      "repaidprincipal": "0.00199666",
                      "repaidInterest": "0.00000417",
                      "paidHt": "0",
                      "paidPoint": "0"
                  }
            }
     ]
}
```
### 响应数据
| **名称**        | **类型** | **是否必需** | **描述**                                                 |
| --------------- | -------- | ------------ | -------------------------------------------------------- |
| code            | integer  | TRUE         | 状态码                                                   |
| message         | string   | FALSE        | 错误描述（如有）                                         |
| data            | array    | TRUE         | 按sort指定顺序排列                                       |
| [{ repayId      | string   | TRUE         | 还币交易ID                                               |
| repayTime       | long     | TRUE         | 还币交易时间（unix time in millisecond）                 |
| accountId       | string   | TRUE         | 还币账户ID                                               |
| currency        | string   | TRUE         | 还币币种                                                 |
| repaidAmount    | string   | TRUE         | 已还币金额                                               |
| transactIds     | object   | TRUE         | 该笔还币所涉及的原始借币交易ID列表（按还币优先顺序排列） |
| { transactId    | long     | TRUE         | 原始借币交易ID                                           |
| repaidPrincipal | string   | TRUE         | 该笔还币交易已还本金                                     |
| repaidInterest  | string   | TRUE         | 该笔还币交易已还利息                                     |
| paidHt          | string   | TRUE         | 该笔还币交易已支付HT金额                                 |
| paidPoint }}]   | string   | TRUE         | 该笔还币交易已支付点卡金额                               |
| nextId          | long     | FALSE        | 下页查询起始编号（仅在存在下页数据时返回）               |

# 借币（C2C）

## 简介

C2C借币相关接口提供了用户对用户之间的借入、借出、还币、查询、划转等功能。

<aside class="notice">访问交易相关的接口需要进行签名认证。</aside>

以下C2C借币相关接口统一限频值为2次/秒。<br>
子用户不可调用以下C2C借币相关接口。<br>
借入账户ID（accountId）须在web页面完成第一次划转后方可生成。<br>

以下是C2C借币相关接口的错误码、错误消息和说明。

| 错误码 | 错误消息                                                     | 说明                                               |
| ------ | ------------------------------------------------------------ | -------------------------------------------------- |
| 40301  | Insufficient available balance                               | 可用余额不足                                       |
| 40302  | Failed to get the account                                    | 获取账户信息失败                                   |
| 40307  | Existence of an ongoing loan order                           | 存在正在进行中的借贷单                             |
| 40309  | Wrong order status                                           | 订单状态错误                                       |
| 40310  | Order does not exist                                         | 借贷单不存在                                       |
| 40311  | User has OTC loans                                           | 用户存在场外借贷                                   |
| 40312  | Only normal and bankrupt users can be included               | 爆仓中账户不能转入资产                             |
| 40315  | There is no liquidation or forced liquidation setting        | 缺少强平或爆仓设置                                 |
| 40317  | Failed to get sub-loan order                                 | 获取子借贷单失败                                   |
| 40319  | No less than the minimum borrowing amount                    | 不能低于最小借出量                                 |
| 40320  | borrowing configuration does not exist                       | 借贷配置不存在                                     |
| 40322  | The user has not passed advanced verification                | 用户未通过高级认证                                 |
| 40324  | The amount of repayment exceeds the amount borrowed          | 还款数量超过借贷量                                 |
| 40326  | White list users only                                        | 非白名单用户                                       |
| 40327  | Exceeding the maximum accuracy                               | 超过最大精度                                       |
| 40328  | Cannot exceed the maximum amount of borrowing                | 不能超过最大借贷量                                 |
| 40329  | Interest rate out of the set range                           | 利率超出设定范围                                   |
| 40330  | Cannot be less than the minimum loan amount                  | 不能低于最小借入量                                 |
| 40331  | cannot exceed the maximum loan amount                        | 不能超过最大借入量                                 |
| 40332  | Cannot be less than the minimum repayment amount             | 不能低于最小还款量                                 |
| 40333  | the ending time must be greater than the starting time       | 结束时间必须大于开始时间                           |
| 40335  | in repayment                                                 | 还款中                                             |
| 40336  | This feature is not open to users in China, the United States, Turkey, Japan, Singapore | 该功能不对中国、美国、土耳其、日本、新加坡用户开放 |
| 40337  | C2C lending transaction is not currently available           | 暂不支持C2C借贷交易                                |
| 40339  | Debit and credit function is closed                          | 借贷功能已关闭                                     |
| 40340  | The current account ID does not belong to the current user   | 当前账户ID不属于当前用户所持有                     |
| 40345  | This account is not a C2C account                            | 该账户非C2C账户                                    |
| 40346  | This order is not allowed to change renew state              | 当前订单不能修改续借状态                           |

## 借入借出下单

POST /v2/c2c/offer<br>
API Key 权限：交易<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	accountId	|	string	|	FALSE	|	借入账户ID（仅对借入订单有效）	|
|	currency	|	string	|	TRUE	|	借入/借出币种	|
|	side	|	string	|	TRUE	|	订单方向（lend, borrow）	|
|	timeInForce	|	string	|	FALSE	|	订单有效期（gtc, ioc）	|
|	amount	|	string	|	TRUE	|	订单金额	|
|	interestRate	|	string	|	TRUE	|	日息率	|
|	loanTerm	|	integer	|	TRUE	|	借币期限（单位：天；有效值：10, 20, 30）	|

注：<br>
•	当前借出订单缺省有效期为gtc，借入订单缺省有效期为ioc。如用户设定timeInForce为非缺省值，返回错误信息。<br>

> Response

```json
{
    "data": {
        "offerId": 14743
        "createTime": 1593172709875
    },
    "code": 200,
    "success": true
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|	状态码	|
|	message	|	string	|	FALSE	|	错误描述（如有）	|
|	data	|	object	|	TRUE	|		|
|	{ offerId	|	string	|	TRUE	|	订单ID	|
|	createTime }	|	long	|	TRUE	|	订单创建时间（unix time in millisecond）	|

## 借入借出撤单

POST /v2/c2c/cancellation<br>
API Key 权限：交易<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	offerId	|	string	|	TRUE	|	订单ID	|

> Response

```json
{
    "data": {
        "rejected": [
            {
                "offerId": 14411,
                "errCode": 40310,
                "errMessage": "order-non-existent(NT)"
            }
        ]
    },
    "code": 200,
    "success": true
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|	状态码	|
|	message	|	string	|	FALSE	|	错误描述（如有）	|
|	data	|	object	|	TRUE	|		|
|	{ accepted	|	object	|	TRUE	|	已接受订单ID列表	|
|	[ offerId ]	|	string	|	FALSE	|	订单ID	|
|	rejected	|	object	|	TRUE	|	已拒绝订单ID列表	|
|	[ offerId	|	string	|	FALSE	|	订单ID	|
|	errCode	|	integer	|	FALSE	|	撤单被拒错误码	|
|	errMessage ]}	|	string	|	FALSE	|	撤单被拒错误消息	|

注：<br>
•	撤单请求被接受（accepted）不意味着撤单成功。用户须在撤单后主动查询该订单以确认撤单状态。<br>

## 撤销所有借入借出订单

POST /v2/c2c/cancel-all<br>
API Key 权限：交易<br>
每次最多撤销500张订单（以offerId降序逐一撤销）<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	accountId	|	string	|	FALSE	|	账户ID（缺省值：所有账户）	|
|	currency	|	string	|	FALSE	|	借入/借出币种（缺省值：所有适用C2C的币种）	|
|	side	|	string	|	FALSE	|	订单方向（有效值：lend, borrow；缺省值：所有方向）	|

> Response

```json
{
    "data": {
        "accepted": [
        {
        "offerId": "14742"
        }
     ]
   },  
    "code": 200,
    "success": true
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|	状态码	|
|	message	|	string	|	FALSE	|	错误描述（如有）	|
|	data	|	object	|	TRUE	|		|
|	{ accepted	|	object	|	TRUE	|	已接受订单ID列表	|
|	[ offerId ]	|	string	|	FALSE	|	订单ID	|
|	rejected	|	object	|	TRUE	|	已拒绝订单ID列表	|
|	[ offerId	|	string	|	FALSE	|	订单ID	|
|	errCode	|	integer	|	FALSE	|	撤单被拒错误码	|
|	errMessage ]}	|	string	|	FALSE	|	撤单被拒错误消息	|

注：<br>
•	撤单请求被接受（accepted）不意味着撤单成功。用户须在撤单后主动查询该订单以确认撤单状态。<br>

## 查询借入借出订单

GET /v2/c2c/offers<br>
API Key 权限：读取<br>
按createTime检索<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	accountId	|	string	|	FALSE	|	账户ID（缺省值：所有账户）	|
|	currency	|	string	|	FALSE	|	借入/借出币种（缺省值：所有适用C2C的币种）	|
|	side	|	string	|	FALSE	|	订单方向（有效值：lend, borrow；缺省值：所有方向）	|
|	offerStatus	|	string	|	TRUE	|	订单状态（有效值：submitted, filled, partial-filled, canceled, partial-canceled；可多填，以逗号分隔）	|
|	startTime	|	long	|	FALSE	|	远点时间（unix time in millisecond）	|
|	endTime	|	long	|	FALSE	|	近点时间（unix time in millisecond）	|
|	limit	|	integer	|	FALSE	|	单页最大返回条目数量（取值范围：[1,100]；缺省值：50）	|
|	fromId	|	long	|	FALSE	|	查询起始编号（仅对翻页查询有效）	|

> Response

```json
{
    "code": 200,
    "data": [
        {
            "offerId": "14736",
            "createTime": 1593175645809,
            "lastActTime": 1593176383232,
            "offerStatus": "filled",
            "accountId": "13699363",
            "currency": "usdt",
            "side": "borrow",
            "timeInForce": "ioc",
            "origAmount": "10",
            "amount": "0",
            "interestRate": "0.0002",
            "loanTerm": 20
        },
        {
            "offerId": "14732",
            "createTime": 1593173423885,
            "lastActTime": 1593174884411,
            "offerStatus": "filled",
            "accountId": "13699363",
            "currency": "usdt",
            "side": "borrow",
            "timeInForce": "ioc",
            "origAmount": "10",
            "amount": "0",
            "interestRate": "0.000192",
            "loanTerm": 10
        }
    ]
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|	状态码	|
|	message	|	string	|	FALSE	|	错误描述（如有）	|
|	data	|	object	|	TRUE	|	按createTime倒序排列	|
|	{ offerId	|	string	|	TRUE	|	订单ID	|
|	createTime	|	long	|	TRUE	|	订单创建时间（unix time in millisecond）	|
|	lastActTime	|	long	|	TRUE	|	订单更新时间（unix time in millisecond）	|
|	offerStatus	|	string	|	TRUE	|	订单状态（有效值：submitted, filled, partial-filled, canceled, partial-canceled）	|
|	accountId	|	string	|	TRUE	|	账户ID	|
|	currency	|	string	|	TRUE	|	借入/借出币种	|
|	side	|	string	|	TRUE	|	订单方向（有效值：lend, borrow）	|
|	timeInForce	|	string	|	TRUE	|	订单有效期（gtc, ioc）	|
|	origAmount	|	string	|	TRUE	|	订单原始金额	|
|	amount	|	string	|	TRUE	|	订单剩余金额	|
|	interestRate	|	string	|	TRUE	|	日息率	|
|	loanTerm }	|	integer	|	TRUE	|	借币期限	|
|	nextId	|	long	|	FALSE	|	下页查询起始编号（仅在存在下页数据时返回）	|

## 查询特定借入借出订单及其交易记录

GET /v2/c2c/offer<br>
API Key 权限：读取<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	offerId	|	string	|	TRUE	|	订单ID	|

> Response

```json
{
    "code": 200,
    "data": {
        "lastActTime": 1593176383232,
        "offerStatus": "filled",
        "origAmount": "10",
        "currency": "usdt",
        "amount": "0",
        "timeInForce": "ioc",
        "side": "borrow",
        "offerId": "14736",
        "accountId": "13699363",
        "interestRate": "0.0002",
        "loanTerm": 20,
        "transactions": [
            {
                "transactRate": "0.00019",
                "transactAmount": "10",
                "transactTime": 1593175646232,
                "transactId": 28152,
                "aggressor": true,
                "unpaidPrincipal": "0",
                "unpaidInterest": "0",
                "paidInterest": "0.00007917",
                "transactStatus": "closed"
            }
        ],
        "createTime": 1593175645809
    }
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|	状态码	|
|	message	|	string	|	FALSE	|	错误描述（如有）	|
|	data	|	object	|	TRUE	|	按市场板块正序排列	|
|	{ offerId	|	string	|	TRUE	|	订单ID	|
|	createTime	|	long	|	TRUE	|	订单创建时间（unix time in millisecond）	|
|	lastActTime	|	long	|	TRUE	|	订单更新时间（unix time in millisecond）	|
|	offerStatus	|	string	|	TRUE	|	订单状态（有效值：submitted, filled, partial-filled, canceled, partial-canceled）	|
|	accountId	|	string	|	TRUE	|	账户ID	|
|	currency	|	string	|	TRUE	|	借入/借出币种	|
|	side	|	string	|	TRUE	|	订单方向（有效值：lend, borrow）	|
|	timeInForce	|	string	|	TRUE	|	订单有效期（gtc, ioc）	|
|	origAmount	|	string	|	TRUE	|	订单原始金额	|
|	amount	|	string	|	TRUE	|	订单剩余金额	|
|	interestRate	|	string	|	TRUE	|	日息率	|
|	loanTerm	|	integer	|	TRUE	|	借币期限	|
|	transactions	|	object	|	TRUE	|	按transactTime倒序排列	|
|	{ transactRate	|	string	|	TRUE	|	交易价格（即达成交易的日息率）	|
|	transactAmount	|	string	|	TRUE	|	交易金额	|
|	transactTime	|	long	|	TRUE	|	交易时间（unix time in millisecond）	|
|	transactId	|	long	|	TRUE	|	交易ID	|
|	aggressor	|	boolean	|	TRUE	|	是否交易主动方（有效值：true, false）	|
|	unpaidPrincipal	|	string	|	TRUE	|	未还本金	|
|	unpaidInterest	|	string	|	TRUE	|	未还币息（截至查询时间）	|
|	paidInterest	|	string	|	TRUE	|	已还币息	|
|	transactStatus }}	|	string	|	TRUE	|	还币状态（有效值：pending, closed）	|

## 查询借入借出交易记录

GET /v2/c2c/transactions<br>
API Key 权限：读取<br>
按transactTime检索<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	accountId	|	string	|	FALSE	|	账户ID（缺省值：所有账户）	|
|	currency	|	string	|	FALSE	|	借入/借出币种（缺省值：所有币种）	|
|	side	|	string	|	FALSE	|	订单方向（有效值：lend, borrow；缺省值：所有方向）	|
|	transactStatus	|	string	|	TRUE	|	还币状态（有效值：pending, closed）	|
|	startTime	|	long	|	FALSE	|	远点时间（unix time in millisecond）	|
|	endTime	|	long	|	FALSE	|	近点时间（unix time in millisecond）	|
|	limit	|	integer	|	FALSE	|	单页最大返回条目数量（取值范围：[1,100]；缺省值：50）	|
|	fromId	|	long	|	FALSE	|	查询起始编号（仅对翻页查询有效）	|

> Response

```json
{
    "data": [
    {
        "transactId": 5585,
        "transactTime": "1593178102345",
        "transactRate": "0.0019",
        "transactAmount": "10",
        "aggressor": "true",
        "unpaidPrincipal": "0",
        "unpaidInterest": "0",
        "piadInterest": "0.00007917",
        "transactStatus": "closed",
        "offerId": "14736",
        "accountId" "13699363",
        "currency": "usdt",
        "side": "borrow"
    }
    ],
    "code": 200,
    "success": true
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|	状态码	|
|	message	|	string	|	FALSE	|	错误描述（如有）	|
|	data	|	object	|	TRUE	|	按sort指定顺序排列	|
|	{ transactRate	|	string	|	TRUE	|	交易价格（即达成交易的日息率）		|
|	transactAmount	|	string	|	TRUE	|	交易金额	|
|	transactTime	|	long	|	TRUE	|	交易时间（unix time in millisecond）	|
|	transactId	|	long	|	TRUE	|	交易ID	|
|	aggressor	|	boolean	|	TRUE	|	是否交易主动方（有效值：true, false）	|
|	unpaidPrincipal	|	string	|	TRUE	|	未还本金	|
|	unpaidInterest	|	string	|	TRUE	|	未还币息（截至查询时间）	|
|	paidInterest	|	string	|	TRUE	|	已还币息	|
|	transactStatus	|	string	|	TRUE	|	还币状态（有效值：pending, closed）	|
|	offerId	|	string	|	TRUE	|	订单ID	|
|	accountId	|	string	|	TRUE	|	账户ID	|
|	currency	|	string	|	TRUE	|	借入/借出币种	|
|	side }	|	string	|	TRUE	|	订单方向（有效值：lend, borrow）	|
|	nextId	|	long	|	FALSE	|	下页查询起始编号（仅在存在下页数据时返回）	|

## 还币
POST /v2/c2c/repayment<br>
API Key 权限：交易<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	accountId	|	string	|	TRUE	|	还币账户ID	|
|	currency	|	string	|	TRUE	|	还币币种	|
|	amount	|	string	|	TRUE	|	还币金额	|
|	offerId	|	string	|	TRUE	|	原始借入订单ID	|

> Response

```json
{
    "data": {
        "repayId": 5585,
        "repayTime": "1593178102345"
    },
    "code": 200,
    "success": true
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|	状态码	|
|	message	|	string	|	FALSE	|	错误描述（如有）	|
|	data	|	object	|	TRUE	|		|
|	{ repayId	|	string	|	TRUE	|	还币交易ID	|
|	repayTime }	|	long	|	TRUE	|	还币交易时间（unix time in millisecond）	|

注：<br>
•	返回relayId不意味着该还币100%成功，用户须在还币后通过查询还币交易记录确认该还币状态。<br>

## 查询还币交易记录
GET /v2/c2c/repayment<br>
API Key 权限：读取<br>
按repayTime检索<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	repayId	|	string	|	FALSE	|	还币交易ID	|
|	accountId	|	string	|	FALSE	|	账户ID（缺省值：所有账户）	|
|	currency	|	string	|	FALSE	|	借入/借出币种（缺省值：所有币种）	|
|	startTime	|	long	|	FALSE	|	远点时间（unix time in millisecond）	|
|	endTime	|	long	|	FALSE	|	近点时间（unix time in millisecond）	|
|	limit	|	integer	|	FALSE	|	单页最大返回条目数量（取值范围：[1,100]；缺省值：50）	|
|	fromId	|	long	|	FALSE	|	查询起始编号（仅对翻页查询有效）	|

> Response

```json
{
    "code": 200,
    "data": [
        {
            "repayId": 2173,
            "repayTime": 1593176382960,
            "accountId": 13699363,
            "currency": "usdt",
            "paidAmount": "10.00007917",
            "transactIds": [
                {
                    "transactId": 28152,
                    "paidPrincipal": "10",
                    "paidInterest": "0.00007917"
                }
            ]
        },
        {
            "repayId": 2171,
            "repayTime": 1593174883839,
            "accountId": 13699363,
            "currency": "usdt",
            "paidAmount": "10.00007",
            "transactIds": [
                {
                    "transactId": 28145,
                    "paidPrincipal": "10",
                    "paidInterest": "0.00007"
                }
            ]
        }
    ]
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|	状态码	|
|	message	|	string	|	FALSE	|	错误描述（如有）	|
|	data	|	object	|	TRUE	|	按repayTime倒序排列	|
|	{ repayId	|	string	|	TRUE	|	还币交易ID	|
|	repayTime	|	long	|	TRUE	|	还币交易时间（unix time in millisecond）	|
|	accountId	|	string	|	TRUE	|	还币账户ID	|
|	currency	|	string	|	TRUE	|	还币币种	|
|	paidAmount	|	string	|	TRUE	|	已还币金额	|
|	transactIds	|	object	|	TRUE	|	还币交易ID列表（按还币优先顺序排列）	|
|	{ transactId	|	long	|	TRUE	|	交易ID	|
|	paidPrincipal	|	string	|	TRUE	|	单笔还币交易已还本金	|
|	paidInterest }}	|	string	|	TRUE	|	单笔还币交易已还币息	|
|	nextId	|	long	|	FALSE	|	下页查询起始编号（仅在存在下页数据时返回）	|

## 资产划转
POST /v2/c2c/transfer<br>
API Key 权限：交易<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	from	|	string	|	TRUE	|	转出账户ID	|
|	to	|	string	|	TRUE	|	转入账户ID	|
|	currency	|	string	|	TRUE	|	划转币种	|
|	amount	|	string	|	TRUE	|	划转金额	|

注：<br>
•	仅允许现货账户与借入账户间划转。<br>

> Response

```json
{
    "data": {
        "transactId": 5585,
        "transactTime": "1593178102345"
    },
    "code": 200,
    "success": true
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|	状态码	|
|	message	|	string	|	FALSE	|	错误描述（如有）	|
|	data	|	object	|	TRUE	|		|
|	{ transactId	|	string	|	TRUE	|	划转交易ID	|
|	transactTime }	|	long	|	TRUE	|	划转交易时间（unix time in millisecond）	|

## 查询账户余额

GET /v2/c2c/account<br>
API Key 权限：读取<br>

### 请求参数
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	accountId	|	string	|	TRUE	|	账户ID	|
|	currency	|	string	|	FALSE	|	币种	|

> Response

```json
{
    "data": {
        "accountId": 13699363,
        "accountStatus": "working",
        "symbol": "btcusdt",
        "riskRate": "10",//风险率为10，意味着最低风险
        "subAccountTypes": [
            {
                "currency": "btc",
                "subAccountType": "trade",
                "acctBalance": "0.00000029",
                "availBalance": "0.00000029",
                "transferable": "0.00000029",
                "borrowable": "0.01969453"
            },
            {
                "currency": "usdt",
                "subAccountType": "trade",
                "acctBalance": "90.27945823",
                "availBalance": "90.27945823",
                "transferable": "90.27945823",
                "borrowable": "180.56423403"
            },
            {
                "currency": "usdt",
                "subAccountType": "loan",
                "acctBalance": "0",
                "availBalance": "0",
                "transferable": "0",
                "borrowable": "0"
            },
            {
                "currency": "usdt",
                "subAccountType": "interest",
                "acctBalance": "0",
                "availBalance": "0",
                "transferable": "0",
                "borrowable": "0"
            }
        ]
    },
    "code": 200,
    "success": true
}
```

### 响应数据
|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	-----	|	------	|	----	|
|	code	|	integer	|	TRUE	|	状态码	|
|	message	|	string	|	FALSE	|	错误描述（如有）	|
|	data	|	object	|	TRUE	|		|
|	{ accountId	|	string	|	TRUE	|	账户ID	|
|	accountStatus	|	string	|	TRUE	|	账户状态（working 正常, lock 锁定, fl-sys 系统自动爆仓, fl-mgt 手动爆仓, fl-end 爆仓结束, fl-negative 穿仓）	|
|	symbol	|	string	|	FALSE	|	交易对（仅对借入账户类型有效）	|
|	riskRate	|	string	|	FALSE	|	风险率（仅对借入账户类型有效）	|
|	subAccountTypes	|	object	|	TRUE	|	账户子类型列表	|
|	{ subAccountType	|	string	|	TRUE	|	账户子类型（trade, lending, earnings, loan, interest, advance）	|
|	currency	|	string	|	TRUE	|	币种	|
|	acctBalance	|	string	|	TRUE	|	账户余额	|
|	availBalance	|	string	|	FALSE	|	可用余额 （仅对借入账户下trade子类型有效）	|
|	transferable	|	string	|	FALSE	|	可转出金额 （仅对借入账户下trade子类型有效）	|
|	borrowable }}	|	string	|	FALSE	|	可借入金额 （仅对借入账户下trade子类型有效）	|

注：<br>
•	账户子类型trade, loan, interest, advance仅对借入账户有效；<br>
•	账户子类型trade, lending, earnings仅对借出账户有效。<br>


# Websocket行情数据

## 简介

### 接入URL

**Global站行情请求地址（除MBP增量推送及MBP全量REQ以外Websocket行情频道）**

**`wss://api.huobi.pro/ws`**  

**`wss://api-aws.huobi.pro/ws`**  

**MBP增量推送及MBP全量REQ请求地址**

**`wss://api.huobi.pro/feed`**  

**`wss://api-aws.huobi.pro/feed`** 

### 数据压缩

WebSocket 行情接口返回的所有数据都进行了 GZIP 压缩，需要 client 在收到数据之后解压。

### 心跳消息

```json
{"ping": 1492420473027} 
```

当用户的Websocket客户端连接到火币Websocket服务器后，服务器会定期（当前设为5秒）向其发送`ping`消息并包含一整数值。

```json
{"pong": 1492420473027} 
```

当用户的Websocket客户端接收到此心跳消息后，应返回`pong`消息并包含同一整数值。

<aside class="warning">当Websocket服务器连续两次发送了`ping`消息却没有收到任何一次`pong`消息返回后，服务器将主动断开与此客户端的连接。</aside>

### 订阅主题

> Sub request:

```json
{
  "sub": "market.btcusdt.kline.1min",
  "id": "id1"
}
```

成功建立与Websocket服务器的连接后，Websocket客户端发送请求以订阅特定主题：

{
  "sub": "topic to sub",
  "id": "id generate by client"
}

> Sub response:

```json
{
  "id": "id1",
  "status": "ok",
  "subbed": "market.btcusdt.kline.1min",
  "ts": 1489474081631
}
```

成功订阅后，Websocket客户端将收到确认。

之后, 一旦所订阅的主题有更新，Websocket客户端将收到服务器推送的更新消息（push）。

### 取消订阅

> UnSub request:

```json
{
  "unsub": "market.btcusdt.trade.detail",
  "id": "id4"
}
```

取消订阅的格式如下：

{
  "unsub": "topic to unsub",
  "id": "id generate by client"
}

> UnSub response:

```json
{
  "id": "id4",
  "status": "ok",
  "unsubbed": "market.btcusdt.trade.detail",
  "ts": 1494326028889
}
```

取消订阅成功确认。

### 请求数据

Websocket服务器同时支持一次性请求数据（pull）。

一次性请求的格式如下：

{
  "req": "topic to req",
  "id": "id generate by client"
}

一次性返回数据的具体格式参见各个主题。

### 限频

数据请求（req）限频规则

单个连接每两次请求不能小于100ms。

### 错误码

以下是WebSocket行情接口的错误码、错误消息和说明。

| 错误码      | 错误消息                               | 说明                     |
| ----------- | -------------------------------------- | ------------------------ |
| bad-request | invalid topic                          | topic错误                |
| bad-request | invalid symbol                         | symbol错误               |
| bad-request | symbol trade not open now              | 该交易对未到开始交易时间 |
| bad-request | 429 too many request                   | req 请求太频繁           |
| bad-request | unsub with not subbed topic            | 未订阅该主题             |
| bad-request | not json string                        | 发送的请求不是JSON格式   |
| 1008        | header required correct cloud-exchange | exchangeCode 参数错误    |
| bad-request | request timeout                        | 请求超时                 |

## K线数据

### 主题订阅

一旦K线数据产生，Websocket服务器将通过此订阅主题接口推送至客户端：

`market.$symbol$.kline.$period$`

> 订阅请求

```json
{
  "sub": "market.ethbtc.kline.1min",
  "id": "id1"
}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 描述     | 取值范围                                                     |
| ------ | -------- | -------- | -------- | ------------------------------------------------------------ |
| symbol | string   | true     | 交易代码 | btcusdt, ethbtc...等（如需获取杠杆ETP净值K线，净值symbol = 杠杆ETP交易对symbol + 后缀‘nav’，例如：btc3lusdtnav） |
| period | string   | true     | K线周期  | 1min, 5min, 15min, 30min, 60min, 4hour, 1day, 1mon, 1week, 1year |

> Response

```json
{
  "id": "id1",
  "status": "ok",
  "subbed": "market.ethbtc.kline.1min",
  "ts": 1489474081631 //system response time
}
```

> Update example

```json
{
  "ch": "market.ethbtc.kline.1min",
  "ts": 1489474082831, //system update time
  "tick": {
    "id": 1489464480,
    "amount": 0.0,
    "count": 0,
    "open": 7962.62,
    "close": 7962.62,
    "low": 7962.62,
    "high": 7962.62,
    "vol": 0.0
  }
}
```

### 数据更新字段列表

| 字段   | 数据类型 | 描述                                        |
| ------ | -------- | ------------------------------------------- |
| id     | integer  | unix时间，同时作为K线ID                     |
| amount | float    | 成交量                                      |
| count  | integer  | 成交笔数                                    |
| open   | float    | 开盘价                                      |
| close  | float    | 收盘价（当K线为最晚的一根时，是最新成交价） |
| low    | float    | 最低价                                      |
| high   | float    | 最高价                                      |
| vol    | float    | 成交额, 即 sum(每一笔成交价 * 该笔的成交量) |

<aside class="notice">当symbol被设为“hb10”或“huobi10”时，amount，count，vol均为零值。</aside>
### 数据请求

用请求方式一次性获取K线数据需要额外提供以下参数：
（每次最多返回300条）

```json
{
  "req": "market.$symbol.kline.$period",
  "id": "id generated by client",
  "from": "from time in epoch seconds",
  "to": "to time in epoch seconds"
}
```

| 参数 | 数据类型 | 是否必需 | 缺省值                                | 描述                            | 取值范围                                                     |
| ---- | -------- | -------- | ------------------------------------- | ------------------------------- | ------------------------------------------------------------ |
| from | integer  | false    | 1501174800(2017-07-28T00:00:00+08:00) | 起始时间 (epoch time in second) | [1501174800, 2556115200]                                     |
| to   | integer  | false    | 2556115200(2050-01-01T00:00:00+08:00) | 结束时间 (epoch time in second) | [1501174800, 2556115200] or ($from, 2556115200] if "from" is set |

## 市场深度行情数据

此主题发送最新市场深度快照。快照频率为每秒1次。

### 主题订阅

`market.$symbol.depth.$type`

> Subscribe request

```json
{
  "sub": "market.btcusdt.depth.step0",
  "id": "id1"
}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述         | 取值范围                                               |
| ------ | -------- | -------- | ------ | ------------ | ------------------------------------------------------ |
| symbol | string   | true     | NA     | 交易代码     | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |
| type   | string   | true     | step0  | 合并深度类型 | step0, step1, step2, step3, step4, step5               |

**"type" 合并深度类型**

| Value | Description                          |
| ----- | ------------------------------------ |
| step0 | 不合并深度                           |
| step1 | Aggregation level = precision*10     |
| step2 | Aggregation level = precision*100    |
| step3 | Aggregation level = precision*1000   |
| step4 | Aggregation level = precision*10000  |
| step5 | Aggregation level = precision*100000 |

当type值为‘step0’时，默认深度为150档;
当type值为‘step1’,‘step2’,‘step3’,‘step4’,‘step5’时，默认深度为20档。

> Response

```json
{
  "id": "id1",
  "status": "ok",
  "subbed": "market.btcusdt.depth.step0",
  "ts": 1489474081631 //system response time
}
```

> Update example

```json
{
  "ch": "market.htusdt.depth.step0",
  "ts": 1572362902027, //system update time
  "tick": {
    "bids": [
      [3.7721, 344.86],// [price, size]
      [3.7709, 46.66] 
    ],
    "asks": [
      [3.7745, 15.44],
      [3.7746, 70.52]
    ],
    "version": 100434317651,
    "ts": 1572362902012 //quote time
  }
}
```

### 数据更新字段列表

<aside class="notice">在'tick'object下方呈现买盘卖盘深度列表</aside>
| 字段    | 数据类型 | 描述                         |
| ------- | -------- | ---------------------------- |
| bids    | object   | 当前的所有买单 [price, size] |
| asks    | object   | 当前的所有卖单 [price, size] |
| version | integer  | 内部字段                     |
| ts      | integer  | 新加坡时间的时间戳，单位毫秒 |

<aside class="notice">当symbol被设为"hb10"时，amount, count, vol均为零值 </aside>
### 数据请求

支持数据请求方式一次性获取市场深度数据：

```json
{
  "req": "market.btcusdt.depth.step0",
  "id": "id10"
}
```

## 市场深度MBP行情数据（增量推送）

用户可订阅此频道以接收最新深度行情Market By Price (MBP) 的增量数据推送；同时，该频道支持用户以req方式请求获取全量数据。

**MBP增量推送及MBP全量REQ请求地址**

**`wss://api.huobi.pro/feed`**  

**`wss://api-aws.huobi.pro/feed`** 

建议下游数据处理方式：<br>
1）	订阅增量数据并开始缓存；<br>
2）	请求全量数据（同等档位数）并根据该全量消息的seqNum与缓存增量数据中的prevSeqNum对齐；<br>
3）	开始连续增量数据接收与计算，构建并持续更新MBP订单簿；<br>
4）	每条增量数据的prevSeqNum须与前一条增量数据的seqNum一致，否则意味着存在增量数据丢失，须重新获取全量数据并对齐；<br>
5）	如果收到增量数据包含新增price档位，须将该price档位插入MBP订单簿中适当位置；<br>
6）	如果收到增量数据包含已有price档位，但size不同，须替换MBP订单簿中该price档位的size；<br>
7）	如果收到增量数据某price档位的size为0值，须将该price档位从MBP订单簿中删除；<br>
8）	如果收到单条增量数据中包含两个及以上price档位的更新，这些price档位须在MBP订单簿中被同时更新。<br>

当前仅支持5档/20档MBP逐笔增量以及150档MBP快照增量的推送，二者的区别为 -<br>
1） 深度不同；<br>
2） 5档/20档为逐笔增量MBP行情，150档为100毫秒定时快照增量MBP行情；<br>
3） 当5档/20档订单簿仅发生单边行情变化时，增量推送仅包含单边行情更新，比如，推送消息中包含数组asks，但不含数组bids；<br>

```json
{
    "ch": "market.btcusdt.mbp.5",
    "ts": 1573199608679,
    "tick": {
        "seqNum": 100020146795,
        "prevSeqNum": 100020146794,
        "asks": [
            [645.140000000000000000, 26.755973959140651643]
        ]
    }
}
```
当150档订单簿仅发生单边行情变化时，增量推送包含双边行情更新，但其中一边行情为空，比如，推送消息中包含数组asks更新的同时，也包含bids空数组；<br>

```json
{
    "ch":"market.btcusdt.mbp.150",
    "ts":1573199608679,
    "tick":{
        "seqNum":100020146795,
        "prevSeqNum":100020146794,
        "bids":[ ],
        "asks":[
            [645.14,26.75597395914065]
        ]
    }
}
```
未来，150档增量推送的数据行为将与5档/20档增量保持一致，即，单边深度行情变更时，推送消息中将不包含另一边行情深度行情；<br>
4） 当150档订单簿在100毫秒时间间隔内未发生变化时，增量推送包含bids和asks空数组；<br>

```json
{
    "ch":"market.zecusdt.mbp.150",
    "ts":1585074391470,
    "tick":{
        "seqNum":100772868478,
        "prevSeqNum":100772868476,
        "bids":[  ],
        "asks":[  ]
    }
}
```
而5档/20档MBP逐笔增量，在订单簿未发生变化时，不推送数据；<br>
未来，150档增量推送的数据行为将与5档增量保持一致，即，在订单簿未发生变化时，不再推送空消息；<br>
5）5档/20档逐笔增量行情仅支持部分交易对（btcusdt,ethusdt,xrpusdt,eosusdt,ltcusdt,etcusdt,adausdt,dashusdt,bsvusdt），150档快照增量支持全部交易对。<br>

REQ频道支持5档/20档/150档全量数据的获取。<br>

### 订阅增量推送

`market.$symbol.mbp.$levels`

> Sub request

```json
{
  "sub": "market.btcusdt.mbp.5",
  "id": "id1"
}
```

### 请求全量数据

`market.$symbol.mbp.$levels`

> Req request

```json
{
  "req": "market.btcusdt.mbp.5",
  "id": "id2"
}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述                         | 取值范围                         |
| ------ | -------- | -------- | ------ | ---------------------------- | -------------------------------- |
| symbol | string   | true     | NA     | 交易代码（不支持通配符）     |                                  |
| levels | integer  | true     | NA     | 深度档位（取值：5, 20, 150） | 当前仅支持5档，20档，或150档深度 |

> Response (增量订阅)

```json
{
  "id": "id1",
  "status": "ok",
  "subbed": "market.btcusdt.mbp.5",
  "ts": 1489474081631 //system response time
}
```

> Incremental Update (增量订阅)

```json
{
	"ch": "market.btcusdt.mbp.5",
	"ts": 1573199608679, //system update time
  "tick": {
           "seqNum": 100020146795,
            "prevSeqNum": 100020146794,
           "asks": [
                 [645.140000000000000000, 26.755973959140651643] // [price, size]
           ]
      }
}
```

> Response (全量请求)

```json
{
	"id": "id2",
	"rep": "market.btcusdt.mbp.150",
	"status": "ok",
	"data": {
		"seqNum": 100020142010,
		"bids": [
			[618.37, 71.594], // [price, size]
			[423.33, 77.726],
			[223.18, 47.997],
			[219.34, 24.82],
			[210.34, 94.463]
    ],
		"asks": [
			[650.59, 14.909733438479636],
			[650.63, 97.996],
			[650.77, 97.465],
			[651.23, 83.973],
			[651.42, 34.465]
		]
	}
}
```

### 数据更新字段列表

| 字段       | 数据类型 | 描述                                    |
| ---------- | -------- | --------------------------------------- |
| seqNum     | integer  | 消息序列号                              |
| prevSeqNum | integer  | 上一消息序列号                          |
| bids       | object   | 买盘，按price降序排列，["price","size"] |
| asks       | object   | 卖盘，按price升序排列，["price","size"] |

## 市场深度MBP行情数据（全量推送）

用户可订阅此频道以接收最新深度行情Market By Price (MBP) 的全量数据推送。推送频率为大约100毫秒一次。

### 订阅增量推送

`market.$symbol.mbp.refresh.$levels`

> Sub request

```json
{
"sub": "market.btcusdt.mbp.refresh.20",
"id": "id1"
}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述                     | 取值范围 |
| ------ | -------- | -------- | ------ | ------------------------ | -------- |
| symbol | string   | true     | NA     | 交易代码（不支持通配符） |          |
| levels | integer  | true     | NA     | 深度档位                 | 5,10,20  |

> Response

```json
{
"id": "id1",
"status": "ok",
"subbed": "market.btcusdt.mbp.refresh.20",
"ts": 1489474081631 //system response time
}
```

> Refresh Update

```json
{
"ch": "market.btcusdt.mbp.refresh.20",
"ts": 1573199608679, //system update time
"tick": {

		"seqNum": 100020142010,
		"bids": [
			[618.37, 71.594], // [price, size]
			[423.33, 77.726],
			[223.18, 47.997],
			[219.34, 24.82],
			[210.34, 94.463], ... // 省略余下15档
   		],
		"asks": [
			[650.59, 14.909733438479636],
			[650.63, 97.996],
			[650.77, 97.465],
			[651.23, 83.973],
			[651.42, 34.465], ... // 省略余下15档
		]
}
}
```

### 数据更新字段列表

| 字段   | 数据类型 | 描述                                    |
| ------ | -------- | --------------------------------------- |
| seqNum | integer  | 消息序列号                              |
| bids   | object   | 买盘，按price降序排列，["price","size"] |
| asks   | object   | 卖盘，按price升序排列，["price","size"] |


## 买一卖一逐笔行情

当买一价、买一量、卖一价、卖一量，其中任一数据发生变化时，此主题推送逐笔更新。

### 主题订阅

`market.$symbol.bbo`

> Subscribe request

```json
{
  "sub": "market.btcusdt.bbo",
  "id": "id1"
}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述     | 取值范围                                               |
| ------ | -------- | -------- | ------ | -------- | ------------------------------------------------------ |
| symbol | string   | true     | NA     | 交易代码 | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |

> Response

```json
{
  "id": "id1",
  "status": "ok",
  "subbed": "market.btcusdt.bbo",
  "ts": 1489474081631 //system response time
}
```

> Update example

```json
{
  "ch": "market.btcusdt.bbo",
  "ts": 1489474082831, //system update time
  "tick": {
    "symbol": "btcusdt",
    "quoteTime": "1489474082811",
    "bid": "10008.31",
    "bidSize": "0.01",
    "ask": "10009.54",
    "askSize": "0.3",
    "seqId":"10242474683"
  }
}
```

### 数据更新字段列表

| 字段      | 数据类型 | 描述         |
| --------- | -------- | ------------ |
| symbol    | string   | 交易代码     |
| quoteTime | long     | 盘口更新时间 |
| bid       | float    | 买一价       |
| bidSize   | float    | 买一量       |
| ask       | float    | 卖一价       |
| askSize   | float    | 卖一量       |
| seqId     | int      | 消息序号     |


## 成交明细

### 主题订阅

此主题提供市场最新成交逐笔明细。

`market.$symbol.trade.detail`

> Subscribe request

```json
{
  "sub": "market.btcusdt.trade.detail",
  "id": "id1"
}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述     | 取值范围                                               |
| ------ | -------- | -------- | ------ | -------- | ------------------------------------------------------ |
| symbol | string   | true     | NA     | 交易代码 | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`） |

> Response

```json
{
  "id": "id1",
  "status": "ok",
  "subbed": "market.btcusdt.trade.detail",
  "ts": 1489474081631 //system response time
}
```

> Update example

```json
{
  "ch": "market.btcusdt.trade.detail",
  "ts": 1489474082831, //system update time
  "tick": {
        "id": 14650745135,
        "ts": 1533265950234, //trade time
        "data": [
            {
                "amount": 0.0099,
                "ts": 1533265950234, //trade time
                "id": 146507451359183894799,
                "tradeId": 102043494568,
                "price": 401.74,
                "direction": "buy"
            }
            // more Trade Detail data here
        ]
  }
}
```

### 数据更新字段列表

| 字段      | 数据类型 | 描述                                           |
| --------- | -------- | ---------------------------------------------- |
| id        | integer  | 唯一成交ID（将被废弃）                         |
| tradeId   | integer  | 唯一成交ID（NEW）                              |
| amount    | float    | 成交量（买或卖一方）                           |
| price     | float    | 成交价                                         |
| ts        | integer  | 成交时间 (UNIX epoch time in millisecond)      |
| direction | string   | 成交主动方 (taker的订单方向) : 'buy' or 'sell' |

### 数据请求

支持数据请求方式一次性获取成交明细数据（仅能获取最多最近300个成交记录）：

```json
{
  "req": "market.btcusdt.trade.detail",
  "id": "id11"
}
```

## 市场概要

### 主题订阅

此主题提供24小时内最新市场概要快照。快照频率不超过每秒10次。

`market.$symbol.detail`

> Subscribe request

```json
{
  "sub": "market.btcusdt.detail",
  "id": "id1"
}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述     | 取值范围             |
| ------ | -------- | -------- | ------ | -------- | -------------------- |
| symbol | string   | true     | NA     | 交易代码 | btcusdt, ethbtc...等 |

> Response

```json
{
  "id": "id1",
  "status": "ok",
  "subbed": "market.btcusdt.detail",
  "ts": 1489474081631 //system response time
}
```

> Update example

```json
{
  "ch": "market.btcusdt.detail",
  "ts": 1494496390001, //system update time
  "tick": {
    "amount": 12224.2922,
    "open":   9790.52,
    "close":  10195.00,
    "high":   10300.00,
    "id":     1494496390,
    "count":  15195,
    "low":    9657.00,
    "vol":    121906001.754751
  }
}
```

### 数据更新字段列表

| 字段   | 数据类型 | 描述                     |
| ------ | -------- | ------------------------ |
| id     | integer  | unix时间，同时作为消息ID |
| amount | float    | 24小时成交量             |
| count  | integer  | 24小时成交笔数           |
| open   | float    | 24小时开盘价             |
| close  | float    | 最新价                   |
| low    | float    | 24小时最低价             |
| high   | float    | 24小时最高价             |
| vol    | float    | 24小时成交额             |

### 数据请求

支持数据请求方式一次性获取市场概要数据：

```json
{
  "req": "market.btcusdt.detail",
  "id": "id11"
}
```

## 杠杆ETP实时净值推送

### 主题订阅

此主题提供杠杆ETP实时净值的推送。

`market.$symbol.etp`

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述     | 取值范围      |
| ------ | -------- | -------- | ------ | -------- | ------------- |
| symbol | string   | true     | NA     | 交易代码 | 杠杆ETP交易对 |

### 数据更新字段列表

| 字段名称       | 数据类型 | 描述                                        |
| -------------- | -------- | -----------------------------------------|
| symbol         | string   | 杠杆ETP交易代码                             |
| nav            | float    | 最新净值                                  |
| navTime        | long     | 最新净值更新时间 (unix time in millisecond) |
| outstanding    | float    | ETP总份额                                  |
| basket         | object   | 篮子                                     |
| { currency     | float    | 币种                                      |
| amount }       | float    | 金额                                      |
| actualLeverage | float    | 实际杠杆率                                |

# Websocket资产及订单（即将废弃）

## 简介（即将废弃）

### 接入URL

**Websocket资产及订单**

**`wss://api.huobi.pro/ws/v1`**  

**`wss://api-aws.huobi.pro/ws/v1`**   

注：api-aws.huobi.pro域名对使用aws云服务的用户做了一定的链路延迟优化。  

请使用中国大陆以外的服务器访问火币 API。

### 数据压缩

WebSocket 资产及订单v1版本返回的所有数据都进行了 GZIP 压缩，需要 client 在收到数据之后解压。

### 心跳消息

 **2019/07/08之后**

当用户的Websocket客户端连接到火币Websocket服务器后，服务器会定期（当前设为20秒）向其发送`ping`消息并包含一整数值如下：

> {
> "op":"ping",
> "ts":1492420473027
> } (资产订单推送)

当用户的Websocket客户端接收到此心跳消息后，应返回`pong`消息并包含同一整数值：

> {
> "op":"pong",
> "ts":1492420473027
> } （资产订单推送）

<aside class="warning">当Websocket服务器连续三次发送了`ping`消息却没有收到任何一次`pong`消息返回后，服务器将主动断开与此客户端的连接。</aside>
**2019/07/08之前**

当用户的Websocket客户端连接到火币Websocket服务器后，服务器会定期（设为30秒）向其发送`ping`消息并包含一整数值如下：

> {
> "op":"ping",
> "ts":1492420473027
> }

当用户的Websocket客户端接收到此心跳消息后，应返回`pong`消息并包含同一整数值：

> {
> "op":"pong",
> "ts":1492420473027
> }

<aside class="warning">当Websocket服务器连续两次发送了`ping`消息却没有收到任何一次`pong`消息返回后，服务器将主动断开与此客户端的连接。</aside>
### 订阅主题

成功建立与Websocket服务器的连接后，Websocket客户端发送如下请求以订阅特定主题：

```json
{
  "op": "operation type, 'sub' for subscription, 'unsub' for unsubscription",
  "topic": "topic to sub",
  "cid": "id generate by client"
}
```

成功订阅后，Websocket客户端将收到确认：

```json
{
  "op": "operation type, refer to the operation which triggers this response",
  "cid": "id1",
  "error-code": 0, // 0 for no error
  "topic": "topic to sub if the op is sub",
  "ts": 1489474081631
}
```

之后, 一旦所订阅的主题有更新，Websocket客户端将收到服务器推送的更新消息（push）：

```json
{
  "op": "notify",
  "topic": "topic of this notify",
  "ts": 1489474082831,
  "data": {
    // data of specific topic update
  }
}
```

### 取消订阅

取消订阅的格式如下：

```json
{
  "op": "unsub",
  "topic": "accounts",
  "cid": "client generated id"
}
```

取消订阅成功确认：

```json
{
  "op": "unsub",
  "topic": "accounts",
  "cid": "id generated by client",
  "err-code": 0,
  "ts": 1489474081631
}
```

### 请求数据

Websocket服务器同时支持一次性请求数据（pull）。

当与Websocket服务器成功建立连接后，以下三个主题可供用户请求：

* accounts.list
* orders.list
* orders.detail

具体请求方式请见后文。

### 限频

**数据请求（sub）限频规则**

限频规则基于API key而不是连接。当sub数量超出限值时，Websocket客户端将收到"too many request"错误码。具体规则如下：

单个连接每秒最多50次sub和50次unsub。
单个连接sub总量限制100个，sub总量达到限额后不允许再sub，但每次unsub可以减少sub总量的计数。比如：30个sub后unsub 1个，此时sub总量count为29，还有71个sub总量可用。 

**数据请求（req）限频规则**

限频规则基于API key而不是连接。当请求频率超出限值时，Websocket客户端将收到"too many request"错误码。以下为各主题当前限频设定：

* accounts.list: once every 2 seconds
* orders.list AND orders.detail: once every 5 seconds

### 鉴权

资产及订单主题鉴权请求数据格式如下：

```json
{
  "op": "auth",
  "AccessKeyId": "e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx",
  "SignatureMethod": "HmacSHA256",
  "SignatureVersion": "2",
  "Timestamp": "2017-05-11T15:19:30",
  "Signature": "4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o=",
}
```

**鉴权请求数据格式说明**

| filed            | type   | instruction                                                  |      |
| ---------------- | ------ | ------------------------------------------------------------ | ---- |
| op               | string | 必填；操作名称，鉴权固定值为 auth；                          |      |
| cid              | string | 选填；Client 请求唯一 ID                                     |      |
| AccessKeyId      | string | 必填； 您申请的 API Key 中的 AccessKey                       |      |
| SignatureMethod  | string | 必填；签名方法, 用户计算签名的基于哈希的协议，此处使用 HmacSHA256 |      |
| SignatureVersion | string | 必填；签名协议的版本，此处使用 2                             |      |
| Timestamp        | string | 必填；时间戳, 您发出请求的时间 (UTC 时区) (UTC 时区) (UTC 时区) 。在查询请求中包含此值有助于防止第三方截取您的请求。如：2017-05-11T16:22:06。再次强调是 (UTC 时区) |      |
| Signature        | string | 必填；签名, 计算得出的值，用于确保签名有效和未被篡改         |      |

**注：**

- 参考[签名认证](#c64cd15fdc)生成有效签名
- 签名计算中请求方法固定值为`GET`，WebSocket v1路径固定为`/ws/v1`
- JSON请求中的数据不需要URL编码

## 订阅账户更新（即将废弃）

API Key 权限：读取

订阅账户资产变动更新。

### 主题订阅

`accounts`

> Subscribe request

```json
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "topic": "accounts",
  "model": "0"
}
```

### 参数

| 参数  | 数据类型 | 是否必需 | 缺省值 | 描述               | 取值范围                              |
| ----- | -------- | -------- | ------ | ------------------ | ------------------------------------- |
| model | string   | false    | 0      | 是否包含已冻结余额 | 1 to include frozen balance, 0 to not |

<aside class="notice">如果同时订阅可用和总余额，需要为 0 和 1 各开启一条websocket连接</aside>
> Response

```json
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "err-code": 0,
  "ts": 1489474081631,
  "topic": "accounts"
}
```

> Update example

```json
{
  "op": "notify",
  "ts": 1522856623232,
  "topic": "accounts",
  "data": {
    "event": "order.place",
    "list": [
      {
        "account-id": 419013,
        "currency": "usdt",
        "type": "trade",
        "balance": "500009195917.4362872650"
      }
    ]
  }
}

```

### 数据更新字段列表

| 字段       | 数据类型 | 描述                                                         |
| ---------- | -------- | ------------------------------------------------------------ |
| event      | string   | 资产变化通知相关事件说明，比如订单创建(order.place) 、订单成交(order.match)、订单成交退款（order.refund)、订单撤销(order.cancel) 、点卡抵扣交易手续费（order.fee-refund)、杠杆账户划转（margin.transfer)、借币本金（margin.loan)、借币计息（margin.interest)、归还借币本金币息(margin.repay)、其他资产变化(other)、充币（deposit）、提币（withdraw） |
| account-id | integer  | 账户 id                                                      |
| currency   | string   | 币种                                                         |
| type       | string   | 账户类型, 交易子账户（trade),借币子账户（loan），币息子账户（interest) |
| balance    | string   | 账户余额 (当订阅model=0时，该余额为可用余额；当订阅model=1时，该余额为总余额） |

注：<br>
账户更新推送的是到账金额，多笔成交产生的多笔交易返佣可能会合并到帐。<br>


## 订阅订单更新（即将废弃）

API Key 权限：读取

订阅账户下的订单更新。

### 主题订阅

`orders.$symbol`

> Subscribe request

```json
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "topic": "orders.htusdt",
}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述     | 取值范围                                                     |
| ------ | -------- | -------- | ------ | -------- | ------------------------------------------------------------ |
| symbol | string   | true     | NA     | 交易代码 | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`）, 支持通配符"*". |

> Response

```json
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "err-code": 0,
  "ts": 1489474081631,
  "topic": "orders.htusdt"
}
```

> Update example

```json
{
  "op": "notify",
  "topic": "orders.htusdt",
  "ts": 1522856623232,
  "data": {
    "seq-id": 94984,
    "order-id": 2039498445,
    "symbol": "htusdt",
    "account-id": 100077,
    "order-amount": "5000.000000000000000000",
    "order-price": "1.662100000000000000",
    "created-at": 1522858623622,
    "order-type": "buy-limit",
    "order-source": "api",
    "order-state": "filled",
    "role": "taker|maker",
    "price": "1.662100000000000000",
    "filled-amount": "5000.000000000000000000",
    "unfilled-amount": "0.000000000000000000",
    "filled-cash-amount": "8301.357280000000000000",
    "filled-fees": "8.000000000000000000"
  }
}
```

### 数据更新字段列表

| 字段               | 数据类型 | 描述                                                         |
| ------------------ | -------- | ------------------------------------------------------------ |
| seq-id             | integer  | 流水号(不连续)                                               |
| order-id           | integer  | 订单 id                                                      |
| symbol             | string   | 交易对                                                       |
| account-id         | string   | 账户 id                                                      |
| order-amount       | string   | 订单数量                                                     |
| order-price        | string   | 订单价格                                                     |
| created-at         | int      | 订单创建时间 (UNIX epoch time in millisecond)                |
| order-type         | string   | 订单类型, 有效取值: buy-market, sell-market, buy-limit, sell-limit, buy-ioc, sell-ioc, buy-limit-maker, sell-limit-maker,buy-stop-limit,sell-stop-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| order-source       | string   | 订单来源, 有效取值: sys, web, api, app                       |
| order-state        | string   | 订单状态, 有效取值: submitted, partial-filled, filled, canceled, partial-canceled |
| role               | string   | 成交角色: taker or maker                                     |
| price              | string   | 成交价格                                                     |
| filled-amount      | string   | 单次成交数量                                                 |
| unfilled-amount    | string   | 单次未成交数量                                               |
| filled-cash-amount | string   | 单次成交金额                                                 |
| filled-fees        | string   | 单次成交手续费（买入为币，卖出为钱）                         |

## 订阅订单更新 (即将废弃)

API Key 权限：读取

相比现有用户订单更新推送主题“orders.$symbol”， 新增主题“orders.$symbol.update”拥有更低的数据延迟以及更准确的消息顺序。建议API用户订阅此新主题接收订单更新推送，以替代现有订阅主题 “orders.$symbol”。（现有订阅主题 “orders.$symbol”仍将在Websocket API服务中被保留直至另行通知。）

### 主题订阅

`orders.$symbol.update`

> Subscribe request

```json
{
  "op": "sub",
  "cid": "40sG903yz80oDFWr",
  "topic": "orders.htusdt.update"
}
```

### 参数

| 参数   | 数据类型 | 是否必需 | 缺省值 | 描述                                                         | 取值范围 |
| ------ | -------- | -------- | ------ | ------------------------------------------------------------ | -------- |
| symbol | string   | true     | NA     | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`）, 支持通配符"*". |          |



> Response

```json
{
  "op": "sub",
  "ts": 1489474081631,
  "topic": "orders.htusdt.update",
  "err-code": 0,
  "cid": "40sG903yz80oDFWr"  
}
```

> Update example

```json
{
  "op": "notify",
  "ts": 1522856623232,
  "topic": "orders.htusdt.update",  
  "data": {
    "unfilled-amount": "0.000000000000000000",
    "filled-amount": "5000.000000000000000000",
    "price": "1.662100000000000000",
    "order-id": 2039498445,
    "symbol": "htusdt",
    "match-id": 94984,
    "filled-cash-amount": "8301.357280000000000000",
    "role": "taker|maker",
    "order-state": "filled",
    "client-order-id": "a0001",
    "order-type": "buy-limit"
  }
}
```

### 数据更新字段列表

| Field              | Data Type | Description                                                  |
| ------------------ | --------- | ------------------------------------------------------------ |
| match-id           | integer   | 最近撮合编号（当order-state = submitted, canceled, partial-canceled时，match-id 为消息序列号；当order-state = filled, partial-filled 时，match-id 为最近撮合编号。） |
| order-id           | integer   | 订单编号                                                     |
| symbol             | string    | 交易代码                                                     |
| order-state        | string    | 订单状态, 有效取值: submitted, partial-filled, filled, canceled, partial-canceled |
| role               | string    | 最近成交角色（当order-state = submitted, canceled, partial-canceled时，role 为缺省值taker；当order-state = filled, partial-filled 时，role 取值为taker 或maker。） |
| price              | string    | 最新价（当order-state = submitted 时，price 为订单价格；当order-state = canceled, partial-canceled 时，price 为零；当order-state = filled, partial-filled 时，price 为最近成交价。） |
| filled-amount      | string    | 最近成交数量                                                 |
| filled-cash-amount | string    | 最近成交数额                                                 |
| unfilled-amount    | string    | 最近未成交数量（当order-state = submitted 时，unfilled-amount 为原始订单量；当order-state = canceled OR partial-canceled 时，unfilled-amount 为未成交数量；当order-state = filled 时，如果 order-type = buy-market，unfilled-amount 可能为一极小值；如果order-type <> buy-market 时，unfilled-amount 为零；当order-state = partial-filled AND role = taker 时，unfilled-amount 为未成交数量；当order-state = partial-filled AND role = maker 时，unfilled-amount 为未成交数量。） |
| client-order-id    | string    | 用户自编订单号                                               |
| order-type         | string    | 订单类型，包括buy-market, sell-market, buy-limit, sell-limit, buy-ioc, sell-ioc, buy-limit-maker, sell-limit-maker,buy-stop-limit => buy-limit,sell-stop-limit => sell-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok => buy-limit-fok, sell-stop-limit-fok => sell-limit-fok |


## 请求用户资产数据（即将废弃）

API Key 权限：读取

查询当前用户的所有账户余额数据。

### 数据请求

`accounts.list`

> Query request

```json
{
  "op": "req",
  "cid": "40sG903yz80oDFWr",
  "topic": "accounts.list",
}
```
成功建立和 WebSocket API 的连接之后，向 Server发送如下格式的数据来查询账户数据：

| 参数  | 数据类型 | 描述                         |      |
| ----- | -------- | ---------------------------- | ---- |
| op    | string   | 必填；操作名称，固定值为 req |      |
| cid   | string   | 选填；Client 请求唯一 ID     |      |
| topic | string   | 必填；固定值为accounts.list  |      |

### 返回

> Successful

```json
    {
      "op": "req",
      "topic": "accounts.list",
      "cid": "40sG903yz80oDFWr",
      "err-code": 0,
      "ts": 1489474082831,
      "data": [
        {
          "id": 419013,
          "type": "spot",
          "state": "working",
          "list": [
            {
              "currency": "usdt",
              "type": "trade",
              "balance": "500009195917.4362872650"
            },
            {
              "currency": "usdt",
              "type": "frozen",
              "balance": "9786.6783000000"
            }
          ]
        },
        {
          "id": 35535,
          "type": "point",
          "state": "working",
          "list": [
            {
              "currency": "eth",
              "type": "trade",
              "balance": "499999894616.1302471000"
            },
            {
              "currency": "eth",
              "type": "frozen",
              "balance": "9786.6783000000"
            }
          ]
        }
      ]
    }
```

> Failed

```json
    {
      "op": "req",
      "topic": "foo.bar",
      "cid": "40sG903yz80oDFWr",
      "err-code": 12001, //Response codes,0  represent success;others value  is error,the list of Response codes is in appendix
      "err-msg": "detail of error message",
      "ts": 1489474081631
    }
```

| 字段       | 数据类型 | 描述       |      |
| ---------- | -------- | ---------- | ---- |
| { id       | long     | 账户ID     |      |
| type       | string   | 账户类型   |      |
| state      | string   | 账户状态   |      |
| list       | string   | 账户列表   |      |
| {currency  | string   | 子账户币种 |      |
| type       | string   | 子账户类型 |      |
| balance }} | string   | 子账户余额 |      |

## 请求当前及历史订单（即将废弃）

API Key 权限：读取

根据设定条件查询当前委托、历史委托。

### 数据请求

`orders.list`

> Query request

```json
{
  "op": "req",
  "topic": "orders.list",
  "cid": "40sG903yz80oDFWr",
  "symbol": "htusdt",
  "states": "submitted,partial-filled"
}
```

### 参数

| 参数       | 数据类型 | 是否必需 | 缺省值 | 描述                             | 取值范围                                                     |
| ---------- | -------- | -------- | ------ | -------------------------------- | ------------------------------------------------------------ |
| account-id | int      | true     | NA     | 账户 id                          | NA                                                           |
| symbol     | string   | true     | NA     | 交易对                           | btcusdt, ethbtc...（取值参考`GET /v1/common/symbols`）       |
| types      | string   | false    | NA     | 查询的订单类型组合，使用','分割  | buy-market, sell-market, buy-limit, sell-limit, buy-ioc, sell-ioc， buy-limit-maker, sell-limit-maker, buy-stop-limit，sell-stop-limit, buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| states     | string   | true     | NA     | 查询的订单状态组合，使用','分割  | submitted, partial-filled, partial-canceled, filled, canceled，created |
| start-date | string   | false    | -61d   | 查询开始日期, 日期格式yyyy-mm-dd | NA                                                           |
| end-date   | string   | false    | today  | 查询结束日期, 日期格式yyyy-mm-dd | NA                                                           |
| from       | string   | false    | NA     | 查询起始 ID                      | NA                                                           |
| direct     | string   | false    | next   | 查询方向                         | next, prev                                                   |
| size       | string   | false    | 100    | 查询记录大小                     | [1, 100]                                                     |

### 数据更新字段列表

> Successful

```json
{
  "op": "req",
  "topic": "orders.list",
  "cid": "40sG903yz80oDFWr",
  "err-code": 0,
  "ts": 1522856623232,
  "data": [
    {
      "id": 2039498445,
      "symbol": "htusdt",
      "account-id": 100077,
      "amount": "5000.000000000000000000",
      "price": "1.662100000000000000",
      "created-at": 1522858623622,
      "type": "buy-limit",
      "filled-amount": "5000.000000000000000000",
      "filled-cash-amount": "8301.357280000000000000",
      "filled-fees": "8.000000000000000000",
      "finished-at": 1522858624796,
      "source": "api",
      "state": "filled",
      "canceled-at": 0
    }
  ]
}
```

| 字段               | 数据类型 | 描述                         |      |
| ------------------ | -------- | ---------------------------- | ---- |
| id                 | long     | 订单ID                       |      |
| symbol             | string   | 交易对                       |      |
| account-id         | long     | 账户ID                       |      |
| amount             | string   | 订单数量                     |      |
| price              | string   | 订单价格                     |      |
| created-at         | long     | 订单创建时间                 |      |
| type               | string   | 订单类型，请参考订单类型说明 |      |
| filled-amount      | string   | 已成交数量                   |      |
| filled-cash-amount | string   | 已成交总金额                 |      |
| filled-fees        | string   | 已成交手续费                 |      |
| finished-at        | string   | 最后成交时间                 |      |
| source             | string   | 订单来源，请参考订单来源说明 |      |
| state              | string   | 订单状态，请参考订单状态说明 |      |
| cancel-at          | long     | 撤单时间                     |      |
| stop-price         | string   | 止盈止损订单触发价格         |      |
| operator           | string   | 止盈止损订单触发价运算符     |      |


## 以订单编号请求订单（即将废弃）

API Key 权限：读取

以订单编号请求订单数据

### 数据请求

`orders.detail`

> Query request

```json
{
  "op": "req",
  "topic": "orders.detail",
  "order-id": "2039498445",
  "cid": "40sG903yz80oDFWr"
}
```

### 参数

| 参数     | 是否必需 | 数据类型 | 描述                   | 缺省值 | 取值范围 |      |
| -------- | -------- | -------- | ---------------------- | ------ | -------- | ---- |
| op       | true     | string   | 操作名称，固定值为 req |        |          |      |
| cid      | true     | string   | Client 请求唯一 ID     |        |          |      |
| topic    | false    | string   | 固定值为 orders.detail |        |          |      |
| order-id | true     | string   | 订单ID                 |        |          |      |


### 返回

> Successful

```json
{
  "op": "req",
  "topic": "orders.detail",
  "cid": "40sG903yz80oDFWr",
  "err-code": 0,
  "ts": 1522856623232,
  "data": {
    "id": 2039498445,
    "symbol": "htusdt",
    "account-id": 100077,
    "amount": "5000.000000000000000000",
    "price": "1.662100000000000000",
    "created-at": 1522858623622,
    "type": "buy-limit",
    "filled-amount": "5000.000000000000000000",
    "filled-cash-amount": "8301.357280000000000000",
    "filled-fees": "8.000000000000000000",
    "finished-at": 1522858624796,
    "source": "api",
    "state": "filled",
    "canceled-at": 0
  }
}
```
| 字段               | 数据类型 | 描述                         |      |
| ------------------ | -------- | ---------------------------- | ---- |
| id                 | long     | 订单ID                       |      |
| symbol             | string   | 交易对                       |      |
| account-id         | long     | 账户ID                       |      |
| amount             | string   | 订单数量                     |      |
| price              | string   | 订单价格                     |      |
| created-at         | long     | 订单创建时间                 |      |
| type               | string   | 订单类型，请参考订单类型说明 |      |
| filled-amount      | string   | 已成交数量                   |      |
| filled-cash-amount | string   | 已成交总金额                 |      |
| filled-fees        | string   | 已成交手续费                 |      |
| finished-at        | string   | 最后成交时间                 |      |
| source             | string   | 订单来源，请参考订单来源说明 |      |
| state              | string   | 订单状态，请参考订单状态说明 |      |
| cancel-at          | long     | 撤单时间                     |      |
| stop-price         | string   | 止盈止损订单触发价格         |      |
| operator           | string   | 止盈止损订单触发价运算符     |      |


# Websocket资产及订单（v2）

## 简介

### 接入URL

**Websocket资产及订单（v2）**

**`wss://api.huobi.pro/ws/v2`**  

**`wss://api-aws.huobi.pro/ws/v2`**   

注：api-aws.huobi.pro域名对使用aws云服务的用户做了一定的链路延迟优化。  

请使用中国大陆以外的服务器访问火币 API。

### 数据压缩

与v1版本不同，v2版本返回的数据未进行 GZIP 压缩。

### 心跳消息

当用户的Websocket客户端连接到火币WebSocket服务器后，服务器会定期（当前设为20秒）向其发送`Ping`消息并包含一整数值如下：

```json
{
	"action": "ping",
	"data": {
		"ts": 1575537778295
	}
}
```

当用户的Websocket客户端接收到此心跳信息后，应返回`Pong`消息并包含同一整数值：

```json
{
    "action": "pong",
    "data": {
          "ts": 1575537778295 // 使用Ping消息中的ts值
    }
}
```

### `action`的有效取值

| 有效取值   | 取值说明                             |
| ---------- | ------------------------------------ |
| sub        | 订阅数据                             |
| req        | 数据请求                             |
| ping、pong | 心跳数据                             |
| push       | 推送数据，服务端发送至客户端数据类型 |

### 限频

此版本对用户采取了多维度的限频策略，具体策略如下：

- 限制单连接**有效**的请求（包括req，sub，unsub，不包括ping/pong和其他无效请求)为**50次/秒**（此处秒限制为滑动窗口）。当超过此限制时，会返回"too many request"错误消息。
- 限制单API Key建连总数为**10**。当超过此限制时，会返回"too many connection"错误消息。
- 限制单IP建立连接数为**100次/秒**。当超过次限制时，会返回"too many request"错误消息。

### 鉴权

鉴权请求格式如下：

```json
{
    "action": "req", 
    "ch": "auth",
    "params": { 
        "authType":"api",
        "accessKey": "e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx",
        "signatureMethod": "HmacSHA256",
        "signatureVersion": "2.1",
        "timestamp": "2019-09-01T18:16:16",
        "signature": "4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o="
    }
}

```

鉴权成功后返回数据格式如下：

```json
{
	"action": "req",
	"code": 200,
	"ch": "auth",
	"data": {}
}
```

参数说明

| 字段             | 是否必需 | 数据类型 | 描述                                                         |
| ---------------- | -------- | -------- | ------------------------------------------------------------ |
| action           | true     | string   | Websocket数据操作类型，鉴权固定值为req                       |
| ch               | true     | string   | 请求主题，鉴权固定值为auth                                   |
| authType         | true     | string   | 鉴权类型，鉴权固定值为api。注意，该参数不在签名计算中。      |
| accessKey        | true     | string   | 您申请的API Key中的AccessKey                                 |
| signatureMethod  | true     | string   | 签名方法，用户计算签名寄语哈希的协议，固定值为HmacSHA256     |
| signatureVersion | true     | string   | 签名协议版本，固定值为2.1                                    |
| timestamp        | true     | string   | 时间戳，您发出请求的时间（UTC时间）在查询请求中包含此值有助于防止第三方截取您的请求。如：2017-05-11T16:22:06。再次强调是 (UTC 时区) |
| signature        | true     | string   | 签名, 计算得出的值，用于确保签名有效和未被篡改               |

### 签名步骤

v2.1版本签名与v2.0版本签名步骤相似，具体区别如下：

1. 生成参与签名的字符串时，请求方法固定使用GET，请求地址固定为/ws/v2

2. 生成参与签名的固定参数名替换为：accessKey，signatureMethod，signatureVersion，timestamp

3. signatureVersion版本升级为2.1

v2版本签名步骤,您可以点击 <a href='https://huobiapi.github.io/docs/spot/v1/cn/#c64cd15fdc'>这里</a> 获取。

签名前最后生成的字符串如下：

```
GET\n
api.huobi.pro\n
/ws/v2\n
accessKey=0664b695-rfhfg2mkl3-abbf6c5d-49810&signatureMethod=HmacSHA256&signatureVersion=2.1&timestamp=2019-12-05T11%3A53%3A03
```

注：JSON请求中的数据不需要URL编码。

### 订阅主题

成功建立与Websocket服务器的连接后，Websocket客户端发送如下请求以订阅特定主题：

```json
{
	"action": "sub",
	"ch": "accounts.update"
}
```
订阅成功Websocket客户端会接收到如下消息：

```json
{
	"action": "sub",
	"code": 200,
	"ch": "accounts.update#0",
	"data": {}
}
```

### 请求数据

成功建立Websocket服务器的连接后，Websocket客户端发送如下请求用以获取一次性数据：


```json
{
    "action": "req", 
    "ch": "topic",
}
```

请求成功后Websocket客户端会收到如下消息：

```json
{
    "action": "req",
    "ch": "topic",
    "code": 200,
    "data": {} // 请求数据体
}
```

### 错误码

以下是WebSocket资产和订单接口的错误码、错误消息和说明。

| 错误码 | 错误消息                 | 说明                                                         |
| ------ | ------------------------ | ------------------------------------------------------------ |
| 200    | 正确                     | 正确返回                                                     |
| 100    | 超时关闭                 | 超时关闭                                                     |
| 400    | Bad Request              | 请求错误                                                     |
| 404    | Not Found                | 找不到服务                                                   |
| 429    | Too Many Requests        | 超过单机服务最大连接数或者超过单IP最大连接数                 |
| 500    | 系统异常                 | 系统错误                                                     |
| 2000   | invalid.ip               | 无效的ip                                                     |
| 2001   | nvalid.json              | 无效的请求json                                               |
| 2001   | invalid.authType         | 验签方式错误                                                 |
| 2001   | invalid.action           | 无效的订阅事件                                               |
| 2001   | invalid.symbol           | 无效的交易对                                                 |
| 2001   | invalid.ch               | 无效的订阅                                                   |
| 2001   | invalid.exchange         | 无效的交易所code                                             |
| 2001   | missing.param.auth       | 缺少验签参数                                                 |
| 2002   | invalid.auth.state       | 认证未通过                                                   |
| 2002   | auth.fail                | 验签失败，包括API Key绑定的IP错误                            |
| 2003   | query.account.list.error | 查询账户列表失败                                             |
| 4000   | too.many.request         | 客户端上行请求限频（单个实例50次/秒）                        |
| 4000   | too.many.connection      | 同一个API Key的建联数量超过服务器单个实例限制（单个实例最多连接10个） |

## 订阅订单更新

API Key 权限：读取

订单的更新推送由任一以下事件触发：<br>
-	计划委托或追踪委托触发失败事件（eventType=trigger）<br>
- 计划委托或追踪委托触发前撤单事件（eventType=deletion）<br>
- 订单创建（eventType=creation）<br>
-	订单成交（eventType=trade）<br>
-	订单撤销（eventType=cancellation）<br>

不同事件类型所推送的消息中，字段列表略有不同。开发者可以采取以下两种方式设计返回的数据结构：<br>
- 定义一个包含所有字段的数据结构，并允许某些字段为空<br>
- 定义不同的数据结构，分别包含各自的字段，并继承自一个包含公共数据字段的数据结构

### 订阅主题

` orders#${symbol}`

### 订阅参数

> Subscribe request

```json
{
	"action": "sub",
	"ch": "orders#btcusdt"
}

```

> Response

```json
{
	"action": "sub",
	"code": 200,
	"ch": "orders#btcusdt",
	"data": {}
}
```

| 参数   | 数据类型 | 描述                      |
| ------ | -------- | ------------------------- |
| symbol | string   | 交易代码（支持通配符 * ） |


### 数据更新字段列表

> Update example

```json
{
	"action":"push",
	"ch":"orders#btcusdt",
	"data":
	{
		"orderSide":"buy",
		"lastActTime":1583853365586,
		"clientOrderId":"abc123",
		"orderStatus":"rejected",
		"symbol":"btcusdt",
		"eventType":"trigger",
		"errCode": 2002,
		"errMessage":"invalid.client.order.id (NT)"
	}
}
```

当计划委托/追踪委托触发失败后 –

| 字段          | 数据类型 | 描述                                                         |
| ------------- | -------- | ------------------------------------------------------------ |
| eventType     | string   | 事件类型，有效值：trigger（本事件仅对计划委托/追踪委托有效） |
| symbol        | string   | 交易代码                                                     |
| clientOrderId | string   | 用户自编订单号                                               |
| orderSide     | string   | 订单方向，有效值：buy,sell                                   |
| orderStatus   | string   | 订单状态，有效值：rejected                                   |
| errCode       | int      | 订单触发失败错误码                                           |
| errMessage    | string   | 订单触发失败错误消息                                         |
| lastActTime   | long     | 订单触发失败时间                                             |

> Update example

```json
{
	"action":"push",
	"ch":"orders#btcusdt",
	"data":
	{
		"orderSide":"buy",
		"lastActTime":1583853365586,
		"clientOrderId":"abc123",
		"orderStatus":"canceled",
		"symbol":"btcusdt",
		"eventType":"deletion"
	}
}
```

当计划委托/追踪委托在触发前被撤销后 –

| 字段          | 数据类型 | 描述                                                         |
| ------------- | -------- | ------------------------------------------------------------ |
| eventType     | string   | 事件类型，有效值：deletion（本事件仅对计划委托/追踪委托有效） |
| symbol        | string   | 交易代码                                                     |
| clientOrderId | string   | 用户自编订单号                                               |
| orderSide     | string   | 订单方向，有效值：buy,sell                                   |
| orderStatus   | string   | 订单状态，有效值：canceled                                   |
| lastActTime   | long     | 订单撤销时间                                                 |

> Update example

```json
{
	"action":"push",
	"ch":"orders#btcusdt",
	"data":
	{
		"orderSize":"2.000000000000000000",
		"orderCreateTime":1583853365586,
		"accountId":992701,
		"orderPrice":"77.000000000000000000",
		"type":"sell-limit",
		"orderId":27163533,
		"clientOrderId":"abc123",
		"orderSource":"spot-api",
		"orderStatus":"submitted",
		"symbol":"btcusdt",
		"eventType":"creation"
	}
}
```

当订单挂单后 –

| 字段            | 数据类型 | 描述                                                         |
| --------------- | -------- | ------------------------------------------------------------ |
| eventType       | string   | 事件类型，有效值：creation                                   |
| symbol          | string   | 交易代码                                                     |
| accountId       | long     | 账户ID                                                       |
| orderId         | long     | 订单ID                                                       |
| clientOrderId   | string   | 用户自编订单号（如有）                                       |
| orderSource     | string   | 订单来源                                                     |
| orderPrice      | string   | 订单价格                                                     |
| orderSize       | string   | 订单数量（对市价买单无效）                                   |
| orderValue      | string   | 订单金额（仅对市价买单有效）                                 |
| type            | string   | 订单类型，有效值：buy-market, sell-market, buy-limit, sell-limit, buy-limit-maker, sell-limit-maker, buy-ioc, sell-ioc, buy-limit-fok, sell-limit-fok |
| orderStatus     | string   | 订单状态，有效值：submitted                                  |
| orderCreateTime | long     | 订单创建时间                                                 |

注：<BR>
- 止盈止损订单在尚未被触发时，接口将不会推送此订单的创建；<br>
- Taker订单在成交前，接口首先推送其创建事件。<br>
- 止盈止损订单的订单类型不再是原始订单类型“buy-stop-limit”或“sell-stop-limit”，而是变为“buy-limit”或“sell-limit”。<BR>

> Update example

```json
{
	"action":"push",
	"ch":"orders#btcusdt",
	"data":
	{
		"tradePrice":"76.000000000000000000",
		"tradeVolume":"1.013157894736842100",
		"tradeId":301,
		"tradeTime":1583854188883,
		"aggressor":true,
		"remainAmt":"0.000000000000000400000000000000000000",
		"execAmt":"2",
		"orderId":27163536,
		"type":"sell-limit",
		"clientOrderId":"abc123",
		"orderSource":"spot-api",
		"orderPrice":"15000",
		"orderSize":"0.01",
		"orderStatus":"filled",
		"symbol":"btcusdt",
		"eventType":"trade"
	}
}
```

当订单成交后 –

| 字段          | 数据类型 | 描述                                                         |
| ------------- | -------- | ------------------------------------------------------------ |
| eventType     | string   | 事件类型，有效值：trade                                      |
| symbol        | string   | 交易代码                                                     |
| tradePrice    | string   | 成交价                                                       |
| tradeVolume   | string   | 成交量                                                       |
| orderId       | long     | 订单ID                                                       |
| type          | string   | 订单类型，有效值：buy-market, sell-market, buy-limit, sell-limit, buy-limit-maker, sell-limit-maker, buy-ioc, sell-ioc, buy-limit-fok, sell-limit-fok |
| clientOrderId | string   | 用户自编订单号（如有）                                       |
| orderSource   | string   | 订单来源                                                     |
| orderPrice    | string   | 原始订单价（市价单无效）                                     |
| orderSize     | string   | 原始订单数量（市价买单无效）                                 |
| orderValue    | string   | 原始订单金额（仅对市价买单有效）                             |
| tradeId       | long     | 成交ID                                                       |
| tradeTime     | long     | 成交时间                                                     |
| aggressor     | bool     | 是否交易主动方，有效值： true (taker), false (maker)         |
| orderStatus   | string   | 订单状态，有效值：partial-filled, filled                     |
| remainAmt     | string   | 该订单未成交数量（市价买单为未成交金额）                     |
| execAmt       | string   | 该订单累计成交量                                             |

注：<BR>
- 止盈止损订单的订单类型不再是原始订单类型“buy-stop-limit”或“sell-stop-limit”，而是变为“buy-limit”或“sell-limit”。<BR>
- 当一张taker订单同时与对手方多张订单成交后，所产生的每笔成交（tradePrice, tradeVolume, tradeTime, tradeId, aggressor）将被分别推送（而不是合并推送一笔）。<BR>

> Update example

```json
{
	"action":"push",
	"ch":"orders#btcusdt",
	"data":
	{
		"lastActTime":1583853475406,
		"remainAmt":"2.000000000000000000",
		"execAmt":"2",
		"orderId":27163533,
		"type":"sell-limit",
		"clientOrderId":"abc123",
		"orderSource":"spot-api",
		"orderPrice":"15000",
		"orderSize":"0.01",
		"orderStatus":"canceled",
		"symbol":"btcusdt",
		"eventType":"cancellation"
	}
}
```

当订单被撤销后 –

| 字段          | 数据类型 | 描述                                                         |
| ------------- | -------- | ------------------------------------------------------------ |
| eventType     | string   | 事件类型，有效值：cancellation                               |
| symbol        | string   | 交易代码                                                     |
| orderId       | long     | 订单ID                                                       |
| type          | string   | 订单类型，有效值：buy-market, sell-market, buy-limit, sell-limit, buy-limit-maker, sell-limit-maker, buy-ioc, sell-ioc, buy-limit-fok, sell-limit-fok |
| clientOrderId | string   | 用户自编订单号（如有）                                       |
| orderSource   | string   | 订单来源                                                     |
| orderPrice    | string   | 原始订单价（市价单无效）                                     |
| orderSize     | string   | 原始订单数量（市价买单无效）                                 |
| orderValue    | string   | 原始订单金额（仅对市价买单有效）                             |
| orderStatus   | string   | 订单状态，有效值：partial-canceled, canceled                 |
| remainAmt     | string   | 该订单未成交数量（市价买单为未成交金额）                     |
| execAmt       | string   | 该订单累计成交量                                             |
| lastActTime   | long     | 订单最近更新时间                                             |
注：<BR>
- 止盈止损订单的订单类型不再是原始订单类型“buy-stop-limit”或“sell-stop-limit”，而是变为“buy-limit”或“sell-limit”。<BR>

## 订阅清算后成交及撤单更新

API Key 权限：读取

仅当用户订单成交或撤销时推送。其中，订单成交为逐笔推送，如一张 taker 订单同时与多张 maker 订单成交，该接口将推送逐笔更新。但用户收到的这几笔成交消息的次序，有可能与实际的成交次序不完全一致。另外，如果一张订单的成交及撤销几乎同时发生，例如 IOC 订单成交后剩余部分被自动撤销，用户可能会先收到撤单推送，再收到成交推送。<br>

如用户需要获取依次更新的订单推送，建议订阅另一频道 orders#${symbol}。<br>

### 订阅主题

`trade.clearing#${symbol}#${mode}`

### 订阅参数

| 参数   | 数据类型 | 是否必需 | 描述                                                         |
| ------ | -------- | -------- | ------------------------------------------------------------ |
| symbol | string   | TRUE     | 交易代码（支持通配符 * ）                                    |
| mode   | int      | FALSE    | 推送模式（0 - 仅在订单成交时推送；1 - 在订单成交、撤销时均推送；缺省值：0） |

注：<br>
可选订阅参数 mode，如不填或填0，仅推送成交事件；如填1，推送成交及撤销事件。<br>

> Subscribe request

```json
{
	"action": "sub",
	"ch": "trade.clearing#btcusdt#0"
}

```

> Response

```json
{
	"action": "sub",
	"code": 200,
	"ch": "trade.clearing#btcusdt#0",
	"data": {}
}
```

> Update example

```json
{
    "ch": "trade.clearing#btcusdt#0",
    "data": {
         "eventType": "trade",
         "symbol": "btcusdt",
         "orderId": 99998888,
         "tradePrice": "9999.99",
         "tradeVolume": "0.96",
         "orderSide": "buy",
         "aggressor": true,
         "tradeId": 919219323232,
         "tradeTime": 998787897878,
         "transactFee": "19.88",
         "feeDeduct ": "0",
         "feeDeductType": "",
         "feeCurrency": "btc",
         "accountId": 9912791,
         "source": "spot-api",
         "orderPrice": "10000",
         "orderSize": "1",
         "clientOrderId": "a001",
         "orderCreateTime": 998787897878,
         "orderStatus": "partial-filled"
    }
}
```

### 数据更新字段列表（当订单成交后）

| 字段            | 数据类型 | 描述                                                         |
| --------------- | -------- | ------------------------------------------------------------ |
| eventType       | string   | 事件类型（trade）                                            |
| symbol          | string   | 交易代码                                                     |
| orderId         | long     | 订单ID                                                       |
| tradePrice      | string   | 成交价                                                       |
| tradeVolume     | string   | 成交量                                                       |
| orderSide       | string   | 订单方向，有效值： buy, sell                                 |
| orderType       | string   | 订单类型，有效值： buy-market, sell-market,buy-limit,sell-limit,buy-ioc,sell-ioc,buy-limit-maker,sell-limit-maker,buy-stop-limit,sell-stop-limit,buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| aggressor       | bool     | 是否交易主动方，有效值： true, false                         |
| tradeId         | long     | 交易ID                                                       |
| tradeTime       | long     | 成交时间，unix time in millisecond                           |
| transactFee     | string   | 交易手续费（正值）或交易手续费返佣（负值）                   |
| feeCurrency     | string   | 交易手续费或交易手续费返佣币种（买单的交易手续费币种为基础币种，卖单的交易手续费币种为计价币种；买单的交易手续费返佣币种为计价币种，卖单的交易手续费返佣币种为基础币种） |
| feeDeduct       | string   | 交易手续费抵扣                                               |
| feeDeductType   | string   | 交易手续费抵扣类型，有效值： ht, point                       |
| accountId       | long     | 账户编号                                                     |
| source          | string   | 订单来源                                                     |
| orderPrice      | string   | 订单价格 （市价单无此字段）                                  |
| orderSize       | string   | 订单数量（市价买单无此字段）                                 |
| orderValue      | string   | 订单金额（仅市价买单有此字段）                               |
| clientOrderId   | string   | 用户自编订单号                                               |
| stopPrice       | string   | 订单触发价（仅止盈止损订单有此字段）                         |
| operator        | string   | 订单触发方向（仅止盈止损订单有此字段）                       |
| orderCreateTime | long     | 订单创建时间                                                 |
| orderStatus     | string   | 订单状态，有效值：filled, partial-filled                     |

注：<br>
- transactFee中的交易返佣金额可能不会实时到账；<br>

### 数据更新字段列表（当订单撤销后）

| 字段            | 数据类型 | 描述                                                         |
| --------------- | -------- | ------------------------------------------------------------ |
| eventType       | string   | 事件类型（cancellation）                                     |
| symbol          | string   | 交易代码                                                     |
| orderId         | long     | 订单ID                                                       |
| orderSide       | string   | 订单方向，有效值： buy, sell                                 |
| orderType       | string   | 订单类型，有效值： buy-market, sell-market,buy-limit,sell-limit,buy-ioc,sell-ioc,buy-limit-maker,sell-limit-maker,buy-stop-limit,sell-stop-limit,buy-limit-fok, sell-limit-fok, buy-stop-limit-fok, sell-stop-limit-fok |
| accountId       | long     | 账户编号                                                     |
| source          | string   | 订单来源                                                     |
| orderPrice      | string   | 订单价格 （市价单无此字段）                                  |
| orderSize       | string   | 订单数量（市价买单无此字段）                                 |
| orderValue      | string   | 订单金额（仅市价买单有此字段）                               |
| clientOrderId   | string   | 用户自编订单号                                               |
| stopPrice       | string   | 订单触发价（仅止盈止损订单有此字段）                         |
| operator        | string   | 订单触发方向（仅止盈止损订单有此字段）                       |
| orderCreateTime | long     | 订单创建时间                                                 |
| remainAmt       | string   | 未成交量（对于市价买单，该字段定义为未成交额）               |
| orderStatus     | string   | 订单状态，有效值：canceled, partial-canceled                 |


## 订阅账户变更

API Key 权限：读取

订阅账户的余额更新。

### 订阅主题

`accounts.update#${mode}`

用户可选择以下任一账户变更推送的触发方式

1、仅在账户余额发生变动时推送；

2、在账户余额发生变动或可用余额发生变动时均推送，且分别推送。

注意：现货和合约之间的账户划转引起的账户余额变动，暂时没有消息推送。

### 订阅参数

| 参数 | 数据类型 | 描述                              |
| ---- | -------- | --------------------------------- |
| mode | integer  | 推送方式，有效值：0, 1，默认值：0 |

订阅示例  
1、不填mode：  
accounts.update  
仅当账户余额变动时推送；  
2、填写mode=0：  
accounts.update#0  
仅当账户余额变动时推送；  
3、填写mode=1：  
accounts.update#1  
在账户余额发生变动或可用余额发生变动时均推送且分别推送。  

注：无论用户采用哪种模式订阅，在订阅成功后，服务器将首先推送当前各账户的账户余额与可用余额，然后再推送后续的账户更新。在首推各账户初始值时，消息中的changeType和changeTime的值为null。

> Subscribe request

```json
{
	"action": "sub",
	"ch": "accounts.update"
}
```

> Response

```json
{
	"action": "sub",
	"code": 200,
	"ch": "accounts.update#0",
	"data": {}
}
```

> Update example

```json
accounts.update#0：
{
	"action": "push",
	"ch": "accounts.update#0",
	"data": {
		"currency": "btc",
		"accountId": 123456,
		"balance": "23.111",
		"changeType": "transfer",
           	"accountType":"trade",
		"changeTime": 1568601800000
	}
}

accounts.update#1：
{
	"action": "push",
	"ch": "accounts.update#1",
	"data": {
		"currency": "btc",
		"accountId": 33385,
		"available": "2028.699426619837209087",
		"changeType": "order.match",
         		"accountType":"trade",
		"changeTime": 1574393385167
	}
}
{
	"action": "push",
	"ch": "accounts.update#1",
	"data": {
		"currency": "btc",
		"accountId": 33385,
		"balance": "2065.100267619837209301",
		"changeType": "order.match",
           	"accountType":"trade",
		"changeTime": 1574393385122
	}
}
```

### 数据更新字段列表

| 字段        | 数据类型 | 描述                                                         |
| ----------- | -------- | ------------------------------------------------------------ |
| currency    | string   | 币种                                                         |
| accountId   | long     | 账户ID                                                       |
| balance     | string   | 账户余额（仅当账户余额发生变动时推送）                       |
| available   | string   | 可用余额（仅当可用余额发生变动时推送）                       |
| changeType  | string   | 余额变动类型，有效值：order-place(订单创建)，order-match(订单成交)，order-refund(订单成交退款)，order-cancel(订单撤销)，order-fee-refund(点卡抵扣交易手续费)，margin-transfer(杠杆账户划转)，margin-loan(借币本金)，margin-interest(借币计息)，margin-repay(归还借币本金币息)，deposit (充币）, withdraw (提币)，other(其他资产变化) |
| accountType | string   | 账户类型，有效值：trade, frozen, loan, interest              |
| changeTime  | long     | 余额变动时间，unix time in millisecond                       |

注：<br>
账户更新推送的是到账金额，多笔成交产生的多笔交易返佣可能会合并到帐。<br>


# 稳定币

## 简介

稳定币接口提供了价格查询和兑换功能。

以下是是稳定币接口的错误码和说明。

| 响应码                         | 说明                                             |
| ------------------------------ | ------------------------------------------------ |
| invalid-currency               | 币种无效                                         |
| invalid-amount                 | 币种数量小于最低值（1000）或大于当前可兑换额度   |
| invalid-type                   | type不为sell或buy                                |
| quote-exceed-price-limit       | 报价超过合理范围（小于0.9或者大于1.1）           |
| quote-exceed-time-limit        | 报价时间已经过期                                 |
| quote-failure                  | 后端其他错误引起的后端其他错误引起的价格查询失败 |
| invalid-quote-id               | 无效的quote-id                                   |
| insufficient-balance           | 可用余额不足                                     |
| insufficient-quota             | 稳定币限额不足/超出稳定币限额                    |
| exchange-failure               | 后端其他错误引起的兑换失败                       |
| Base-user-request-exceed-limit | 您的操作太频繁，请稍后再试                       |

## 稳定币兑换价格查询

GET v1/stable-coin/quote
API Key 权限：读取

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述                       | 取值范围         |
| -------- | -------- | ------ | -------------------------- | ---------------- |
| currency | true     | string | 与HUSD兑换的稳定币币种     | PAX/USDC/TUSD    |
| amount   | true     | string | 与HUSD兑换的稳定币币种数量 | amount必须为整数 |
| type     | true     | string | 兑换方向                   | buy兑入/sell兑出 |

### 响应数据

| 参数名称       | 是否必须 | 数据类型 | 描述                       | 取值范围                                                     |
| -------------- | -------- | -------- | -------------------------- | ------------------------------------------------------------ |
| currency       | true     | string   | 与HUSD兑换的稳定币币种     | PAX/USDC/TUSD                                                |
| amount         | true     | string   | 与HUSD兑换的稳定币币种数量 | 因兑换账户额度等因素影响，返回的amount可能会比请求的amount小 |
| type           | true     | string   | 兑换方向                   | buy兑入/sell兑出                                             |
| exchangeAmount | true     | string   | 匹配的HUSD数量             | type=buy时，exchangeAmount为用户所需支付的husd数量；type=sell时，exchangeAmount为用户可获得的husd数量 |
| exchangeFee    | true     | string   | 手续费金额 （单位：HUSD）  |                                                              |
| quoteId        | true     | string   | 该次稳定币报价唯一ID       |                                                              |
| expiration     | true     | string   | 确认兑换有效期             | 时间（一般为接口请求时间向后延伸10秒）                       |

## 兑换稳定币

POST v1/stable-coin/exchange
API Key 权限：交易

### 请求参数

| 参数名称 | 是否必须 | 类型   | 描述                 | 取值范围 |
| -------- | -------- | ------ | -------------------- | -------- |
| quote-id | true     | string | 该次稳定币报价唯一ID |          |

### 响应数据

| 参数名称        | 是否必须 | 数据类型 | 描述                       | 取值范围                                                     |
| --------------- | -------- | -------- | -------------------------- | ------------------------------------------------------------ |
| transact-id     | true     | long     | 兑换记录ID                 |                                                              |
| currency        | true     | string   | 与HUSD兑换的稳定币币种     | PAX/USDC/TUSD                                                |
| amount          | true     | string   | 与HUSD兑换的稳定币币种数量 |                                                              |
| type            | true     | string   | 兑换方向                   | buy兑入/sell兑出                                             |
| exchange-amount | true     | string   | 匹配的HUSD数量             | type=buy时，exchange-amount为用户所需支付的husd数量；type=sell时，exchange-amount为用户可获得的husd数量 |
| exchange-fee    | true     | string   | 手续费金额 （单位：HUSD）  |                                                              |
| time            | true     | long     | 时间戳                     |                                                              |

# ETF（HB10）

## 简介

ETF接口提供了ETF基本信息、换入、换出、查询等功能。

以下是ETF接口的错误码、错误消息和说明。

| 错误码 | 错误消息                                                     | 说明                               |
| ------ | ------------------------------------------------------------ | ---------------------------------- |
| 504    | Missing Parameter: [name]                                    | 缺失参数[参数名]                   |
| 10404  | The fund does not exist                                      | 基金名称不存在（当前只支持hb10）   |
| 13404  | Exchange ratio of the coin and etf is missing                | 基金调整中，不能换入换出           |
| 13406  | Non-API calls. The request is rejected                       | 非API调用，请求被拒绝              |
| 13410  | API signature error                                          | API签名错误                        |
| 13601  | Position adjustment phase: swap-in and swap-out are suspended | 调仓期：暂停换入换出               |
| 13603  | Swap-in and swap-out have been suspended                     | 换入换出已暂停                     |
| 13604  | Swap-in has been suspended                                   | 换入已暂停                         |
| 13605  | Swap-out has been suspended                                  | 换出已暂停                         |
| 13606  | Incorrect transaction share                                  | 申购或赎回份额超出上限或者低于下限 |

## 基本信息

用户可以通过该接口取得关于 ETF 换入换出的 基本信息，包括一次换入最小量，一次换入最大量，一 次换出最小量，一次换出最大量，换入费率，换出费率，最新 ETF 换入换出状态，以及 ETF 的成分结构。

### HTTP 请求

- GET `/etf/swap/config`

### 请求参数

| 参数     | 是否必填 | 数据类型 | 长度 | 说明        | 取值范围 |      |
| -------- | -------- | -------- | ---- | ----------- | -------- | ---- |
| etf_name | true     | string   | -    | etf基金名称 | hb10     |      |

> Response:

```json
{
  "code": 200,
  "data": {
    "purchase_min_amount": 10000,
    "purchase_max_amount": 100000,
    "redemption_min_amount": 10000,
    "redemption_max_amount": 10000,
    "purchase_fee_rate": 0.001,
    "redemption_fee_rate": 0.002,
    "etf_status":1,
    "unit_price":
    [
      {
        "currency": "eth",
        "amount": 19.9
      },
      {
        "currency": "btc",
        "amount": 9.9
      }
    ]
  },
  "message": null,
  "success": true
}
```

### 响应数据

| 参数                  | 是否必填 | 数据类型 | 长度  | 说明                                    | 取值范围                                                     |      |
| --------------------- | -------- | -------- | ----- | --------------------------------------- | ------------------------------------------------------------ | ---- |
| purchase_min_amount   | true     | int      | -     | 最小单次换入数量                        |                                                              |      |
| purchase_max_amount   | False    | int      | -     | 最大单次换入数量                        |                                                              |      |
| redemption_min_amount | true     | int      | -     | 最小单次换出数量                        |                                                              |      |
| redemption_max_amount | False    | int      | -     | 最大单次换出数量                        |                                                              |      |
| purchase_fee_rate     | true     | double   | (5,4) | 换入费率                                |                                                              |      |
| redemption_fee_rate   | true     | double   | (5,4) | 换出费率                                |                                                              |      |
| etf_status            | true     | int      | -     | 换入换出状态                            | 状态： 正常 – 1;  由调仓引起的换入换出暂停 - 2; 其他原因引起的换入换出暂停 - 3; 换入暂停 - 4; 换出暂停 – 5 |      |
| unit_price            | true     | Array    | -     | ETF成分信息，包含成分币代码和对应的数量 | 调仓会引起成分信息发生变化                                   |      |

- unit_price

| 参数     | 是否必填 | 数据类型 | 长度 | 说明       |      |
| -------- | -------- | -------- | ---- | ---------- | ---- |
| currency | true     | string   | -    | 成分币币种 |      |
| amount   | true     | double   | -    | 成分币数量 |      |


## 换入换出

API Key 权限：交易

用户可以通过该接口取得关于 ETF 换入（swap/in）换出（swap/out）的 基本信息，包括一次换入最小量，一次换入最大量，一次换出最小量，一次换出最大量，换入费率，换出费率，最新 ETF 换入换出状态，以及 ETF 的成分结构。


### HTTP 请求

- POST ` /etf/swap/in `

- POST ` /etf/swap/out`

### 请求参数

| 参数     | 是否必填 | 数据类型 | 长度 | 说明                                                         | 取值范围                                                     |      |
| -------- | -------- | -------- | ---- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| etf_name | true     | string   | -    | etf基金名称                                                  | hb10                                                         |      |
| amount   | true     | int      | -    | 换入数量  (POST /etf/swap/in) 或 换出数量 (POST /etf/swap/out) | 换入换出数量的范围请参照接口GET /etf/swap/config 提供的相应范围 |      |


> Response:

```json
{
    "code": 200,
    "data": null,
    "message": null,
    "success": true
}
```


### 响应数据


| 参数    | 是否必填 | 数据类型 | 长度 | 说明         | 取值范围           |      |
| ------- | -------- | -------- | ---- | ------------ | ------------------ | ---- |
| code    | true     | int      | -    | 结果返回码   | 请参照返回码解释表 |      |
| data    | true     |          | -    |              |                    |      |
| message | true     |          | -    |              |                    |      |
| success | true     | Boolean  | -    | 请求是否成功 | true or false      |      |

## 操作记录

API Key 权限：读取

用户可以通过该接口取得关于 ETF 换入换出操 作的明细记录。最多返回 100 条记录。


### HTTP 请求

- GET `/etf/swap/list `

### 请求参数

| 参数     | 是否必填 | 数据类型 | 长度 | 说明             | 取值范围                                               |      |
| -------- | -------- | -------- | ---- | ---------------- | ------------------------------------------------------ | ---- |
| etf_name | true     | string   | -    | etf基金名称      | hb10                                                   |      |
| offset   | true     | int      | -    | 开始位置         | >=0. 比如，当offset=0, 开始位置就 是最新的这一条记录。 |      |
| limit    | true     | int      | -    | 最大返回记录条数 | [1, 100]                                               |      |

> Response:

```json
{
  "code": 200,
  "data": [
    {
      "id": 112222,
      "gmt_created": 1528855872323,
      "currency": "hb10",
      "amount": 11.5,
      "type": 1,
      "status": 2,
      "detail": 
      {
        "used_currency_list": 
        [
          {
            "currency": "btc",
            "amount": 0.666
          },
          {
            "currency": "eth",
            "amount": 0.666
          }
        ],
        "rate": 0.002,
        "fee": 100.11,
        "point_card_amount":1.0,
        "obtain_currency_list": 
        [
          {
            "currency": "hb10",
            "amount": 1000
          }
        ]
      }
    },
    {
      "id": 112223,
      "gmt_created": 1528855872323,
      "currency": "hb10",
      "amount": 11.5,
      "type": 2,
      "status": 1,
      "detail": 
      {
        "used_currency_list": 
        [
          {
            "currency": "btc",
            "amount": 0.666
          },
          {
            "currency": "eth",
            "amount": 0.666
          }
        ],
        "rate": 0.002,
        "fee": 100.11,
        "point_card_amount":1.0,
        "obtain_currency_list":
        [
          {
            "currency": "hb10",
            "amount": 1000
          }
        ]
      }
    }
  ],
  "message": null,
  "success": true
}
```

### 响应数据


| 参数        | 是否必填 | 数据类型 | 长度 | 说明             | 取值范围       |      |
| ----------- | -------- | -------- | ---- | ---------------- | -------------- | ---- |
| id          | true     | long     | -    | 操作ID           |                |      |
| gmt_created | true     | long     | -    | 操作时间（毫秒） |                |      |
| currency    | true     | string   | -    | 基金名称         |                |      |
| amount      | true     | double   | -    | 基金数量         |                |      |
| type        | true     | int      | -    | 操作类型         | 换入-1；换出-2 |      |
| status      | true     | int      | -    | 操作结果状态     | 成功-2         |      |
| detail      | true     | Detail[] | -    | 详情             |                |      |

Detail

| 参数                 | 是否必填 | 数据类型   | 长度 | 说明                                                         |      |
| -------------------- | -------- | ---------- | ---- | ------------------------------------------------------------ | ---- |
| used_currency_list   | ture     | Currency[] | -    | 换出的资产列表。如果是换入，该参数包括的是用于换入的成分币详情。如果是换出，该参数则是用于换出的基金详情。 |      |
| rate                 | ture     | double     | -    | 费率                                                         |      |
| fee                  | ture     | double     | -    | 实际收取的手续费                                             |      |
| point_card_amount    | ture     | double     | -    | 用点卡折扣的手续费                                           |      |
| obtain_currency_list | ture     | Currency[] | -    | 换回的资产列表。如果是换入，该参数包括的是用 于换出的基金详情。如果是换出，该参数则是用于 换入的成分币详情。 |      |

Currency

| 参数     | 是否必填 | 数据类型 | 长度 | 说明                 |      |
| -------- | -------- | -------- | ---- | -------------------- | ---- |
| currency | true     | string   | -    | 成分币名称或基金名称 |      |
| amount   | true     | double   | -    | 数量                 |      |

# 杠杆ETP

## 简介

杠杆ETP接口提供了ETP的换入、换出、调仓、查询等功能。

以下是杠杆ETP接口的错误码、错误消息和说明。

| 错误码 | 错误消息                       | 说明                                                   |
| ------ | ------------------------------ | ------------------------------------------------------ |
| 1002   | 您所在的国家禁止申购赎回       | 用户注册或认证国籍不允许申赎                           |
| 80007  | 申购关闭，订单已取消           | 申购关闭                                               |
| 80008  | 赎回关闭，订单已取消           | 赎回关闭                                               |
| 80009  | 申购金额不得低于{0}            | 小于最小下单量                                         |
| 80010  | 申购金额不得高于{0}            | 高于最大下单量                                         |
| 80011  | 个人今日可申购额度超限         | 个人单日申购已超出限额                                 |
| 80012  | 平台今日可申购额度超限         | 平台整体申购超出                                       |
| 80013  | 赎回数量不得低于{0}            | 小于最小下单量                                         |
| 80014  | 赎回数量不得高于{0}            | 高于最大下单量                                         |
| 80015  | 个人今日可赎回额度超限         | 人单日赎回已超出限额                                   |
| 80016  | 平台今日可赎回额度超限         | 平台整体赎回超出限额                                   |
| 80018  | 资产余额不足                   | 资产余额不足                                           |
| 80019  | 下单失败，请重试               | broker返回非已知错误异常                               |
| 80021  | 申购失败，订单已取消           | 用户申购金额过小，不足合约1张                          |
| 80022  | 赎回失败，订单已取消           | 用户赎回金额过小，不足合约1张                          |
| 80023  | 申购失败，订单已取消           | 行情波动较大，合约下单后计算用户需扣款金额大于下单金额 |
| 80024  | 赎回失败，订单已取消           | 行情波动较大，合约下单后计算用户需扣款金额大于下单金额 |
| 80026  | 系统繁忙，请稍后再试。         | 超出订单排队队列                                       |
| 80027  | 赎回失败，订单已取消           | 没有份额可供用户赎回                                   |
| 80028  | 下单失败，超出该币种的持仓限额 | 下单失败，超出该币种的持仓限额                         |

## 基础参考信息

用户可以通过该接口取得关于杠杆ETP换入换出的基础参考信息。

### HTTP 请求

- GET `/v2/etp/reference`

公共数据接口

### 请求参数

| 名称    | 类型 | 是否必需 | 描述                             |      |
| ------- | ---- | -------- | -------------------------------- | ---- |
| etpName | true | string   | 杠杆ETP名称 (for example: btc3l) |      |

> Response:

```json
{
    "data": {
        "etpStatus": "normal",
        "creationQuota": {
            "maxCreationValue": "10000",
            "minCreationValue": "200",
            "dailyCreationValue": "50000",
            "creationCurrency": "btc3l"
        },
        "maxRedemptionAmount": "1000",
        "minRedemptionAmount": "50",
        "dailyRedemptionAmount": "5000",
        "creationFeeRate": "0.0035",
        "redemptionFeeRate": "0.0035",
        "displayName": "BTC*3/USDT",
        "etpName": "btc3l"
    },
    "code": 200,
    "success": true
}
```

### 响应数据

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	--------	|	-----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|	|
|	{ etpName	|	string	|	TRUE	|杠杆ETP名称	|
|	displayName	|	string	|	TRUE	|杠杆ETP显示名称	|
|	creationQuota	|	object	|	TRUE	|	|
|	{ maxCreationValue	|	int	|	TRUE	|单次最大申购金额	|
|	minCreationValue	|	int	|	TRUE	|单次最小申购金额	|
|	dailyCreationValue	|	int	|	TRUE	|单日最大申购金额	|
|	creationCurrency }	|	string	|	TRUE	|申购金额单位（计价币种）	|
|	maxRedemptionAmount	|	int	|	TRUE	|单次最大赎回数量	|
|	minRedemptionAmount	|	int	|	TRUE	|单次最小赎回数量	|
|	dailyRedemptionAmount	|	int	|	TRUE	|单日最大赎回数量	|
|	creationFeeRate	|	float	|	TRUE	|申购费率	|
|	redemptionFeeRate	|	float	|	TRUE	|赎回费率	|
|	etpStatus	} |	string	|	TRUE	|ETP申购赎回状态（normal, creation-only, redemption-only, halted）	|

## 杠杆ETP换入

用户可以通过该接口换入杠杆ETP。

### HTTP 请求

- POST `/v2/etp/creation`

API Key 权限：交易<br>
限频值：2次/秒<br>

### 请求参数

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	------	|	-----	|
|	etpName	|	string	|	TRUE	| 杠杆ETP名称 (for example: btc3l)	|
|	value	|	float	|	TRUE	| 申购金额（基于计价币种）		|
|	currency	|	string	|	TRUE	| 申购金额单位（计价币种）	|

### 响应数据

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	--------	|	-----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|	|
|	{ transactId	|	long	|	TRUE	|交易ID	|
|	transactTime }	|	long	|	TRUE	|交易时间（unix time in millisecond）	|

注：
返回transactId 不意味着申购成功，用户须在申购后通过查询交易记录确认该申购状态。

## 杠杆ETP换出

用户可以通过该接口换出杠杆ETP。

### HTTP 请求

- POST `/v2/etp/redemption`

API Key 权限：交易<br>
限频值：2次/秒<br>

### 请求参数

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	------	|	-----	|
|	etpName	|	string	|	TRUE	| ETP名称 (for example: btc3l)	|
|	currency	|	string	|	TRUE	| 赎回币种（计价币种）	|
|	amount	|	float	|	TRUE	| 赎回数量	|

### 响应数据

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	--------	|	-----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|	|
|	{ transactId	|	long	|	TRUE	|交易ID	|
|	transactTime }	|	long	|	TRUE	|交易时间（unix time in millisecond）	|

注：
返回transactId不意味着赎回成功，用户须在赎回后通过查询交易记录确认该赎回状态。

## 获取杠杆ETP换入换出记录

用户可以通过该接口获取杠杆ETP换入换出记录。

### HTTP 请求

- GET `/v2/etp/transactions`

API Key 权限：读取<br>
限频值：2次/秒<br>
按transactTime检索<br>

### 请求参数

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	------	|	-----	|
|	etpNames	|	string	|	FALSE	| ETP名称（可多填，以逗号分隔；缺省值：所有ETP名称; for example: btc3l）	|
|	currencies	|	string	|	FALSE	| 计价币种（仅对transactTypes=creation有效；可多填，以逗号分隔；缺省值：该ETP下所有计价币种）	|
|	transactTypes	|	string	|	FALSE	| 交易类型（可多填，以逗号分隔；有效值：creation, redemption；缺省值：所有交易类型）	|
|	transactStatus	|	string	|	FALSE	|交易状态（可多填，以逗号分隔；有效值：completed, processing, clearing, rejected；缺省值：所有交易状态）	|
|	startTime|	long	|	FALSE	|远点时间（unix time in millisecond；取值范围：[(endTime - 10天), endTime]；缺省值：(endTime - 10天)）	|
|	endTime|	long	|	FALSE	|近点时间（unix time in millisecond；取值范围：[(当前时间 - 180天), 当前时间]；缺省值：当前时间）	|
|	sort|	string	|	FALSE	|检索方向（有效值：asc 由远及近, desc 由近及远；缺省值：desc）	|
|	limit|	integer	|	FALSE	|单页最大返回条目数量（取值范围：[1,500]；缺省值：100）	|
|	fromId	|	long	|	FALSE	| 查询起始编号（仅对翻页查询有效）	|

注：<br>
startTime与endTime构成查询窗口，窗口最大可设置为10天，窗口可在“之前180天”与“当前时间”范围内平移。<br>

### 响应数据

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	--------	|	-----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|按用户指定sort方向排列	|
|	{ etpName	|	string	|	TRUE	| 杠杆ETP名称	|
|	transactId	|	long	|	TRUE	|交易ID	|
|	transactTime	|	long	|	TRUE	|交易时间（unix time in millisecond）	|
|	transactType	|	string	|	TRUE	|交易类型（有效值：creation, redemption）	|
|	transactAmount	|	float	|	TRUE	| 实际交易数量（基础币种）	|
|	transactAmountOrig	|	float	|	FALSE	| 原始赎回数量（基于基础币种；仅对transactType=redemption有效）	|
|	transactValue	|	float	|	TRUE	| 实际交易金额（计价币种）	|
|	transactValueOrig	|	float	|	FALSE	| 原始申购金额（基于计价币种；仅对transactType=creation有效）	|
|	transactPrice	|	float	|	TRUE	| 实际交易价格（基于计价币种）	|
|	currency	|	string	|	TRUE	| 计价币种	|
|	transactFee	|	float	|	TRUE	| 交易手续费	|
|	feeCurrency	|	string	|	TRUE	| 交易手续费币种	|
|	transactStatus	|	string	|	TRUE	|交易状态（有效值：completed, processing, clearing, rejected）	|
|	errCode	|	integer	|	FALSE	|错误码（仅对transactStatus=rejected有效）	|
|	errMessage }	|	string	|	FALSE	|错误描述（仅对transactStatus=rejected有效）	|
|	nextId	|	long	|	FALSE	| 下页查询起始编号（仅在存在下页数据时返回）	|

注：<br>
如用户查询时，实际交易数量、实际交易金额、实际交易价格尚未生成，字段transactAmount、transactValue、transactPrice更新为空。<br>

## 获取特定杠杆ETP换入换出记录

用户可以通过该接口获取特定杠杆ETP换入换出记录。

### HTTP 请求

- GET `/v2/etp/transaction`

API Key 权限：读取<br>
限频值：2次/秒<br>

### 请求参数

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	------	|	-----	|
|	transactId	|	long	|	TRUE	|交易ID	|

### 响应数据

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	--------	|	-----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|	|
|	{ etpName	|	string	|	TRUE	| 杠杆ETP名称	|
|	transactId	|	long	|	TRUE	|交易ID	|
|	transactTime	|	long	|	TRUE	|交易时间（unix time in millisecond）	|
|	transactType	|	string	|	TRUE	|交易类型（有效值：creation, redemption）	|
|	transactAmount	|	float	|	TRUE	| 实际交易数量（基础币种）	|
|	transactAmountOrig	|	float	|	FALSE	| 原始赎回数量（基于基础币种；仅对transactType=redemption有效）	|
|	transactValue	|	float	|	TRUE	| 实际交易金额（计价币种）	|
|	transactValueOrig	|	float	|	FALSE	| 原始申购金额（基于计价币种；仅对transactType=creation有效）	|
|	transactPrice	|	float	|	TRUE	| 实际交易价格（基于计价币种）	|
|	currency	|	string	|	TRUE	| 计价币种	|
|	transactFee	|	float	|	TRUE	| 交易手续费	|
|	feeCurrency	|	string	|	TRUE	| 交易手续费币种	|
|	transactStatus	|	string	|	TRUE	|交易状态（有效值：completed, processing, clearing, rejected）	|
|	errCode	|	integer	|	FALSE	|状态码（仅对transactStatus=rejected有效）	|
|	errMessage }	|	string	|	FALSE	|错误描述（仅对transactStatus=rejected有效）	|

注：<br>
如用户查询时，实际交易数量、实际交易金额、实际交易价格尚未生成，字段transactAmount、transactValue、transactPrice更新为空。<br>

## 获取杠杆ETP调仓记录

用户可以通过该接口获取杠杆ETP调仓记录。

### HTTP 请求

- GET `/v2/etp/rebalance`

公共数据接口<br>
按rebalTime检索<br>

### 请求参数

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	------	|	-----	|
|	symbol	|	string	|	TRUE	| ETP交易代码 (for example: btc3lusdt)|
|	rebalTypes	|	string	|	FALSE	| 调仓类型（可多填，以逗号分隔；有效值：daily, adhoc；缺省值：所有类型）	|
|	startTime|	long	|	FALSE	|远点时间（unix time in millisecond；取值范围：[(endTime - 10天), endTime]；缺省值：(endTime - 10天)）	|
|	endTime|	long	|	FALSE	|近点时间（unix time in millisecond；取值范围：[(当前时间 - 180天), 当前时间]；缺省值：当前时间）	|
|	sort|	string	|	FALSE	|检索方向（有效值：asc 由远及近, desc 由近及远；缺省值：desc）	|
|	limit|	integer	|	FALSE	|单页最大返回条目数量（取值范围：[1,500]；缺省值：100）	|
|	fromId	|	long	|	FALSE	| 查询起始编号（仅对翻页查询有效）	|

注：<br>
startTime与endTime构成查询窗口，窗口最大可设置为10天，窗口可在“之前180天”与“当前时间”范围内平移。<br>

> Response

```json
{
  "code": 200,
  "data": [
    {
      "symbol": "btc3lusdt",
      "rebalTime": 1594990401594,
      "rebalType": "adhoc"
    },
    {
      "symbol": "btc3lusdt",
      "rebalTime": 1595065303552,
      "rebalType": "adhoc"
    }
  ],
  "nextId": 2989
}
```

### 响应数据

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	--------	|	-----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|按用户指定sort方向排列	|
|	{ symbol	|	string	|	TRUE	|ETP交易代码	|
|	rebalTime	|	long	|	TRUE	|调仓时间（unix time in millisecond）	|
|	rebalType }	|	string	|	TRUE	|调仓类型（daily, adhoc）	|
|	nextId	|	long	|	FALSE	| 下页查询起始编号（仅在存在下页数据时返回）	|

##### <br>

## 杠杆ETP单个撤单

用户可以通过该接口进行杠杆ETP撤单。

### HTTP 请求

- POST /v2/etp/{transactId}/cancel

API Key 权限：交易<br>限频值：1次/秒<br>

### 请求参数

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	------	|	-----	|
|	transactId	|	long	|	TRUE	| ETP交易ID|



> Response

```json

{
"code": 80042,
"message": "撤单失败，订单不存在"
}

```

### 响应数据

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	--------	|	-----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|



##### <br>

## 杠杆ETP批量撤单

用户可以通过该接口进行杠杆ETP批量撤单。

### HTTP 请求

- POST /v2/etp/batch-cancel

API Key 权限：交易<br>限频值：1次/5秒<br>

### 请求参数

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	------	|	-----	|
|	transactId	|	long	|	TRUE	| ETP交易ID|





> Response

```json
{
    "code":200,
    "data":{
        "success":[
            "5983466"
        ],
        "failed":[
            {
                "errMsg":"撤单失败，订单不存在",
                "transactId":"65445",
                "errCode":80043
            }
        ]
    },
    "message":null
}

```

### 响应数据

|	名称	|	类型	|	是否必需	|	描述	|
|	-----	|	----	|	--------	|	-----	|
|	code	|	integer	|	TRUE	|状态码	|
|	message	|	string	|	FALSE	|错误描述（如有）	|
|	data	|	object	|	TRUE	|	|
|	{ success	|	string	|	TRUE	|ETP撤单成功交易列表	|
|	errMsg	|	long	|	TRUE	|撤单失败错误信息	|
|	errCode 	|	string	|	TRUE	|撤单失败错误码	|
|	transactId}	|	long	|	FALSE	| 交易ID	|

##### <br>


