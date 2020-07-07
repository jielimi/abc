# Extensions {#extensions}

用于创建和管理运行时扩展的类

#### Extension

用于编写按需加载模块的基扩展类。

###### Methods

| name | description |
| :--- | :--- |
| constructor\(name: string\): Extension | 构造函数 |
| onExecute\(\_args: string\[\]\): Promise&lt;void&gt; | 在第一次加载扩展时在调用onLoad之后立即调用的方法。 |
| onLoad\(\_args: string\[\]\): Promise&lt;void&gt; | 在首次加载扩展时调用的方法。 |
| resolveResourceUrl\(relativeUrl: string\): string | 返回从外部服务器加载扩展时需要的完全限定的资源URL |

###### Properties

| name | type | description |
| :--- | :--- | :--- |
| \_defaultNs | string | 子类应该用默认的I18N命名空间名称覆盖它。 |
| i18n | I18n | 该属性检索特定于扩展的本地化实例。 |
| name | string | 扩展的名称。 |



