# ToolRegistry

保存了ToolID和它们对应的工具类之间的映射。这提供了一种通过工具ID查找工具的机制，还提供了一种遍历可用工具集的方法。

### Methods

| name | description |
| :--- | :--- |
| create\(toolId: string, ...args: any\[\]\): Tool | 按toolId查找工具，如果找到，则使用提供的参数创建一个实例。 |
| find\(toolId: string\): ToolType | 按toolId查找工具。 |
| getToolList\(\): ToolList | 获取当前注册的工具列表，不包括隐藏工具。 |
| register\(toolClass: ToolType, namespace?: I18NNamespace, i18n?: I18N\): void | 注册工具类。 |
| registerModule\(moduleObj: any, namespace?: I18NNamespace, i18n?: I18N\): void | 注册模块中找到的所有工具类。 |
| run\(toolId: string, ...args: any\[\]\): boolean | 按toolId查找工具，如果找到，使用提供的参数创建一个实例并运行它。 |
| unRegister\(toolId: string\): void | 取消注册已经注册的工具类。 |

### Properties

| name | type | description |
| :--- | :--- | :--- |
| tools | Map&lt;string, Tool&gt; |  |

### Defined in

[core/frontend/src/tools/Tool.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/tools/Tool.ts#L740)

