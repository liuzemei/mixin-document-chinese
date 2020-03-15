
## Read Profile (获取自己信息)

获取自己的基本信息

```
GET  /me
```

请求示例

```
https://api.mixin.one/me
```

响应示例

```json{
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

## Update Perference（更新偏好）

更新用户的偏好

```
POST  /me/preferences
```

| 请求体参数                 | 介绍                                                         |
| -------------------------- | ------------------------------------------------------------ |
| receive_message_source     | `String: 接受所有人信息或者联系人信息， 值为： “EVERYBODY”(所有人) 或 “CONTACTS”(联系人)` |
| accept_conversation_source | `String:“EVERYBODY” 或 “CONTACTS”`                           |

> 前者是谁可以给我发消息，后者是谁可以拉我入群。

请求体示例

```json
{  
  "receive_message_source": "CONTACTS", 
  "accept_conversation_source": "CONTACTS"
}
```

## Update Profile(更新个人信息)

更新个人基本信息

```
POST  /me
```

| 请求体参数    | 介绍                                                         |
| ------------- | ------------------------------------------------------------ |
| full_name     | `String: 个人昵称`                                           |
| avatar_base64 | `String: Base64 格式的图片， 可以为空， 图片大小要大于 1024 字节` |

请求体示例：

```json
{  
  "avatar_base64": "" ,  
  "full_name": "Around World"
}
```

响应示例

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

## Read User List（获取多个用户基本信息）

通过id获取多个用户信息。

```
POST  /users/fetch
```

请求体格式为一个数组

请求体示例

```json
["06aed1e3-bd77-4a59-991a-5bb5ae6fbb09","06aed1e3-bd77-4a59-991a-5bb5ae6fbb10",...]
```

> 注意，这里放的是 user_id 的一个`String数组`

响应示例

```json
{
  "data":[{
      "type":"user",
      "user_id":"773e5e77-4107-45c2-b648-8fc722ed77f5",
      "identity_number":"7000",
      "phone":"+8613801380138",
      "full_name":"Team Mixin",
      "biography":"",
      "avatar_url":"https://images.mixin.one/E2y0BnTopFK9qey0YI-8xV3M82kudNnTaGw0U5SU065864SsewNUo6fe9kDF1HIzVYhXqzws4lBZnLj1lPsjk-0=s256",
      "relationship":"STRANGER",
      "mute_until":"0001-01-01T00:00:00Z",
      "created_at":"2017-12-23T18:23:26.996149Z",
      "is_verified":true
  },
  ...
  ]
}
```

## Read User （获取用户基本信息）

通过 `user_id` 获取用户信息

```
GET /users/:id
```

请求示例

```
https://api.mixin.one/users/06aed1e3-bd77-4a59-991a-5bb5ae6fbb09
```

响应示例

```json
{
  "data": {
    "type": "user",
    "user_id": "773e5e77-4107-45c2-b648-8fc722ed77f5",
    "identity_number": "7000",
    "phone": "+8613801380138",
    "full_name": "Team Mixin",
    "biography": "",
    "avatar_url": "https://images.mixin.one/E2y0BnTopFK9qey0YI-8xV3M82kudNnTaGw0U5SU065864SsewNUo6fe9kDF1HIzVYhXqzws4lBZnLj1lPsjk-0=s256",
    "relationship": "STRANGER",
    "mute_until": "0001-01-01T00:00:00Z",
    "created_at": "2017-12-23T18:23:26.996149Z",
    "is_verified": true
  }
}
```

## Search User （查找用户）

根据 `identity_number` 搜索用户，获取用户基本信息，这是一个有请求限制的api。

```
GET  /search/:q
```

| 请求参数 | 介绍                               |
| -------- | ---------------------------------- |
| q        | `String: Mixin ID 或者是 电话号码` |

请求示例：

```
https://api.mixin.one/search/7000
```

响应示例

```json
{
  "data":{
      "type":"user",
      "user_id":"773e5e77-4107-45c2-b648-8fc722ed77f5",
      "identity_number":"7000",
      "phone":"+8613801380138",
      "full_name":"Team Mixin",
      "biography":"",
      "avatar_url":"https://images.mixin.one/E2y0BnTopFK9qey0YI-8xV3M82kudNnTaGw0U5SU065864SsewNUo6fe9kDF1HIzVYhXqzws4lBZnLj1lPsjk-0=s256",
      "relationship":"STRANGER",
      "mute_until":"0001-01-01T00:00:00Z",
      "created_at":"2017-12-23T18:23:26.996149Z",
      "is_verified":true
  }
}
```

## Rotate User’s QR（重置二维码）

重置用户的code_id。

> 重置之后 以前用户的二维码 和 code_id 会失效。

```
GET  /me/code
```

请求示例

```
https://api.mixin.one/me/code
```

响应示例

```json
{
  "data": {
    "type": "user",
    "user_id": "06aed1e3-bd77-4a59-991a-5bb5ae6fbb09",
    "identity_number": "7000",
    "phone": "+8613801380138",
    "full_name": "Around World",
    "biography": "",
    "avatar_url": "",
    "relationship": "ME",
    "mute_until": "0001-01-01T00:00:00Z",
    "created_at": "2018-05-03T06:03:56.867971412Z",
    "is_verified": false,
    "session_id": "a34c07a9-755d-4b54-94c5-e45e9a2dd43e",
    "pin_token": "",
    "code_id": "dabcf1c2-6a5e-4ea3-ad51-6e6641a06c7c",
    "code_url": "https://mixin.one/codes/dabcf1c2-6a5e-4ea3-ad51-6e6641a06c7c",
    "has_pin": true,
    "has_emergency_contact": true,
    "receive_message_source": "CONTACTS",
    "accept_conversation_source": "CONTACTS",
    "fiat_currency": "USD",
    "transfer_notification_threshold": 0
  }
}
```

## Friends（获取好友列表）

获取用户的好友列表

```
GET  /friends
```

请求示例

```
https://api.mixin.one/friends
```

响应示例

```json
{
  "data": [
    {
      "type": "user",
      "user_id": "773e5e77-4107-45c2-b648-8fc722ed77f5",
      "identity_number": "7000",
      "phone": "+8613801380138",
      "full_name": "Team Mixin",
      "biography": "",
      "avatar_url": "https://images.mixin.one/E2y0BnTopFK9qey0YI-8xV3M82kudNnTaGw0U5SU065864SsewNUo6fe9kDF1HIzVYhXqzws4lBZnLj1lPsjk-0=s256",
      "relationship": "STRANGER",
      "mute_until": "0001-01-01T00:00:00Z",
      "created_at": "2017-12-23T18:23:26.996149Z",
      "is_verified": true
    },
  ...
  ]
}
```

## APP User（创建用户）
创建一个新的 Mixin Network 用户(就像普通的 Mixin Messenger 用户一样)。您应该保留PrivateKey，它用于为用户签署身份验证令牌和加密的PIN。

`POST /users`

|请求体参数|	介绍|
| - | - |
|full_name|	String: 用户名称|
|session_secret|	String: RSA 公钥的 Base64|
请求体示例

```json
{
  "full_name": "Bot User",
  "session_secret": "MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDMTuli9K9k7F+L7Rq34se23nQeV2yvjVGCZyRTbp8qNASnRq6N679ZflgVxNUsr2qkHN4eqvafrQ9IIcRXfofMlWWIU6MrgVVD0UEVyH4jKA5gUr4smU/SDnVLqb3TojYMELIKHgqnrjqDJ0b+vMUG1Iix4fi+CvjSiJzsWPOavQIDAQAB"
}
```
响应示例

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
