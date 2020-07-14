## Viewport

Viewport将一个或多个模型的内容通过HTMLCanvasElement呈现到一个或多个视口中。它包含一个定义其查看参数的ViewState对象。ViewTools可以修改ViewState对象。对视图状态的更改仅在Viewport.synchWithView方法被调用。

通常，由于Viewport基本上控制其附加的ViewState，所以应该通过Viewport自己的API间接地更改ViewState。这样做可以确保Viewport与其ViewState之间的同步是可靠和自动的。例如：

`要更改Viewport中显示的类别或模型集，请使用Viewport.changeCategoryDisplay以及Viewport.changeModelDisplay而不是直接修改ViewState的CategorySelectorState或ModelSelectorState。`

`要更改视图标志，请设置Viewport.viewFlags而不是直接修改ViewState的DisplayStyleState。`

`要修改DisplayStyleState：`

```
const style = viewport.displayStyle.clone();
style.backgroundColor = ColorDef.red.clone(); // 或任何其他需要的修改
viewport.displayStyle = style;
```

在对ViewState进行更改时，Viewport也会保留其以前副本的堆栈，通过允许撤消/重做查看工具（即“undo”和“redo”）。

#### Methods

| name | description |
| :--- | :--- |
| addViewedModels\(models: Id64Arg\): Promise&lt;void&gt; | 将一组模型添加到此Viewport中当前显示的模型集中。 |
| changeBackgroundMapProps\(props: BackgroundMapProps\): void | 修改背景地图显示设置的子集。 |
| changeCategoryDisplay\(categories: Id64Arg, display: boolean, enableAllSubCategories: boolean = false\): void | 启用或禁用属于由Id指定的一组类别的元素的显示。 |
| changeModelDisplay\(models: Id64Arg, display: boolean\): boolean | 在此视口中当前显示的模型中添加或删除一组模型。 |
| changeSubCategoryDisplay\(subCategoryId: Id64String, display: boolean\): void | 在此视口中显示时，更改属于指定子类别的几何图形的可见性。 |
| changeView\(view: ViewState, \_opts?: ViewChangeOptions\): void | 更改此视口的视图状态。 |
| changeViewedModel2d\(baseModelId: Id64String, options?: undefined\): Promise&lt;void&gt; | 尝试更改此视口显示的二维模型（如果其ViewState为ViewState2d）。 |
| changeViewedModels\(modelIds: Id64Arg\): boolean | 如果该视口正在显示空间视图，尝试替换当前由该视口查看的模型集。 |
| clearAlwaysDrawn\(\): void | 清除始终绘制的元素集。 |
| clearNeverDrawn\(\): void | 清除从未绘制的元素集。 |
| cssPixelsToDevicePixels\(cssPixels: number\): number | 使用此视口的设备像素比率将以CSS像素为单位的数字转换为设备像素。 |
| determineVisibleDepthRange\(rect?: ViewRect, result?: DepthRangeNpc\): DepthRangeNpc | 计算屏幕区域的npc深度值的范围。 |
| dispose\(\): void |  |
| dropSubCategoryOverride\(id: Id64String\): void | 删除指定子类别的任何子类别覆盖。 |
| getContrastToBackgroundColor\(\): ColorDef | 获取与此视口的当前背景色形成对比的颜色。 |
| getFrustum\(sys: CoordSystem = CoordSystem.World, adjustedBox: boolean = true, box?: Frustum\): Frustum | 获取与指定坐标系中视口的8个角相对应的8点截锥。 |
| getPixelSizeAtPoint\(point?: Point3d\): number | 获取世界坐标系中给定点处像素的宽度（视图坐标系中x方向的单位矢量），返回以米（世界单位）为单位的结果。 |
| getSubCategoryAppearance\(id: Id64String\): SubCategoryAppearance | 查询属于特定子类别的几何体在此视口中渲染时使用的符号。 |
| getSubCategoryOverride\(id: Id64String\): SubCategoryOverride | 在此视口中渲染时，查询应用于属于特定子类别的几何体的符号替代。 |
| getWorldFrustum\(box?: Frustum\): Frustum | 以世界坐标获取此视口的当前（未调整）视锥的副本。 |
| invalidateDecorations\(\): void | 将当前的装饰集标记为无效，以便在下一个渲染帧上重新创建它们。 |
| isSubCategoryVisible\(id: Id64String\): boolean | 确定属于特定子类别的几何图形是否在此视口中可见（假定显示包含的类别）。 |
| npcToView\(pt: Point3d, out?: Point3d\): Point3d | 从转换点协调系统。Npc到坐标系视图。 |
| npcToViewArray\(pts: Point3d\[\]\): void | 转换点数组协调系统。Npc到坐标系视图 |
| npcToWorld\(pt: XYAndZ, out?: Point3d\): Point3d | 从转换点协调系统。Npc到世界坐标系 |
| npcToWorldArray\(pts: Point3d\[\]\): void | 转换点数组协调系统。Npc到世界坐标系 |
| overrideSubCategory\(id: Id64String, ovr: SubCategoryOverride\): void | 在该视口中渲染时，替代属于特定子类别的几何体的符号。 |
| pixelsFromInches\(inches: number\): number | 根据屏幕DPI将英寸转换为像素。 |
| readImage\(rect: ViewRect = new ViewRect\(0, 0, -1, -1\), targetSize: Point2d = Point2d.createZero\(\), flipVertically: boolean = false\): ImageBuffer | 从当前视口中读取当前渲染系统中的图像。 |
| replaceViewedModels\(modelIds: Id64Arg\): Promise&lt;void&gt; | 如果该视口正在显示空间视图，请尝试替换当前由该视口查看的模型集 |
| scroll\(screenDist: XAndY, options?: ViewChangeOptions\): void | 按给定的像素数滚动视图。 |
| setAlwaysDrawn\(ids: Id64Set, exclusive: boolean = false\): void | 指定应始终在此视图中呈现的一组元素的ID，而不管类别和子类别的可见性如何。 |
| setFeatureOverrideProviderChanged\(\): void | 通知此视口Viewport.FeatureOverrideProvider已经改变到 |
| setLightSettings\(settings: LightSettings\): void |  |
| setNeverDrawn\(ids: Id64Set\): void | 指定不应在此视图中呈现的一组元素的ID。 |
| setStandardRotation\(id: StandardViewId\): void | 将此视口定向为标准视图的一个旋转。 |
| setupFromView\(pose?: ViewPose\): ViewStatus | 根据ViewState中的当前信息建立此视口的参数 |
| setupViewFromFrustum\(inFrustum: Frustum\): boolean | 调用视图.setupfromstum然后Viewport.setupFromView |
| synchWithView\(\_options\): void | 调用Viewport.setupFromView然后应用可选行为。 |
| turnCameraOn\(lensAngle?: Angle\): ViewStatus | 如果相机当前处于关闭状态，将其打开。 |
| updateChangeFlags\(newView: ViewState\): void Protected | 从finishUndoRedo、applyViewState和changeView调用，可能会根据当前和新ViewState之间的差异重新计算更改标志。 |
| view4dToWorld\(input: Point4d, out?: Point3d\): Point3d | 从转换点坐标系视图作为4d点坐标系视图 |
| view4dToWorldArray\(viewPts: Point4d\[\], worldPts: Point3d\[\]\): void | 转换点数组坐标系视图4ds指向世界坐标系 |
| viewToNpc\(pt: Point3d, out?: Point3d\): Point3d | 从转换点坐标系视图到协调系统。Npc |
| viewToNpcArray\(pts: Point3d\[\]\): void | 转换点数组坐标系视图到协调系统。Npc |
| viewToWorld\(input: XYAndZ, out?: Point3d\): Point3d | 从转换点坐标系视图到世界坐标系 |
| viewToWorldArray\(pts: Point3d\[\]\): void | 转换点数组坐标系视图到世界坐标系 |
| viewsModel\(modelId: Id64String\): boolean | 如果此视口当前正在显示具有指定Id的模型，则返回true。 |
| worldToNpc\(pt: XYAndZ, out?: Point3d\): Point3d | 从转换点世界坐标系到协调系统。Npc |
| worldToNpcArray\(pts: Point3d\[\]\): void | 转换点数组世界坐标系到协调系统。Npc |
| worldToView\(input: XYAndZ, out?: Point3d\): Point3d | 从转换点世界坐标系到坐标系视图 |
| worldToView4d\(input: XYAndZ, out?: Point4d\): Point4d | 从转换点世界坐标系到坐标系视图作为4d点 |
| worldToView4dArray\(worldPts: Point3d\[\], viewPts: Point4d\[\]\): void | 转换点数组世界坐标系到坐标系视图，如4ds点 |
| worldToViewArray\(pts: Point3d\[\]\): void | 转换点数组世界坐标系到坐标系视图 |
| zoom\(newCenter, factor: number, options?: ViewChangeOptions\): ViewStatus | 按比例因子缩放视图，将新中心放置在给定点（世界坐标）。 |
| zoomToElementProps\(elementProps: ElementProps\[\], options?: undefined\): void | 缩放视图以显示给定的一组ElementProps周围最紧的框。 |
| zoomToElements\(ids: Id64Arg, options?: undefined\): Promise&lt;void&gt; | 缩放视图以显示给定元素集周围最紧的框。 |
| zoomToPlacementProps\(placementProps: PlacementProps\[\], options?: undefined\): void | 缩放视图以显示给定PlacementProps集周围最紧的框。 |
| zoomToVolume\(volume, options?: ViewChangeOptions\): void | 将视图缩放到世界坐标系中的空间体积。 |

