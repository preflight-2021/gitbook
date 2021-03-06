



# OAuth2 (Open Auth To)



## 阐述

OAuth2（开放授权）开放标准给到第三方接入用户登录授权并获取服务方存储的用户基本信息，服务方无需向第三方应用提供用户方登录名、密码和用户方数据的所有内容。作用是让第三方应用在用户授权的情况下，并通过认证服务器授权，实现在资源服务区上获取用户基本信息。

与上篇JWT不同的是,  OAuth2是一种授权框架 ，而JWT是一种认证协议。而要保证数据的安全性， 则是用HTTPS保证。

OAuth2主要完成第三方帐号登录的场景（如：微信、微博、QQ、Github帐号）一键注册登录某APP。

JWT则是用在前后端分离的场景下实现API接口进行保护。

### 角色：

1. **Third-party application**：第三方应用， 即客户端

2. **Resource Owner**：用户本身，即资源持有方

3. **Authorization server**: 认证服务器

4. **Resource server**: 资源服务器，与认证服务器仅逻辑 节点不同， 实际可放一起

5. **User Agent**: 用户代理， 指浏览器

6. **Http Service**: 服务提供方（如：QQ或微信具备用户信息的服务方）

   

### 运行流程

<<img src="http://raw.githubusercontent.com/preflight-2021/gitbook/master/business/resources/oauth2-flow.png" alt="Oauth2-flow"  />

1. 用户打开客户端，客户端响应用户授权请求。

2. 用户允许授权客户端。

3. 客户端通过用户授权获得的授权码(Code)， 向认证服务器申请令牌（Token）。

4. 认证服务器完成认证，则发放令牌（Token）至客户端。

5. 客户端使用令牌，向资源服务器申请获取资源（UserInfo）。

6. 资源服务器确认令牌有效，同意获取资源（UserInfo）。

   

## 客户端授权模式

### 	**授权码模式(authorization code)**

​		授权码模式（authorization code）是目前功能最完整、流程最严密的授权模式。

​		授权流程:

​		1,  用户访问客户端, 客户端引导并跳转到认证服务器进行授权认证。

​		2，用户给与授权， 认证服务器发送一个固定时效的认证码， 并重定向的原页面。

​        3，原页面请求客户端，客户端获取授权码， 根据授权码和重定向URL向认证服务器换取申请令牌（Access Token）。

​		4， 认证服务器核对授权码有效， 则发放访问令牌（Access Token）和更新令牌（Refresh Token），并跳转到重定向页。



### 	密码模式(resource ower password credentials)

​		密码模式（resource ower password credentials）是用户将访问认证服务器（服务商）的用户名和密码提供给到客户端。客户端获取到帐号密码像认证服务		器索要授权。这种模式下， 用户需要提供帐号密码给到客户端， 且不支持更新令牌。通常不允许客户端存储用户账号信息， 前提要基于高信任度的情况下。

​		授权流程：

​		1， 用户向客户端提供用户名和密码。

​		2， 客户端将用户名和密码发给认证服务器，向后者请求令牌。

​		3， 认证服务器确认无误后，向客户端提供访问令牌。（不支持Refresh Token）

### 客户端模式(client credentials)

​		客户端模式(client credentials)是客户端以自己的名义，而不借助用户授权，直接向认证服务器（服务商）进行认证。该模式并不属于OAuth框架所要解决的		问题。例如：用户直接在客户端进行注册，客户端直接向认证服务器申请授权提供服务， 其实不存在授权问题。

​		授权流程：

​		1， 客户端向认证服务器进行身份证认证， 并要求一个访问令牌。

​		2， 认证服务器确认无误后， 像客户端提供授权令牌。

###  简化模式(implicit)

​		简化模式（implicit grant type）不通过第三方应用程序的服务器，直接在浏览器中向认证服务器申请令牌，跳过了"授权码"这个步骤，因此得名。所有步骤		在浏览器中完成，令牌对访问者是可见的，且客户端不需要认证。

​		授权流程：

​		1， 客户端将用户导向认证服务器。

​		2， 用户决定是否给于客户端授权。如用户给予授权，认证服务器将用户导向客户端指定的"重定向URI"，并在URI的Hash部分包含了访问令牌。

​		3， 浏览器向资源服务器发出请求，其中不包括上一步收到的Hash值。

​		4， 资源服务器返回一个网页，其中包含的代码可以获取Hash值中的令牌。

​		5， 浏览器执行上一步获得的脚本，提取出令牌。再将令牌发给客户端。

### 扩展模式(Extension)

​		扩展模式，是一种自定义模式。规范中仅对“grant type”参数提出了须为URI的要求。对于其他申请数据，可以根据需求进行自定义。

## 应用场景

​		1， 系统敏感资源服务进行安全认证及资源保护工作。

​		2， 多个服务的统一登录认证中心、内部系统之间受保护资源请求。

​		3， 将受保护的用户资源授权给第三方信任用户。

​		4， 开发平台类似百度开放平台，腾讯开放平台。

## 官方网站

### https://oauth.net/2/

### https://oauth.net/code/(go/java )

## 代码示例

> 地址： https://github.com/

