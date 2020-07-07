# IModelApp

用于配置和管理iModel.js应用程序

连接用户界面与iModel.js服务。一个会话中只能有一个IModelApp处于活动状态。IModelApp的所有成员都是静态的，它是一个获取会话信息访问权的单例对象。

在@bentley/imodeljs-frontend前端包执行任何交互操作之前，IModelApp.startup必须被调用。可以通过向IModelApp.startup配置选项信息自定义前端应用程序。

#### Methods

| name | description |
| :--- | :--- |
| makeLogoCard\(opts:object\) | 创建一个新的logo标志 |
| queryRenderCompatibility\(\) | 获取客户端系统的对WebGL呈现的兼容性信息。 |
| shutdown\(\) | 必须在应用程序退出前调用以释放任何保留的资源 |
| startup\(opts?: IModelAppOptions\) | 在任何使用imodel.js fronted服务的应用程序中，必须调用此方法 |

#### Properties

| name | description |
| :--- | :--- |
| accuSnap  |  |
| animationInterval | 控制应用程序轮询可能需要请求新动画帧的更改的频率 |
| applicationId | 此应用程序的id |
| applicationLogoCard | 应用程序可以实现此方法来提供徽标卡 |
| applicationVersion | 应用版本 |
| authorizationClient | 提供各种前端api的授权信息 |
| i18n | 当前会话的i18n |
| iModelClient | 当前会话的iModelClient  |
| notifications | 当前会话的通知管理器 |
| renderSystem | 当前会话的renderSystem |
| sessionId | 会话的唯一标识 |
| settings | 配置信息 |
| toolAdmin | 此会话的toolAdmin |
| tools | 当前所注册的tools工具组件 |
| uiAdmin | 当前uiAdmin |
| viewManager | 当前viewManager |

defined in [core/frontend/src/IModelApp.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/IModelApp.ts#L158)