### Properties

| name | description |
| :--- | :--- |
| alwaysDrawn | 应始终在此视图中呈现的一组元素的ID，而不考虑类别和子类别的可见性。 |
| backgroundMapSettings | 控制如何在视图中显示背景贴图的设置。 |
| continuousRendering | 启用或禁用连续渲染。 |
| devicePixelRatio | 此视口使用的设备像素比率。 |
| displayStyle | 显示样式控制器如何渲染此视口的内容。 |
| emphasisSettings | 控制在该视口中如何显示强调元素的设置。 |
| featureOverrideProvider | 可以自定义外观的对象视口。功能在视口中。 |
| hilite | 控制如何在此视口中突出显示元素的设置。 |
| iModel | 当前viewport的iModel |
| isAlwaysDrawnExclusive | 如果Viewport.alwaysDrawnset是此视图中唯一呈现的元素，返回ture |
| isCameraOn | 如果这是打开相机的三维视图，则为真。 |
| isDisposed | 如果此视口Viewport.dispose方法已被调用。 |
| isFadeOutActive | 启用或禁用“淡出”模式。 |
| isGridOn | 确定当前是否在此视口中启用栅格显示。 |
| neverDrawn | 不应在此视图中呈现的一组元素的ID。 |
| numReadyTiles | 最近绘制的框架，准备就绪并满足在视图中显示的所需详细程度的平铺数。 |
| numRequestedTiles | 要在此视口中显示的平铺的未完成请求数。 |
| numSelectedTiles | 从最近绘制的框架开始，选择在视图中显示的平铺数。 |
| onAlwaysDrawnChanged | 在该视口的“始终绘制”元素集更改后在下一帧调用的事件。 |
| onChangeView | 当Viewport.changeView调用以将当前ViewState替换为其他ViewState。 |
| onDisplayStyleChanged | 此视口的DisplayStyleState或其成员更改后在下一帧调用的事件。 |
| onFeatureOverrideProviderChanged | 事件在该视口之后的下一帧调用Viewport.FeatureOverrideProvider或提供程序的内部状态发生更改，因此需要重新计算重写。 |
| onFeatureOverridesChanged | 视口的FeatureSymbology.Overrides改变时候调用的事件。 |
| onNeverDrawnChanged | 在该视口的一组从未绘制的元素更改后在下一帧调用的事件。 |
| onRender | 当重画视口的可见内容时调用。 |
| onViewChanged | 每当此视口与其ViewState同步时调用的事件。 |
| onViewedCategoriesChanged | 此视口显示的类别集更改后在下一帧调用的事件。 |
| onViewedCategoriesPerModelChanged | 在该视口的PerMod集之后的下一帧调用的事件elCategoryVisibility.覆盖变化。 |
| onViewedModelsChanged | 此视口显示的模型集更改后在下一帧调用的事件。 |
| rotation | 此视口的旋转矩阵。 |
| solarShadowSettings | 控制此视口的阴影显示的设置。 |
| undoDelay | 不允许视图撤消缓冲区中的条目，除非它们之间的间隔超过此时间量。 |
| view | 此视口的ViewState |
| viewDelta | 此视口范围的对角之间的向量。 |
| viewFlags | 确定如何渲染此视口内容的ViewFlags。 |
| viewRect | 获取此视口的矩形坐标系视图协调。 |
| worldToViewMap | 提供世界坐标和视图坐标之间的转换。 |

### Defined in

[core/frontend/src/Viewport.t](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/Viewport.ts#L744)s



