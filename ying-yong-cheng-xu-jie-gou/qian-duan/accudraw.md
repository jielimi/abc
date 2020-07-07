# AccuDraw {#accudraw}

AccuDraw为在视图中创建和修改图元提供了有用的帮助。

## Classes

| name | description |
| :--- | :--- |
| AccuDrawHintBuilder | AccuDrawHintBuilder是一个工具辅助类，它促进AccuDraw交互。 |

## AccuDrawHintBuilder

AccuDrawHintBuilder是一个工具帮助器类，用于促进AccuDraw交互。Accudraw是输入坐标数据的辅助工具。工具不会直接更改当前AccuDraw状态；工具的工作只是向AccuDraw提供有关当前刀具状态的首选AccuDraw配置的“提示”。“上下文敏感度”和“浮动原点”等用户设置会影响应用提示的方式。

参考：[https://www.imodeljs.org/learning/frontend/primitivetools/\#accudraw](https://www.imodeljs.org/learning/frontend/primitivetools/#accudraw "Writing a PrimitiveTool")

### Methods

| name | description |
| :--- | :--- |
| sendHints\(activate: boolean = true\): boolean | 使用当前生成器状态调用AccuDraw.setContext。 |
| setAngle\(angle: number\): void |  |
| setDistance\(distance: number\): void |  |
| setModePolar\(\): void |  |
| setModeRectangular\(\): void |  |
| setNormal\(normal: Vector3d\): void |  |
| setOrigin\(origin: Point3d\): void |  |
| setRotation\(rMatrix: Matrix3d\): void |  |
| setXAxis\(xAxis: Vector3d\): void |  |
| setXAxis2\(xAxis: Vector3d\): void |  |
| activate\(\): void |  |
| deactivate\(\): void |  |

### Properties

| name | type | description |
| :--- | :--- | :--- |
| enableSmartRotation	 | boolean |  |
| setLockAngle | boolean |  |
| setLockDistance | boolean |  |
| setLockX | boolean |  |
| setLockY | boolean |  |
| setLockZ | boolean |  |
| setOriginAlways | boolean |  |
| setOriginFixed | boolean |  |

### Defined in

[core/frontend/src/AccuDraw.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/AccuDraw.ts#L3048)



