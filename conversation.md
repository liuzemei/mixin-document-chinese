
## Create Conversation（创建对话）

创建一个 `GROUP`(群聊) 或者 `CONTACT`(联系人) 对话

```
POST  /conversations
```

| 请求体参数      | 介绍                                                         |
| --------------- | ------------------------------------------------------------ |
| category        | `String: 类别，取值为 "GROUP" 或 "CONTACK"`                  |
| conversation_id | `String: 唯一标识，由客户端生成，请注意，如果类别是"CONTACT"，则需要使用"UniqueConversationId"生成。，` |
| participants    | `JSON Array: 包含 action(行为), role(角色), user_id(用户id)` |
| action          | `String: 取值为 "ADD"(添加) "REMOVE"(移除) "JOIN"(加入) "EXIT"(退出) "ROLE"(???)` |
| role            | `String: 为空"" 或者 "ADMIN"(管理员)`                        |
| user_id         | `String: 唯一标识，用户 id`                                  |

> conversation_id: 正常的UUID用于“组”对话，但是唯一的UUID用于“联系人”对话。

请求体参数示例

```json
{
  "category": "GROUP",
  "conversation_id": "928c5c40-769c-3e97-8387-fb1ae0645311",
  "participants": [
    {
      "action": "ADD",
      "role": "",
      "user_id": "e8e5b807-fa8b-455a-8dfa-b189d28310ff"
    }
  ]
}
```

响应示例

```json
{
  "data": {
    "type": "conversation",
    "conversation_id": "928c5c40-769c-3e97-8387-fb1ae0645311",
    "creator_id": "8dcf823d-9eb3-4da2-8734-f0aad50c0da6",
    "category": "GROUP",
    "name": "",
    "icon_url": "",
    "announcement": "",
    "created_at": "2018-05-16T12:34:44.134238105Z",
    "code_id": "d8244b92-30e9-44b5-bfb0-ce597c788125",
    "code_url": "https://mixin.one/codes/d8244b92-30e9-44b5-bfb0-ce597c788125",
    "mute_until": "2018-05-16T12:34:44.143010035Z",
    "participants": [
      {
        "type": "participant",
        "user_id": "8dcf823d-9eb3-4da2-8734-f0aad50c0da6",
        "role": "OWNER",
        "created_at": "2018-05-16T12:34:44.134238105Z"
      },
      {
        "type": "participant",
        "user_id": "e8e5b807-fa8b-455a-8dfa-b189d28310ff",
        "role": "",
        "created_at": "2018-05-16T12:34:44.149277666Z"
      }
    ]
  }
}
```

获取 `UniqueConversationId` 的方法：

```go
func UniqueConversationId(userId, recipientId string) string {
    minId, maxId := userId, recipientId    if strings.Compare(userId, recipientId) > 0 {
      maxId, minId = userId, recipientId
    }
    h := md5.New()
    io.WriteString(h, minId)
    io.WriteString(h, maxId)
    sum := h.Sum(nil)
    sum[6] = (sum[6] & 0x0f) | 0x30
    sum[8] = (sum[8] & 0x3f) | 0x80
    return uuid.FromBytesOrNil(sum).String()
  }
```

## Rotate Conversation（重置会话链接）
使旧的 `code_url` 过期并更改对话的 `code_url` 。
这个 `id` 是 `conversation_id`
```
POST /conversations/:id/rotate
```

| 请求体参数      | 介绍                                                         |
| --------------- | ------------------------------------------------------------ |
| name        | `String: 群聊名称`                  |
| announcement | `String: 群聊公告` |

请求体参数示例(仅支持群聊传参)

```json
{
  "name": "Group 001",
  "announcement": "The description of the conversation"
}
```

响应示例

```json
{
  "data":{
    "type":"conversation",
      "conversation_id":"928c5c40-769c-3e97-8387-fb1ae0645311",
      "creator_id":"8dcf823d-9eb3-4da2-8734-f0aad50c0da6",
      "category":"GROUP",
      "name":"",
      "icon_url":"",
      "announcement":"",
      "created_at":"2018-05-16T12:34:44.134238105Z",
      "code_id":"d8244b92-30e9-44b5-bfb0-ce597c788125",
      "code_url":"https://mixin.one/codes/d8244b92-30e9-44b5-bfb0-ce597c788125",
      "mute_until":"2018-05-16T12:34:44.143010035Z",
      "participants":[
      {
        "type":"participant",
        "user_id":"8dcf823d-9eb3-4da2-8734-f0aad50c0da6",
        "role":"OWNER",
        "created_at":"2018-05-16T12:34:44.134238105Z"
      },
      {
        "type":"participant",
        "user_id":"e8e5b807-fa8b-455a-8dfa-b189d28310ff",
        "role":"",
        "created_at":"2018-05-16T12:34:44.149277666Z"
      }
      ]
  }
}
```

## Update Conversation（更新群聊名称和公告）
更新一个群聊的 名称 和 公告。
```
POST /conversations/:id
```

