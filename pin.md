
## Create & Update PIN（创建或更新 PIN）
PIN用于管理用户的地址、资产等。Mixin网络用户没有默认密码(APP除外)。

`POST /pin/update`

|请求体参数|	介绍|
| - | -|
|old_pin|	String: 老加密 PIN 码 或 为空字符串|
|pin|	String: 新的加密 PIN 码|

```json
{
  "old_pin":"",
  "pin":"+mRm5rm9bkQztvpsaTyz1Rib0BEM0S1FKl/oYaMfbUJM3ZmrxJhafj/tjHi+3kwQ"
}
```
> 1. 请求头要包含 Authorization ，其值为上文介绍的 Authentication Token
> 2. 也就是说，在进行任何请求之前，都需要先生成认证令牌(每次请求前，需要通过uid、sid、privateKey、method、url、body来动态生成)

响应信息
```json
{
  "data":{
    "type":"user",
    "user_id":"06aed1e3-bd77-4a59-991a-5bb5ae6fbb09",
    "identity_number":"7000",
    "phone":"+8613801380138",
    "full_name":"Around World",
    "biography":"",
    "avatar_url":"",
    "relationship":"ME",
    "mute_until":"0001-01-01T00:00:00Z",
    "created_at":"2018-05-03T06:03:56.867971412Z",
    "is_verified":false,
    "session_id":"a34c07a9-755d-4b54-94c5-e45e9a2dd43e",
    "pin_token":"",
    "code_id":"dabcf1c2-6a5e-4ea3-ad51-6e6641a06c7c",
    "code_url":"https://mixin.one/codes/dabcf1c2-6a5e-4ea3-ad51-6e6641a06c7c",
    "has_pin":true,
    "has_emergency_contact":true,
    "receive_message_source":"CONTACTS",
    "accept_conversation_source":"CONTACTS",
    "fiat_currency":"USD",
    "transfer_notification_threshold":0
  }
}
```
## Verify PIN（验证PIN）
验证PIN是否有效。例如，您可以在更新PIN之前验证它。

`POST /pin/verify`

|请求体参数|	介绍|
| - | - |
|pin|	String: 加密 PIN 码|

请求体示例：
```json
{
  "pin":"rIqULBd+xaiLuKImKAI7r72azK0zMPy7dIw1fQfhYskWKxkObZvOv5E6A8bACaws"}
```
响应示例：

```json
{
  "data":{
    "type":"user",
    "user_id":"06aed1e3-bd77-4a59-991a-5bb5ae6fbb09",
    "identity_number":"7000",
    "phone":"+8613801380138",
    "full_name":"Around World",
    "biography":"",
    "avatar_url":"",
    "relationship":"ME",
    "mute_until":"0001-01-01T00:00:00Z",
    "created_at":"2018-05-03T06:03:56.867971412Z",
    "is_verified":false,
    "session_id":"a34c07a9-755d-4b54-94c5-e45e9a2dd43e",
    "pin_token":"",
    "code_id":"dabcf1c2-6a5e-4ea3-ad51-6e6641a06c7c",
    "code_url":"https://mixin.one/codes/dabcf1c2-6a5e-4ea3-ad51-6e6641a06c7c",
    "has_pin":true,
    "has_emergency_contact":true,
    "receive_message_source":"CONTACTS",
    "accept_conversation_source":"CONTACTS",
    "fiat_currency":"USD",
    "transfer_notification_threshold":0
  }
}
```