## ViewState

ViewDefinition元素的前端状态。ViewState通常与Viewport关联，以在屏幕上显示视图的内容。

通过将ViewDefinition加载到ViewState对象中来打开视图。他们开始显示保存在iModel中的内容，但用户可以使用查看工具修改所看到的内容。这些更改只是临时的（在内存中），除非通过将它们保存回iModelIModelDb.Elements.updateElement。

内存中ViewState的实例保存对其他几个对象的引用，包括CategorySelectorState、DisplayStyle3dState和ModelSelectorState（用于空间视图）。由于这些对象中的每一个都必须异步加载到前端，因此有一个异步方法称为IModelConnection.Views.load当ViewState和显示视图所需的所有其他状态对象就绪时，返回一个promise。

#### Methods

| name | description |
| :--- | :--- |
| adjustAspectRatio\(aspect: number\): void | 调整此ViewState的纵横比，使其与提供的值匹配。 |
| allow3dManipulations\(\): boolean | 如果允许ViewTools在此视图上以三维方式操作，则返回true。 |
| calculateFrustum\(result?: Frustum\): Frustum | 根据此ViewState的参数计算世界坐标截锥。 |
| computeFitRange\(\): Range3d | 计算范围世界坐标系紧密包围此视图内容的坐标。 |
| equals\(other: this\): boolean | 确定此ViewState是否与另一个ViewState完全匹配。 |
| forEachModel\(func: \(model: GeometricModelState\) =&gt; void\): void | 对每个查看的模型执行一个函数 |
| getAspectRatio\(\): number | 获取此视图的纵横比（宽/高） |
| getAspectRatioSkew\(\): number | 获取用于放大视图y轴的纵横比倾斜（x/y，通常为1.0）。 |
| getAuxiliaryCoordinateSystemId\(\): Id64String | 获取此ViewState的辅助坐标系的Id |
| getCenter\(result?: Point3d\): Point3d | 在视图的几何中心获取点。 |
| getExtents\(\): Vector3d | 获取此视图的范围世界坐标系协调。 |
| getGridOrientation\(\): GridOrientationType | 获取此视图的网格设置 |
| getGridSettings\(vp: Viewport, origin: Point3d, rMatrix: Matrix3d, orientation: GridOrientationType\): void | 使用栅格设置中来自栅格方向的信息填充给定原点和旋转。 |
| getOrigin\(\): Point3d | 获取此视图的来源世界坐标系协调 |
| getRotation\(\): Matrix3d | 获取此视图的3x3正交法线矩阵。 |
| getSubCategoryOverride\(id: Id64String\): SubCategoryOverride | 使用此ViewState渲染时，查询应用于属于特定子类别的几何体的符号替代。 |
| getTargetPoint\(result?: Point3d\): Point3d | 获取目标视角。 |
| getViewClip\(\): ClipVector | 获取此视图的剪裁体积（如果已定义） |
| getViewedExtents\(\): AxisAlignedBox3d | 获取此视图的范围世界坐标系协调。 |
| getXVector\(result?: Vector3d\): Vector3d | 得到指向视图X（从左到右）方向的单位向量。 |
| getYVector\(result?: Vector3d\): Vector3d | 获取指向视图Y（从下到上）方向的单位向量。 |
| getZVector\(result?: Vector3d\): Vector3d | 获取指向视图Z（从前到后）方向的单位向量。 |
| is2d\(\): this | 如果此ViewState为-ViewState2d，则返回true |
| is3d\(\): this | 如果此ViewState为-ViewState3d，则返回true |
| isCameraEnabled\(\): this | 如果此ViewState是当前打开相机的ViewState3d，则返回true。 |
| isDrawingView\(\): this | 如果此ViewState是DrawingViewState，则返回true |
| isSpatialView\(\): this | 如果此ViewState为-SpatialViewState，则返回true |
| load\(\): Promise&lt;void&gt; | 从后端异步加载此ViewState所需的任何数据。 |
| lookAtViewAlignedVolume\(volume: Range3d, aspect?: number, options?: ViewChangeOptions\): void | 查看由视图局部坐标中的范围定义的空间体积，保持其当前旋转。 |
| lookAtVolume\(volume, aspect?: number, options?: ViewChangeOptions\): void | 更改此视图显示的体积，保持其当前旋转。 |
| resetExtentLimits\(\): void | 将此ViewState的范围允许的最大值和最小值重置为其默认值。 |
| setAspectRatioSkew\(val: number\): void | 为此视图设置纵横比倾斜（x/y）。 |
| setAuxiliaryCoordinateSystem\(acs?: AuxCoordSystemState\): void | 为此视图设置或清除辅助坐标系统。 |
| setCategorySelector\(categories: CategorySelectorState\): void for this view. | 为此视图设置CategorySelector。 |
| setCenter\(center: Point3d\): void | 将此视图的中心设置为新位置。 |
| setExtents\(viewDelta: Vector3d\): void | 在中设置此视图的范围世界坐标系协调。 |
| setGridSettings\(orientation: GridOrientationType, spacing: Point2d, gridsPerRef: number\): void | 设置此视图的网格设置 |
| setOrigin\(viewOrg: XYAndZ\): void | 在中设置此视图的原点世界坐标系协调。 |
| setRotation\(viewRot: Matrix3d\): void | 更改视图的旋转。 |
| setRotationAboutPoint\(rotation: Matrix3d, point?: Point3d\): void | 通过围绕一个点旋转，将此ViewState的旋转设置为提供的旋转。 |
| setStandardRotation\(id: StandardViewId\): void | 将此视图定向为标准视图的一个旋转。 |
| setViewClip\(clip?: ClipVector\): void | 设置或清除此视图的剪裁体积。 |
| setupFromFrustum\(inFrustum: Frustum, opts?: ViewChangeOptions\): ViewStatus | 从现有的截锥初始化原点、范围和旋转 |
| viewsCategory\(id: Id64String\): boolean | 确定指定的类别是否显示在此视图中 |
| viewsModel\(modelId: Id64String\): boolean | 如果此视图显示ViewState.模型由Id指定。 |
| createFromProps\(\_props: ViewStateProps, \_iModel: IModelConnection\): ViewState | 从一组属性创建一个新的ViewState对象。 |

#### Properties

| name | description |
| :--- | :--- |
| analysisStyle | 从该ViewState的displayStyle获取AnalysisDisplayProperties。 |
| auxiliaryCoordinateSystem | 获取此ViewState的辅助坐标系状态对象。 |
| backgroundColor | 获取此视图的背景色。 |
| categorySelector | 选择此ViewState显示的类别。 |
| defaultExtentLimits | 返回此ViewState的默认范围限制。 |
| displayStyle | 为此视图状态选择样式参数。 |
| extentLimits | 获取或设置此ViewState的范围允许的最大值和最小值 |
| globalScopeFactor | 表示视图全局范围的值--大于1表示该视图的范围是全局的（查看地球的大部分地区）。 |
| name | 获取生成此ViewState的ViewDefinition的名称。 |
| viewFlags | 从这个ViewState的DisplayStyleState获取ViewFlags。 |

### Defined in

[core/frontend/src/ViewState.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/ViewState.ts#L176)

