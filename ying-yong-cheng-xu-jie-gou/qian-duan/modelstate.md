# ModelState

用于在前端处理模型状态的类。

### Methods

| name | description |
| :--- | :--- |
| constructor\(props: ModelProps, iModel: IModelConnection, state?: ModelState\): ModelState | 构造函数 |
| toJSON\(\): ModelProps | 将模型的所有自定义处理属性添加到json对象 |

### Properties

| name | description |
| :--- | :--- |
| asGeometricModel | 将此模型转换为几何模型 |
| asGeometricModel2d | 将此模型转换为二维几何模型 |
| asGeometricModel3d | 将此模型转换为三二维几何模型 |
| asSpatialModel | 将此模型转换为空间模型 |
| isGeometricModel | 判断是否为几何模型 |
| isPrivate |  |
| isTemplate |  |
| modelEmenent |  |
| name |  |
| parentModel |  |

### Defined in

[core/frontend/src/ModelState.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/ModelState.ts#L22)

