# DisplayStyles

显示样式，描述应该应用于视图内容的样式。包括：ViewFlags，Background，RenderMode，Environment等。它们通过DisplayStyleState类加载到前端的内存中。

### DisplayStyleState 

DisplayStyle定义了为ViewState的内容设置样式的参数

注意：如果DisplayStyle与正在视口中渲染的ViewState关联，则直接修改DisplayStyle通常不会导致屏幕上立即可见的更改。ViewState提供了转发到displayStypeapi的API，并确保屏幕及时更新。

### Methods

| name | description |
| :--- | :--- |
| constructor\(props: DisplayStyleProps, iModel: IModelConnection\): DisplayStyleState | 从它的JSON表示构造一个新的DisplayStyleState。 |
| changeBackgroundMapProps\(props: BackgroundMapProps\): void | 修改背景地图显示设置的子集。 |
| dropSubCategoryOverride\(id: Id64String\): void | 删除此样式应用于子类别外观的任何子类别覆盖。 |
| equalState\(other: DisplayStyleState\): boolean | 与其他显示样式执行逻辑比较。 |
| getSubCategoryOverride\(id: Id64String\): SubCategoryOverride \| undefined | 获取此样式应用于子类别外观的覆盖。 |
| is3d\(\): this | 获取此样式应用于子类别外观的覆盖。 |
| overrideSubCategory\(id: Id64String, ovr: SubCategoryOverride\): void | 自定义此显示样式绘制属于子类别的几何图形的方式。 |

### Properties

| name | type | description |
| :--- | :--- | :--- |
| backgroundColor | ColorDef | 此DisplayStyle的背景色 |
| backgroundMapSettings | BackgroundMapSettings | 控制如何在视图中显示背景贴图的设置。 |
| hasSubCategoryOverride | boolean | 如果\[\[SubCategoryOverride\]由此样式定义，则返回true。 |
| monochromeColor | ColorDef | 在单色模式下用于绘制几何图形的颜色。 |
| name | String | 此DisplayStyle的名称。 |
| settings | DisplayStyleSettings | 此显示样式设置的容器。 |
| viewFlags | ViewFlags | 与此样式关联的ViewFlags。 |

### Defined in

[core/frontend/src/DisplayStyleState.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/DisplayStyleState.ts#L34)



