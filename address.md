
## Create Address（创建地址）
创建一个提现地址，您只能通过现有的地址提现。

`POST /addresses`

|请求体参数|	介绍|
| - | - |
|asset_id|	String:UUID(资产唯一识别码)|
|destination|	String: BTC 地址( ETH 地址/或者 EOS 账户名...)|
|tag|	String: 可以为空，EOS 账户的 tag 或 memo |
|label|	String:不能为空，可以为 Mixin 或者其他描述 最多 64 位|
|pin|	String: PIN加密|
请求体参数示例

```json
{
  "asset_id": "43d61dcd-e413-450d-80b8-101d5e903357",
  "label": "Jason ETH Address",
  "pin": "nRF5OyFmO4REG6lcPk1jwKDJrENim791uLe+HH0g7EwQHXK9FgCMJl5RDKbeCNDW",
  "destination": "0x86fa049857e0209aa7d9e616f7eb3b3b78ecfdb0",
  "tag": ""
}
```
响应示例

```json
{
  "data":{
    "type":"address",
    "address_id":"e1524f3c-2e4f-411f-8a06-b5e1b1601308",
    "asset_id":"43d61dcd-e413-450d-80b8-101d5e903357",
    "destination":"0x86Fa049857E0209aa7D9e616F7eb3b3B78ECfdb0",
    "tag": "",
    "label":"Eth Address",
    "fee":"0.016",
    "reserve":"0",
    "dust":"0.0001",
    "updated_at":"2018-07-10T03:58:17.5559296Z"
  }
}
```
## Delete Address（删除地址）
通过 address_id 删除一个提现地址

`POST /addresses/:id/delete`

请求示例：(POST)
```
/addresses/ba3a2e33-efde-40b9-9cac-c293f0d1a3f2/delete
```
请求体示例：

```json
{"pin":"d2EJy5kmt56d3U5PeKm+TJLBnXBuyxBTcWxytL8pk/LXwJEak9r8iVMcASjgvoO+"}
```
响应为一个空对象

```json
{}
```
## Read Address（获取地址所有信息）
通过 address_id 读取地址所有信息

`GET /addresses/:id`

请求示例
```
https://api.mixin.one/addresses/e1524f3c-2e4f-411f-8a06-b5e1b1601308
```
响应示例

```json
{
  "data":{
    "type":"address",
    "address_id":"e1524f3c-2e4f-411f-8a06-b5e1b1601308",
    "asset_id":"43d61dcd-e413-450d-80b8-101d5e903357",
    "destination":"0x86Fa049857E0209aa7D9e616F7eb3b3B78ECfdb0",
    "tag": "",
    "label":"Eth Address",
    "fee":"0.016",
    "reserve":"0",
    "dust":"0.0001",
    "updated_at":"2018-07-10T03:58:17.5559296Z"
  }
}
```

## Addresses by Asset（资产账户集合）
根据 asset_id 读取所有的拥有该资产的地址(账户)。

`GET /assets/:id/addresses`

请求示例

```
https://api.mixin.one/assets/43d61dcd-e413-450d-80b8-101d5e903357/addresses
```
响应示例

```json
{
  "data":[ // 这里是一个数组
    {
      "type":"address",
      "address_id":"e1524f3c-2e4f-411f-8a06-b5e1b1601308",
      "asset_id":"43d61dcd-e413-450d-80b8-101d5e903357",
      "destination":"0x86Fa049857E0209aa7D9e616F7eb3b3B78ECfdb0",
      "tag": "",
      "label":"Eth Address",
      "fee":"0.016",
      "reserve":"0",
      "dust": "0.0001",
      "updated_at":"0001-01-01T00:00:00Z"
    },
    ...
  ]
}
```