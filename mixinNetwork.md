## Live Exchange Rates （实时汇率）
获取实时汇率

`GET /fiats`

请求示例：
```
https://api.mixin.one/fiats
```

响应示例

```json
{
  "data": [
    {"code":"ISK","rate":121.13998},
    {"code":"CNY","rate":6.9669},
    ...
  ]
}
```
## Top Assets（资产排行）
阅读 Mixin Network 最具价值的资产。

`GET /network/assets/top`

请求示例
```
https://api.mixin.one/network/assets/top
```
这个请求的 header 不用带 Authentication Token

响应示例

```json
{
  "data": {
    "assets": [
      {
        "amount": "134289.9334158",
        "asset_id": "c94ac88f-4671-3976-b60a-09064f1811e8",
        "icon_url": "https://images.mixin.one/E2y0BnTopFK9qey0YI-8xV3M82kudNnTaGw0U5SU065864SsewNUo6fe9kDF1HIzVYhXqzws4lBZnLj1lPsjk-0=s128",
        "symbol": "XIN",
        "type": "asset"
      },
      ....
    ]
  }
}
```
## Network Asset（主网资产）
通过 asset_id 从 Mixin Network 读取公共资产信息。

`GET /network/assets/:id`

请求示例
```
https://api.mixin.one/network/assets/c94ac88f-4671-3976-b60a-09064f1811e8
```
响应示例

```json
{
  "data": {
    "amount": "296369.17400899",
    "asset_id": "c94ac88f-4671-3976-b60a-09064f1811e8",
    "chain_id": "43d61dcd-e413-450d-80b8-101d5e903357",
    "icon_url": "https://images.mixin.one/UasWtBZO0TZyLTLCFQjvE_UYekjC7eHCuT_9_52ZpzmCC-X-NPioVegng7Hfx0XmIUavZgz5UL-HIgPCBECc-Ws=s128",
    "name": "Mixin",
    "snapshots_count": 35224199,
    "symbol": "XIN",
    "type": "asset"
  }
}
```
## Network Snapshots（主网快照集合）
读取 Mixin Network 的公共快照。因为您需要在头文件中添加一个授权令牌来获取私有信息，例如:user_id、trace_id等。

`GET /network/snapshots`

|请求(体)参数|	介绍|
| - | - |
|limit|	Integer: 最大为500|
|offset|	String: 格式为 RFC3339Nano 或者 UTC 或者 non UTC 的时间格式|
|asset|	String: [选填]（唯一标识）返回所有的网络快照或者指定的资产快照|
|order|	String: [选填]ASC 或者 DESC ，默认为 DESC|
|offset| 例子：`2006-01-02T15:04:05.999999999Z` *或* `2006-01-02T15:04:05.999999999%2B07:00` *或* `2006-01-02T15:04:05.999999999-07:00` |


请求示例
```
https://api.mixin.one/network/snapshots?limit=10&offset=2018-05-29T16:30:24.845515732%2B08:00
```
响应示例

```json
{
  "data": [
    {
      "amount": "-1688168",
      "asset": {
        "asset_id": "965e5c6e-434c-3fa9-b780-c50f43cd955c",
        "chain_id": "43d61dcd-e413-450d-80b8-101d5e903357",
        "icon_url": "https://images.mixin.one/0sQY63dDMkWTURkJVjowWY6Le4ICjAFuu3ANVyZA4uI3UdkbuOT5fjJUT82ArNYmZvVcxDXyNjxoOv0TAYbQTNKS=s128",
        "name": "Chui Niu Bi",
        "symbol": "CNB",
        "type": "asset"
      },
      "created_at": "2018-05-29T09:31:04.202186212Z",
      "data": "",
      "snapshot_id": "529934b0-abfd-43ab-9431-1805773000a4",
      "source": "TRANSFER_INITIALIZED",
      "type": "snapshot",
      // 仅对具有访问权限的用户(或应用程序)提供选项。
      "user_id": "06aed1e3-bd77-4a59-991a-5bb5ae6fbb09",
      "trace_id": "7c67e8e8-b142-488b-80a3-61d4d29c90bf",
      "opponent_id": "a465ffdb-4441-4cb9-8b45-00cf79dfbc46",
      "data": "Transfer!"
    },
  ...
  ]
}
```
## Network Snapshot（主网快照记录）
通过 snapshot_id 读取 Mixin Network 的公共快照。

