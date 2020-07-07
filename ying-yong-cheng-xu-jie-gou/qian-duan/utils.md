# Utils

其他实用程序类。

### Classes

| name | description |
| :--- | :--- |
| AuthorizedFrontendRequestContext | 为下游服务器应用程序提供一些通用上下文，以获取请求的详细信息。 |
| FrontendRequestContext | 为下游服务器应用程序提供通用上下文，以获取请求的详细信息。 |

###### AuthorizedFrontendRequestContext

为下游服务器应用程序提供一些通用上下文，以获取来自前端的请求的详细信息。上下文用于需要授权的应用程序。

###### Methods

| name | description |
| :--- | :--- |
| constructor\(accessToken: AccessToken, activityId: string = Guid.createValue\(\)\): AuthorizedFrontendRequestContext | 为前端操作创建一个新的上下文以传递给各种服务。 |
| create\(activityId: string = Guid.createValue\(\)\): Promise&lt;AuthorizedFrontendRequestContext&gt; | 为前端操作创建一个新的上下文，以传递给需要的服务。 |

###### FrontendRequestContext

###### method

| name | description |
| :--- | :--- |
| constructor\(activityId: string = Guid.createValue\(\)\): FrontendRequestContext | 为代理应用程序或长时间运行的前端操作创建新的上下文，以便传递给各种服务。 |

### Defined in

[core/frontend/src/FrontendRequestContext.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/FrontendRequestContext.ts#L56)







