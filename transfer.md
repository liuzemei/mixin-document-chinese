
## Deposit（存款）
查看资产的存款地址。api与Read Asset相同

`GET /assets/:id`

请求示例：
```
https://api.mixin.one/assets/3596ab64-a575-39ad-964e-43b37f44e8cb
```
响应示例：

```json
{
  "data":{
    "type":"asset",
      "asset_id":"3596ab64-a575-39ad-964e-43b37f44e8cb",
      "chain_id":"43d61dcd-e413-450d-80b8-101d5e903357",
      "symbol":"eosDAC",
      "name":"eosDAC Community Owned EOS Block Producer ERC20 Tokens",
      "icon_url":"https://images.mixin.one/HovctUnrBkLPlDotWvWPsIuFb8qKrLddwF5-f2Fi9q9uO829YB2qGITgOd2YmTMKnGg_z9XrVYzEwFE_rD_REz9C=s128",
      "balance":"203.975",
      "destination":"0x2CEab41716F4ce0Db36B6FdABEdc6a0BE5DC442B",
      "tag":"",
      "price_btc":"0",
      "price_usd":"0",
      "change_btc": "1",
      "change_usd": "2",
      "asset_key": "",
      "confirmations": 10,
      "capitalization": 1000.3
  }
}
```
这个 id 就是指创建出来 app 的 user-id点击这里然后往上划拉图中的 User Id

## Withdrawal（提款）
将资产从Mixin网络中取出，需要创建一个提现地址。

`POST /withdrawals`

|请求体参数|	介绍|
| - | - |
|address_id|	String:创建地址时产生的唯一标识|
|amount|	String:提款的数量|
|pin|	String:加密 PIN|
|trace_id|	String: 每笔交易的id（唯一标识）|
|memo|	String:备注，少于 140 个字节|
请求体示例：

```json
{
  "address_id": "43d61dcd-e413-450d-80b8-101d5e903357",
  "amount": "100",
  "pin": "xDcSiAsvsekYpnxEShqLgecvQ4GhP7o660nOodK9BG7k+xsszxO56Yg6DQLWtOek",
  "trace_id": "ca90fd5b-e047-4a66-affa-2b40f026b165",
  "memo": "hello"
}
```
响应示例

```json
{
  "data":{
    "type":"withdrawal",
    "snapshot_id":"ab56be4c-5b20-41c6-a9c3-244f9a433f35",
    "transaction_hash":"axt..ze",
    "asset_id":"43d61dcd-e413-450d-80b8-101d5e903357",
    "amount":"-10",
    "trace_id":"7c67e8e8-b142-488b-80a3-61d4d29c90bf",
    "memo":"hello",
    "created_at":"2018-05-03T10:08:34.859542588Z"
  }
}
```

## Verify Payment（确认交易）
验证一笔交易，付款状态：是paid已支付或pending未决。

`POST /payments`

| 请求体参数 |	介绍|
| - | - |
|asset_id|	String: 资产 id（唯一标识）|
|opponent_id|	String: 交易接收方的 user_id（唯一标识）|
|amount|	String: 转入数量|
|trace_id|	String: 每笔交易的id（唯一标识）|
请求体示例

```json
{
  "asset_id": "43d61dcd-e413-450d-80b8-101d5e903357",
  "opponent_id": "a465ffdb-4441-4cb9-8b45-00cf79dfbc46",
  "amount": "10",
  "trace_id": "99f1f10f-81a0-4887-907f-c5b37f2c1bc8"
}
```
响应示例

```json
{
  "data": {
    "recipient": {
      "type": "user",
      "user_id": "a465ffdb-4441-4cb9-8b45-00cf79dfbc46",
      "identity_number": "20018",
      "full_name": "OS105",
      "avatar_url": "",
      "relationship": "",
      "mute_until": "0001-01-01T00:00:00Z",
      "created_at": "2018-04-25T05:37:10.06433488Z",
      "is_verified": false
    },
    "asset": {
      "type": "asset",
      "asset_id": "43d61dcd-e413-450d-80b8-101d5e903357",
      "chain_id": "43d61dcd-e413-450d-80b8-101d5e903357",
      "symbol": "EOS",
      "name": "EOS",
      "icon_url": "https://images.mixin.one/zVDjOxNTQvVsA8h2B4ZVxuHoCF3DJszufYKWpd9duXUSbSapoZadC7_13cnWBqg0EmwmRcKGbJaUpA8wFfpgZA=s128",
      "balance": "0",
      "destination": "",
      "tag": "",
      "price_btc": "0.0776679",
      "price_usd": "715.394"
    },
    "amount": "10",
    "status": "pending" // "paid" OR "pending"
  }
}
```
## Transfer（交易）
在 Mixin Network 用户之间转移资产。

`POST /transfers`

|请求体参数|	介绍|
| - | - |
|amount|	String: 转移的数量|
|asset_id|	String: 转移资产的 id（唯一标识）|
|opponent_id|	String: 收款人的 userId|
|memo|	String: 交易备注，140 字节以内|
|pin|	String: 加密 PIN 码|
|trace_id|	String: 每笔交易的id（唯一标识）|
请求体参数示例

```json
{
  "amount": "10",
  "asset_id": "43d61dcd-e413-450d-80b8-101d5e903357",
  "opponent_id": "a465ffdb-4441-4cb9-8b45-00cf79dfbc46",
  "memo": "hello",
  "pin": "F39IsJmUaZW03VMV/01lHyY2RCoZ7/X764akX+EmthIc4uVsWAWQTM/IxX5Z9C1y",
  "trace_id": "7c67e8e8-b142-488b-80a3-61d4d29c90bf"
}
```
响应示例

```json
{
  "data": {
    "type": "transfer",
    "snapshot_id": "ab56be4c-5b20-41c6-a9c3-244f9a433f35",
    "opponent_id": "a465ffdb-4441-4cb9-8b45-00cf79dfbc46",
    "asset_id": "43d61dcd-e413-450d-80b8-101d5e903357",
    "amount": "-10",
    "trace_id": "7c67e8e8-b142-488b-80a3-61d4d29c90bf",
    "memo": "hello",
    "created_at": "2018-05-03T10:08:34.859542588Z"
  }
}
```
## Read Transfer（读取交易）
通过查询 trace_id 读取交易记录详情。

`GET /transfers/trace/:id`

请求示例
```
https://api.mixin.one/transfers/trace/7c67e8e8-b142-488b-80a3-61d4d29c90bf
```
响应示例

```json
{
  "data": {
    "type": "transfer",
    "snapshot_id": "ab56be4c-5b20-41c6-a9c3-244f9a433f35",
    "opponent_id": "a465ffdb-4441-4cb9-8b45-00cf79dfbc46",
    "asset_id": "43d61dcd-e413-450d-80b8-101d5e903357",
    "amount": "-10",
    "trace_id": "7c67e8e8-b142-488b-80a3-61d4d29c90bf",
    "memo": "hello",
    "created_at": "2018-05-03T10:08:34.859542588Z"
  }
}
```