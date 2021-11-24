# JWT(JSON Web Token)

## 场景

1. Authorization (授权) : 这是使用JWT的最常见场景。一旦用户登录，后续每个请求都将包含JWT，允许用户访问该令牌允许的路由、服务和资源。单点登录是现在广泛使用的JWT的一个特性，开销很小，轻松地跨域使用。
2. Information Exchange (信息交换) : 用于安全的在各方之间传输信息。因为JWT可以被签名，例如，用公钥/私钥对，签名是使用头和有效负载计算的，还可以验证内容没有被篡改，由此可以验证发送方身份。

## 结构

1. Header
2. Payload
3. Signature

### Header

​	header典型的由两部分组成：算法名称（如：HMAC、SHA512、RSA等等）和 token 类型（JWT）。

```json
{
    "alg": "HS512",
    "typ": "JWT"
}
```

​	用Base64对这个JSON编码就得到第一部分。

### Payload

1. Registered claims : 这里有一组预定义的声明，它们不是强制的，但是推荐。比如：iss (issuer), exp (expiration time), sub (subject), aud (audience)等。
2. Public claims : 可以随意定义。
3. Private claims : 用于在同意使用它们的各方之间共享信息，并且不是注册的或公开的声明。

```json
{
    "sub": "1234567890",
    "name": "preflight",
    "expire": "2020-12-20 00：00：00"
}
```

​	用进行Base64编码就得到第二部分。

### Signature

​	签名是用于验证消息在传递过程中有没有被更改，并且，对于使用私钥签名的token，它还可以验证JWT的发送方是否为它所称的发送方。

​	例如：HMACSHA256(base64UrlEncode(header) + "." + base64UrlEncode(payload), secret)

​	用编码过的header、编码过的payload、一个秘钥，Header签名算法，得到第三部分。

### 官网地址：https://jwt.io/

### 官网示例：

![image-1](http://preflight-gitbook.oss-cn-shenzhen.aliyuncs.com/resources/image-1.png)

代码示例：

- java：github.com
- golang： github.com

文献参考:

- https://zhuanlan.zhihu.com/p/86937325