| 请求体参数      | 介绍                                                         |
| --------------- | ------------------------------------------------------------ |
| name        | `String: 群聊名称`                  |
| announcement | `String: 群聊公告` |

请求体参数示例

```json
{
  "name": "Group 001",
  "announcement": "The description of the conversation"
}
```

响应示例

```json
{
  "data":{
    "type":"conversation",
      "conversation_id":"928c5c40-769c-3e97-8387-fb1ae0645311",
      "creator_id":"8dcf823d-9eb3-4da2-8734-f0aad50c0da6",
      "category":"GROUP",
      "name":"",
      "icon_url":"",
      "announcement":"",
      "created_at":"2018-05-16T12:34:44.134238105Z",
      "code_id":"d8244b92-30e9-44b5-bfb0-ce597c788125",
      "code_url":"https://mixin.one/codes/d8244b92-30e9-44b5-bfb0-ce597c788125",
      "mute_until":"2018-05-16T12:34:44.143010035Z",
      "participants":[
      {
        "type":"participant",
        "user_id":"8dcf823d-9eb3-4da2-8734-f0aad50c0da6",
        "role":"OWNER",
        "created_at":"2018-05-16T12:34:44.134238105Z"
      },
      {
        "type":"participant",
        "user_id":"e8e5b807-fa8b-455a-8dfa-b189d28310ff",
        "role":"",
        "created_at":"2018-05-16T12:34:44.149277666Z"
      }
      ]
  }
}
```

## Read Conversation（获取对话）

通过 `conversation_id` 获取对话内容

```
GET  /conversations/:id
```

请求示例

```
https://api.mixin.one/conversations/928c5c40-769c-3e97-8387-fb1ae0645311
```

响应示例

```json
{
  "data":{
    "type":"conversation",
    "conversation_id":"928c5c40-769c-3e97-8387-fb1ae0645311",
    "creator_id":"8dcf823d-9eb3-4da2-8734-f0aad50c0da6",
    "category":"GROUP",
    "name":"",
    "icon_url":"",
    "announcement":"",
    "created_at":"2018-05-16T12:34:44.134238105Z",
    "code_id":"d8244b92-30e9-44b5-bfb0-ce597c788125",
    "code_url":"https://mixin.one/codes/d8244b92-30e9-44b5-bfb0-ce597c788125",
    "mute_until":"2018-05-16T12:34:44.143010035Z",
    "participants":[
      {
        "type":"participant",
        "user_id":"8dcf823d-9eb3-4da2-8734-f0aad50c0da6",
        "role":"OWNER",
        "created_at":"2018-05-16T12:34:44.134238105Z"
      },
      {
        "type":"participant",
        "user_id":"e8e5b807-fa8b-455a-8dfa-b189d28310ff",
        "role":"",
        "created_at":"2018-05-16T12:34:44.149277666Z"
      }
    ]
  }
}
```

## Participants Actions（参与者行为）
添加，删除或更新对话的参与者。

```
POST /conversations/:id/participants/:action
```

| 请求体参数      | 介绍                                                         |
| --------------- | ------------------------------------------------------------ |
| id        | `String: conversation_id`                  |
| action          | `String: 取值为 "ADD"(添加) "REMOVE"(移除) "JOIN"(加入) "ROLE"` |
| participants    | `JSON Array: 包含 role(角色), user_id(用户id)` |
| role            | `String: 描述（participants）为空"" 或者 "ADMIN"(管理员)`                        |
| user_id         | `String: 描述（participants）唯一标识，用户 id`                                  |

> conversation_id: 正常的UUID用于“组”对话，但是唯一的UUID用于“联系人”对话。

请求示例
```
https://api.mixin.one/conversations/928c5c40-769c-3e97-8387-fb1ae0645311/participants/ADD
```

请求体参数示例

```json
[
  {
    "role": "",
    "user_id": "e8e5b807-fa8b-455a-8dfa-b189d28310ff"
  }
]
```

响应示例

```json
{
  "data":{
    "type":"conversation",
      "conversation_id":"928c5c40-769c-3e97-8387-fb1ae0645311",
      "creator_id":"8dcf823d-9eb3-4da2-8734-f0aad50c0da6",
      "category":"GROUP",
      "name":"",
      "icon_url":"",
      "announcement":"",
      "created_at":"2018-05-16T12:34:44.134238105Z",
      "code_id":"d8244b92-30e9-44b5-bfb0-ce597c788125",
      "code_url":"https://mixin.one/codes/d8244b92-30e9-44b5-bfb0-ce597c788125",
      "mute_until":"2018-05-16T12:34:44.143010035Z",
      "participants":[
      {
        "type":"participant",
        "user_id":"8dcf823d-9eb3-4da2-8734-f0aad50c0da6",
        "role":"OWNER",
        "created_at":"2018-05-16T12:34:44.134238105Z"
      },
      {
        "type":"participant",
        "user_id":"e8e5b807-fa8b-455a-8dfa-b189d28310ff",
        "role":"",
        "created_at":"2018-05-16T12:34:44.149277666Z"
      }
      ]
  }
}
```
