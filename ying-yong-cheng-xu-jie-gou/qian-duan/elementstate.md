# ElementState

类来处理前端元素的状态

## Classes

| name | description |
| :--- | :--- |
| ElementState | 在web浏览器中表示的元素的“状态” |
| EntityState | 在web浏览器中表示的实体的“状态”。 |

### Methods

| name | description |
| :--- | :--- |
| constructor\(props: ElementProps, iModel: IModelConnection\): ElementState | 构造函数 |

### Inherited methods

| name | inherited from | description |
| :--- | :--- | :--- |
| clone\(iModel?: IModelConnection\): this | EntityState | 复制此EntityState的独立副本 |
| equals\(other: this\): boolean | EntityState | 如果此EntityState等于另一个EntityState，则返回true |

### Properties

| name | type | description |
| :--- | :--- | :--- |
| code | Code | 此元素的Code |
| federationGuid | undefined \| GuidString | 分配给此元素的FederationGuid |
| model | Id64String | 包含此元素的模型的ModelId |
| parent | undefined \| RelatedElement | 父元素，如果没有定义，返回undefined |
| userLabel | undefined \| string | 为此元素指定的标签 |

### Defined in

[core/frontend/src/EntityState.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/EntityState.ts#L79)



