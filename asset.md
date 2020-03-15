
## Read Asset（获取资产详情）
通过 asset_id 获取该资产的详细信息。

`GET /assets/:id`

请求示例
```
https://api.mixin.one/assets/3596ab64-a575-39ad-964e-43b37f44e8cb
```
响应示例

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
    "tag": "",
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
## Read Asset List（获取资产集合）
读取用户的所有资产。存款地址可能在这个api中不返回，使用/assets/:id来获取存款地址。

`GET /assets`

请求示例
```
https://api.mixin.one/assets
```
响应示例

```json
{
  "data":[
    {
      "type":"asset",
      "asset_id":"3596ab64-a575-39ad-964e-43b37f44e8cb",
      "chain_id":"43d61dcd-e413-450d-80b8-101d5e903357",
      "symbol":"eosDAC",
      "name":"eosDAC Community Owned EOS Block Producer ERC20 Tokens",
      "icon_url":"https://images.mixin.one/HovctUnrBkLPlDotWvWPsIuFb8qKrLddwF5-f2Fi9q9uO829YB2qGITgOd2YmTMKnGg_z9XrVYzEwFE_rD_REz9C=s128",
      "balance":"203.975",
      "destination":"0x2CEab41716F4ce0Db36B6FdABEdc6a0BE5DC442B",
      "tag": "",
      "label": "",
      "price_btc":"0",
      "price_usd":"0",
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

## Read Asset Fee（获取资产提现手续费）
读取用户的所有资产。存款地址可能在这个api中不返回，使用/assets/:id来获取存款地址。

`GET /assets`

请求示例
```
https://api.mixin.one/assets/3596ab64-a575-39ad-964e-43b37f44e8cb/fee
```
响应示例

```json
{  
  "data":{
    "type": "fee",
    "asset_id": "43d61dcd-e413-450d-80b8-101d5e903357",
    "amount":   "0.01",
  }
}
```
