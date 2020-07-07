# OIDC {#oidc}

用于使用OpenID连接（OIDC）协议的类。

### Classes

| name | description |
| :--- | :--- |
| OidcBrowserClient | 为单页应用程序生成OIDC/OAuth令牌的实用程序（在浏览器中运行）。 |

###### OidcBrowserClient

| name | description |
| :--- | :--- |
| constructor\(\_configuration: OidcFrontendClientConfiguration\): OidcBrowserClient | 构造函数。 |
| dispose\(\): void | 处理此客户端持有的资源。 |
| getAccessToken\(requestContext?: ClientRequestContext\): Promise&lt;AccessToken&gt; | 返回一个promise，解析为当前授权用户的AccessToken。 |
| initialize\(requestContext: FrontendRequestContext\): Promise&lt;void&gt; | 用于初始化客户端-必须在调用任何其他方法之前等待。 |
| signIn\(requestContext: ClientRequestContext, successRedirectUrl?: string\): Promise&lt;void&gt; | 启动登录过程。 |
| signInSilent\(requestContext: ClientRequestContext\): Promise&lt;User&gt; | 尝试使用授权提供程序进行静默登录。 |
| signOut\(requestContext: ClientRequestContext\): Promise&lt;void&gt; | 启动注销过程。 |

###### Properties

| name | type | description |
| :--- | :--- | :--- |
| \_accessToken | undefined \| AccessToken |  |
| hasExpired  | boolean | 如果用户已登录，但令牌已过期并需要刷新，则设置为true。 |
| hasSignedIn | boolean | 如果已登录，则设置为true-accessToken可能处于活动状态或已过期，需要刷新。 |
| isAuthorized  | boolean | 如果有当前授权用户，则设置为true。 |
| onUserStateChanged | BeEvent&lt;\(token: AccessToken \| undefined\) =&gt; void&gt; | 当用户的登录状态更改时调用的事件-这可能是由于调用signIn（）、signOut（）。 |

### Defined in

[core/frontend/src/oidc/OidcBrowserClient.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/oidc/OidcBrowserClient.ts#L82)



