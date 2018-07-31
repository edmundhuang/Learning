# Grant Types 授权类型  
* Implicit 隐式
* Authorization Code 授权码
* Hybrid 混合
* Client credentials 客户端证书
* Rosource owner password 资源拥有者密码
* Refresh tokens  刷新令牌
* Entension grants   扩展授权

文章
[Identity Server 4 with ASP.NET Core 2.0](https://www.codeproject.com/Articles/1205745/Identity-Server-with-ASP-NET-Core)
### Require User Interaction with Auth. Server  需要用户和授权服务交互
**Implicit Grant  隐式发放**
此流程通常用在 原生/本地/移动 客户端并具有下列步骤：
1.  `用户` 访问客户端
2.  `用户` 被转向到授权服务
3.  `用户` 提供用户名密码
4.  `用户` 被转向会客户端，并包含一个访问令牌

**注意事项：** 建议使用 Authorization Code （授权码）方式代替 隐式发放。

**Authorization Code 授权码方式**
此流程通常用在 Web 应用客户端，并具有下列步骤：
1. `用户` 访问客户端
2. `用户` 被转向到授权服务
3. `用户` 提供用户名密码
4. `用户` 被转向会客户端，并包含一个授权码  
  **注意：** 授权码是暴露给用户的。
5. `客户端` 访问授权服务，交换授权码和访问令牌  
  **注意：** 访问令牌没有暴露给用户。
6. `客户端` 使用访问令牌获取被保护的字眼。

### Not Requiring User Interaction with Auth. Server 不需要用户和授权服务交互  

**Reousrce Owner Password Credentials 资源拥有者密码凭证**  
此流程通常用在“可信客户端”，并具有如下步骤
1. `用户` 访问客户端，提供用户名密码。
2. `客户端` 访问授权服务器，使用用户名密码交换访问令牌。
3. `客户端` 使用访问令牌，访问受保护资源。

**Client Credentials 客户端凭证**  
此流程通常用在 “客户-服务器” 通信中，不需要人工介入，具有如下步骤：  
1. `客户端` 访问授权服务器，使用“客户端ID”和“安全码”交换访问令牌。
2. `客户端` 使用访问令牌，访问受保护资源。