`GET /network/snapshots/:id`

请求示例
```
https://api.mixin.one/network/snapshots/8f5b244e-cf86-4374-8eaa-c551fd70cd83
```
响应示例

```json
{
  "data": {
    "amount": "-1688168",
    "asset": {
      "asset_id": "965e5c6e-434c-3fa9-b780-c50f43cd955c",
      "chain_id": "43d61dcd-e413-450d-80b8-101d5e903357",
      "icon_url": "https://images.mixin.one/0sQY63dDMkWTURkJVjowWY6Le4ICjAFuu3ANVyZA4uI3UdkbuOT5fjJUT82ArNYmZvVcxDXyNjxoOv0TAYbQTNKS=s128",
      "name": "Chui Niu Bi",
      "symbol": "CNB",
      "type": "asset"
    },
    "created_at": "2018-05-29T09:31:04.202186212Z",
    "data": "",
    "snapshot_id": "529934b0-abfd-43ab-9431-1805773000a4",
    // 包含 DEPOSIT_CONFIRMED, TRANSFER_INITIALIZED, WITHDRAWAL_INITIALIZED, WITHDRAWAL_FEE_CHARGED, WITHDRAWAL_FAILED 
    "source": "TRANSFER_INITIALIZED",
    "type": "snapshot",
    // 仅对具有访问权限的用户(或应用程序)提供选项。
    "user_id": "06aed1e3-bd77-4a59-991a-5bb5ae6fbb09",
    "trace_id": "7c67e8e8-b142-488b-80a3-61d4d29c90bf",
    "opponent_id": "a465ffdb-4441-4cb9-8b45-00cf79dfbc46",
    "data": "Transfer!"
  }
}
```
## External Transactions（其他区块信息）
按指定地址、标记和资产id读取外部事务(未决存款)

`GET /external/transactions`

header 不需要带 Token

|请求体参数|	介绍|
| - | - |
|destination|	String: BTC 地址( ETH 地址/或者 EOS 账户名...)|
|tag|	String:[选填] 可以为空，EOS 账户的 tag 或 memo |
|limit|	Integer:[选填]最大为 500|
|offset|	String:[选填]同上的 offset(Network Snapshot)|
|asset|	String:[选填] asset_id 唯一标识|

请求示例

```json
https://api.mixin.one/external/transactions?asset=43d61dcd-e413-450d-80b8-101d5e903357&destination=1AK4LYE6PYwBmSYHQX3v2UsXXHTvCAsJeK
```
响应示例

```json
{
  "data":[{
    "type":"transaction",
    "transaction_id":"ab56be4c-5b20-41c6-a9c3-244f9a433f35",
    "transaction_hash":"axt..ze",
    "sender":"137FkAtj1KcVKKt4tPeP1Djz3Nvc5DEYri",
    "amount":"10.0",
    "destination":"1AK4LYE6PYwBmSYHQX3v2UsXXHTvCAsJeK",
    "tag":"",
    "asset_id":"43d61dcd-e413-450d-80b8-101d5e903357",
    "chain_id":"43d61dcd-e413-450d-80b8-101d5e903357",
    "confirmations":1,
    "threshold":12,
    "created_at":"2018-05-03T10:08:34.859542588Z"
  },
    ...
  ]
}
```
## Search Assets（查询代币信息）
搜索资产的符号或代币名称，市场有一定流通量的代币。

`GET /network/assets/search/:symbol`

请求示例
```
https://api.mixin.one/network/assets/search/eos
```
响应示例

```json
{
  "data":[{
    "type":"asset",
      "asset_id":"3596ab64-a575-39ad-964e-43b37f44e8cb",
      "chain_id":"43d61dcd-e413-450d-80b8-101d5e903357",
      "symbol":"EOS",
      "name":"eos",
      "icon_url":"https://images.mixin.one/HovctUnrBkLPlDotWvWPsIuFb8qKrLddwF5-f2Fi9q9uO829YB2qGITgOd2YmTMKnGg_z9XrVYzEwFE_rD_REz9C=s128",
      "balance":"203.975",
      "destination":"0x2CEab41716F4ce0Db36B6FdABEdc6a0BE5DC442B",
      "tag": "",
      "price_btc":"0",
      "price_usd":"0"
      "change_btc": "1",
      "change_usd": "2",
      "asset_key": "",
      "confirmations": 10,
      "capitalization": 1000.3
  },
  ...
  ]
}
```