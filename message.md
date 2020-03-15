
## Create Attachment（添加附件）

创建一个附件上传地址。我们使用s3作为存储，您可以使用HTTP POST跟随s3基于浏览器的上传。[https://docs.aws.amazon.com/AmazonS3/latest/API/sigv4-post-example.html](https://docs.aws.amazon.com/AmazonS3/latest/API/sigv4-post-example.html.)


```
POST  /attachments
```

响应示例：

```json
{
  "data": {
    "type": "attachment",
    "attachment_id": "7a54e394-1626-4cd4-b967-543932c2a032",
    "upload_url": "https://moments-shou-tv.s3.amazonaws.com/mixin/attachments/1526305123-de9892550143c713c45f6265c9e61959ebfac6cc8de4badf5c0489636796ad8a?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAJW6D5Q3Z5WYA2KRQ%2F20180514%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20180514T133843Z&X-Amz-Expires=21600&X-Amz-SignedHeaders=content-type%3Bhost%3Bx-amz-acl&X-Amz-Signature=591fb0a1057109d45e26a8e4e9e61599e302818ab2e7aa706826a2b838a089e3",
    "view_url": "https://moments.shou.tv/mixin/attachments/1526305123-de9892550143c713c45f6265c9e61959ebfac6cc8de4badf5c0489636796ad8a"
  }
}
```
> 直接根据响应的 `upload_url` 上传文件即可。

## Create Acknowledgements（创建确认消息）
通过HTTP创建简单的确认消息。 最大数组大小为100。

```
POST  /acknowledgements
```

| 请求体参数        | 介绍                          |
| ----------------- | ----------------------------- |
| message_id        | `String: 消息 id`             |
| status  | `String: 值为 "READ"`         |

请求体参数示例

```json
[
  {
    "message_id": "e8e5b807-fa8b-455a-8dfa-b189d28310ff",
    "status": "READ"
  }
]
```

响应结果为一个空对象

```js
{}
```

## Create Messages（创建消息）

通过HTTP创建纯消息，仅供bot使用。最多发送 100 条消息，即数组长度最大为 100。

```
POST  /messages
```

| 请求体参数        | 介绍                          |
| ----------------- | ----------------------------- |
| conversation_id   | `String: 对话 id（唯一标识）` |
| recipient_id      | `String: 收件人的 user_id`    |
| message_id        | `String: 消息 id`             |
| category          | `String: 请求格式类别`        |
| data              | `String: base64 之后的消息`   |
| representative_id | `String: 代表 id`             |
| quote_message_id  | `String: 引用消息 id`         |
> 1. recipient_id: 即接收人的 user_id
> 2. message_id: 是这个消息的唯一标识的 uuid
> 3. representative_id: 这个消息是谁发送的。相当于发送人的 user_id
> 4. quote_message_id: 引用消息的 message_id，相当于长按消息后点击回复，那条消息的 message_id 就是这个字段。

请求体参数示例

```json
[
  {
    "conversation_id": "928c5c40-769c-3e97-8387-fb1ae0645311",
    "recipient_id": "2a4969f3-6afd-425a-8b9e-ff012e988863",
    "message_id": "e8e5b807-fa8b-455a-8dfa-b189d28310ff",
    "category": "PLAIN_TEXT",
    "data": "base64 of data",
    "representative_id": "f9906f66-2f4c-405c-9a18-d30d32811397",
    "quote_message_id": "b3b71bfe-0722-4da3-8a10-efda24d59934"
  }
]
```

响应结果为一个空对象

```js
{}
```
