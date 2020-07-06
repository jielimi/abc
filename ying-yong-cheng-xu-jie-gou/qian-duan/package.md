# IModelApp

用于配置和管理iModel.js应用程序

连接用户界面与iModel.js服务。一个会话中只能有一个IModelApp处于活动状态。IModelApp的所有成员都是静态的，它是一个获取会话信息访问权的单例对象。

在@bentley/imodeljs-frontend前端包执行任何交互操作之前，IModelApp.startup必须被调用。可以通过向IModelApp.startup配置选项信息自定义前端应用程序。

#### Methods

| name | description |
| :--- | :--- |
| makeLogoCard\(opts:object\) | 创建一个新的logo标志 |
|  |  |

#### Properties

|  |  |
| :--- | :--- |
|  |  |



