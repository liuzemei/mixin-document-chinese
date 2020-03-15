## Authentication Token（认证令牌）
Authentication Token用于请求受保护的资源。

> key:privateKey是使用 RSA PKCS#1 v1.5 生成的。您可以从 [https://golang.org/pkg/crypto/rsa](https://golang.org/pkg/crypto/rsa) 获得更多信息。

#### 获取认证令牌的参数
1. uid: 用户id
2. sid: 会话id
3. privateKey: 密钥
4. method: HTTP 请求方式, 例如: GET, POST
5. url: 没有主机名的URL路径, 例如: /transfers
6. body: HTTP 请求体, 例如: {“pin”: “encrypted pin token”}
#### 如何生成认证令牌
```go
// go语言代码示例
func SignAuthenticationToken(uid, sid, secret, method, uri, body string) (string, error) {
  expire := time.Now().UTC().Add(time.Hour * 24 * 30 * 3)
  sum := sha256.Sum256([]byte(method + uri + body))
  token := jwt.NewWithClaims(jwt.SigningMethodRS512, jwt.MapClaims{
    "uid": uid,
    "sid": sid,
    "iat": time.Now().UTC().Unix(),
    "exp": expire.Unix(),
    "jti": uuid.NewV4().String(),
    "sig": hex.EncodeToString(sum[:]),
  })

  block, _ := pem.Decode([]byte(secret))
  key, err := x509.ParsePKCS1PrivateKey(block.Bytes)
  if err != nil {
    return "", err
  }
  return token.SignedString(key)
}
```
Authentication Token 的格式如下：
```go
// Signed Authentication Token
eyJhbGciOiJSUzUxMiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1MzMwOTY0ODUsImlhdCI6MTUyNTMyMDQ4NSwianRpIjoiMjU5NGFkNTctOWRhZC00MjRmLTg1OTUtYjE0NzI3ZTI0ZTYxIiwic2lkIjoiYzA5Y2YzMTMtN2RlZC00MjVkLWFkM2YtYTFjZTRjZmQ1ZTVlIiwic2lnIjoiODVkZDIzOGE5ODM0NzE3ZGMxM2QzODQ0ZjYzYTFmZWUxM2Q4MmQyZTZjMmVlNDRlYWM3Yzc5MGY1ZGIyNWY4OCIsInVpZCI6Ijg5ZTBiZGVlLWMzNTUtNDdmMi05NDVhLWJlNDhiZTg3NTYwNiJ9.PYg6Cx5grs0flJe862R3VLEWKyTZPcXOGYF9RouztgR_mi3kleIzJt4vCwUZI9F7QrHBFMtTc3_wG_ymnnjsmnm0pBdoON4I-RxeaztIlyc1Ey9lLFe6_ARRUBXo_15ZORilS1hRdMREd84eQOLlO0ChieBPY0tSSiVqTaFZt3Q
```
你还需要从 PrivateKey 生成一个 base64 编码的 PublicKey

```go
// go语言代码示例
privateKey, _ := rsa.GenerateKey(rand.Reader, 1024)
publicKeyBytes, _ := x509.MarshalPKIXPublicKey(privateKey.Public())
sessionSecret := base64.StdEncoding.EncodeToString(publicKeyBytes)
```


## Encrypted PIN（PIN加密）
在您使用Mixin网络进行取款或转账之前。你必须有一个加密的密码。

>以下是生成加密pin所需的参数。
>1. pin: PIN码 例如：1234
>2. pinToken
>3. sessionId
>4. key: PrivateKey
>5. iterator: (迭代器)必须大于前一次，第一次必须大于0。创建新会话后，它将被重置为0。

如何生成一个加密的 PIN
```go
// go语言代码示例
func EncryptPIN(pin, pinToken, sessionId, privateKey string, iterator uint64) string {
  keyBlock, _ := pem.Decode([]byte(privateKey))
  key, err := x509.ParsePKCS1PrivateKey(keyBlock.Bytes)
  if err != nil {
    return ""
  }
  token, _ := base64.StdEncoding.DecodeString(pinToken)
  keyBytes, err := rsa.DecryptOAEP(sha256.New(), rand.Reader, key, token, []byte(sessionId))
  if err != nil {
    return ""
  }
  pinByte := []byte(pin)
  timeBytes := make([]byte, 8)
  binary.LittleEndian.PutUint64(timeBytes, uint64(time.Now().Unix()))
  pinByte = append(pinByte, timeBytes...)
  iteratorBytes := make([]byte, 8)
  binary.LittleEndian.PutUint64(iteratorBytes, iterator)
  pinByte = append(pinByte, iteratorBytes...)
  padding := aes.BlockSize - len(pinByte)%aes.BlockSize
  padtext := bytes.Repeat([]byte{byte(padding)}, padding)
  pinByte = append(pinByte, padtext...)
  block, _ := aes.NewCipher(keyBytes)
  ciphertext := make([]byte, aes.BlockSize+len(pinByte))
  iv := ciphertext[:aes.BlockSize]
  io.ReadFull(rand.Reader, iv)
  mode := cipher.NewCBCEncrypter(block, iv)
  mode.CryptBlocks(ciphertext[aes.BlockSize:], pinByte)
  return base64.StdEncoding.EncodeToString(ciphertext)
}
```
一个加密的 PIN 示例：
```
XgG4PAKf/Jq39Vo2t2oYPMDyoz1JMoC2+HZwzko44Yp8K565ZRhCNCPfgVZcw9/2
```
## Error Codes（错误代码）
Mixin API 只会使用 20x 和 500，你需要注意，500错误，可能是由 web 服务器，而不是 Mixin API 服务器造成的。

|Status	|Code|	Description|
| - | - | :- |
|202|	400|	请求体参数无效|
|202|	401|	请求未经授权的(Unauthorized)|
|202|	403|	请求拒绝|
|202|	404|	无法找到请求地址|
|202|	429|	请求太频繁|
|202|	10002|	请求字段无效|
|202|	10003|	发送短信到+8613800138000失败|
|202|	10004|	验证无效|
|202|	10005|	缺少验证|
|202|	10006|	需要更新|
|202|	20110|	无效电话号码+8613800138000|
|202|	20111|	权限不足|
|202|	20112|	无效的邀请码|
|202|	20113|	无效的电话验证码|
|202|	20114|	过期的手机验证码|
|202|	20115|	无效的二维码|
|202|	20116|	群组聊天已满|
|202|	20117|	余额不足|
|202|	20118|	无效的密码格式|(PIN)
|202|	20119|	密码不正确|(PIN)
|202|	20120|	转账金额太小|
|202|	20121|	授权代码过期了|
|202|	20122|	别人使用的电话号码|
|202|	20123|	你已经创建了太多的应用程序|
|202|	20124|	费用不足|
|202|	20125|	转账已由他人支付|
|202|	20126|	太多的贴纸(Too many stickers)|
|202|	20127|	提现金额太小|
|202|	20128|	好友太多|
|202|	20129|	发送验证码太频繁|
|202|	20130|	无效紧急联系人|
|202|	20131|	提现的 memo 格式无效|
|202|	30100|	区块链没有同步|
|202|	30101|	XYZ的私钥已丢失|
|202|	30102|	无效的地址格式|
|202|	30103|	%asset_id%池不足|
|500|	500|	内部服务器出错|
|500|	7000	|服务器错误(Blaze server error)|
|500|	7001	|操作超时(The blaze operation timeout.)|

一个错误相应的例子：
```json
{
  "error":{
    "status":500,
    "code":500,
    "description":"Internal Server Error"
  }
}
```