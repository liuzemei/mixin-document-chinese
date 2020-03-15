
## Oauth Scopes (OAuth的范围)

Mixin允许开发人员使用OAuth获得对用户某些信息的授权访问。

| 范围          | 介绍                                                     |
| ------------- | -------------------------------------------------------- |
| PROFILE:READ  | 授予对用户信息的读访问权，包括Mixin ID、名称和用户头像。 |
| PHONE:READ    | 授予读取用户电话号码的访问权。                           |
| CONTACTS:READ | 授予对读好友、联系人和blocking_users的访问权限。         |
| ASSETS:READ   | 授予对读取用户资产列表、余额的访问权。     |
| SNAPSHOTS:READ   | 授予对读取用户交易历史记录的访问权。     |

请求示例

```
https://mixin.one/oauth/authorize?client_id=CLIENT_ID&scope=PROFILE:READ+ASSETS:READ&response_type=code
```

> 参数 client_id 来源, 来自于 创建 app 时生成的那个 json 文件里。


## Register APP （注册 APP）
你必须注册一个应用程序才能使用Mixin网络，所以你需要访问 https://developers.mixin.one 得到以下信息。

下面是一个参数示例。

> [创建一个](https://developers.mixin.one/dashboard) 基于 Mixin Network 的应用开发Dapp。

注册一个应用程序后，你可以得到以下信息，所有信息都将在以后使用。
```
ClientId        = "89e0bdee-c355-47f2-945a-be48be875606"
ClientSecret    = "2d9c60d4b4dd2185d2938229ac76fea2b69440fbff4608cbbf80b32a5a598368"
PinCode = "948159"
SessionId       = "c09cf313-7ded-425d-ad3f-a1ce4cfd5e5e"
PinToken        = "GSusC2myf/meJJnqorrcg2EWnHEAFXoT4so36ggrM4WSRGXFGtPDo3CZCQhldMpFc84MdvdS94tZ4na+0NUWIkkXOMSLFfubf6PNS2DrlC+xjQWjWYN1Py8Y0SDyP1AjQe5+7iXrCoiyrBOxatov5UbRFrTJDX9Jgqh9fTFJfR4="
PrivateKey      = `-----BEGIN RSA PRIVATE KEY-----
MIICXAIBAAKBgQCKUnJ8IEiGci7Gu+oKoy6I1wy0H3f2BwHBcSSVy5sglDHHTlBA
Czg6HcNuy5PXfdrulpz0tr4Prn5x5upUH6CrL8dAT6oUB3V72f0gqSWde90APlsH
ZVSYFaq6PxqZ2HJg40aXAvHiuGbqwmN5LZiDdR0uewTDZjUo1rijqPb2fwIDAQAB
AoGACReqVuZ4Xf4bfQzVMaXQZUZdm2mGJTIIt4KMeRxNMjMLoqJPPCaAp7FVK29O
ZJftUEmuP5fTnoxF247mUGlT0lQtIv3E5sSFTpzwYu8No9+Whpr4/rYgJ4OBpAE/
i3lTPwKXnHvkTDcrlCc8rGdN4oVmnFVwOM5tUBZtBKKLh2ECQQDCSYiWJ0nQul9e
pVn4yv0s3ur/VHoLqNvqV38vpieiV9cVwSpuXN3evSDb9k0CC/Qmn7PXfKN7zLhX
z/t2rzDbAkEAtkIa6NGsasg8b/4r+zHOWU8B51bLNC6b3NEAakgxB9Qo82Wgqmdf
64C1DZjuIee6InLq1DoGzM68z+XcRzAgLQJAGKTtL2ayZUiOulmtDPLqpFtuYY7c
oEf+BT6uAmRIGL6dqMPE1xTui8dfuKcIY58SjCerz0SfFCAGrhTSp95XCwJAQR1A
6+jtBoFfRkuyft3+cN3POk1B7/Su7qck1NPR4JAlyT+HtRmVpVeoV6FJgod9co1H
5GaOw2EhB82Bc1V4SQJBAIi8gIyTW4ITfuhyXPepIOlVKe2DfGMB0bNLHj/VSrV6
tUUyTyrnVfJsARw5YUjkvzm81Sd8mvQBr5HR+IKXYco=
-----END RSA PRIVATE KEY-----`
```


## Keystore 秘钥库
对于app用户，您可以提供以下格式的信息，让他访问自己的信息(如资产)，也可以让Mixin网络上的其他dapp使用。

```json
// file name keystore.json
{
  "version":"1.0.0",
  "user_id":"06aed1e3-bd77-4a59-991a-5bb5ae6fbb09",
  "session_id":"a34c07a9-755d-4b54-94c5-e45e9a2dd43e",
  "pin_token":"brM63kx....1w6pFM=",
  "session_key":"-----BEGIN RSA PRIVATE KEY-----
MIICXQIBAAKBgQC+cgmjyrFoWUblxsldm2kxCJEwgLN89+rxV+dmZr0l6e4X7JpA
...
TvI+F9wH+FzB7USctTCSQR22asSDRiSsG8omvHbp+X2R
-----END RSA PRIVATE KEY-----"
}
```
其实就是创建 app 之后会生成的一个文件