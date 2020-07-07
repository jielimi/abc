## Using Viewports

Viewport是一个抽象类，它将ViewState连接到RenderTarget。

要将ViewState连接到网页上的矩形区域，请创建ScreenViewport类的实例。方法ScreenViewport.create接受一个htmldevelment和一个（完全加载的）ViewState。通过这种方式，ScreenViewport在web页面上的一个矩形区域（“div”）与iModel中的一组模型、一个显示截锥、一个DisplayStyle和渲染系统之间形成了连接。

##### `注意：在创建屏幕视口之前，请务必调用IModelApp.startup.`

### Loading Views from an iModel

IModelConnection.Views.getViewList返回一个数组IModelConnection.ViewSpecs以方便用户界面的格式。这可用于在列表中按名称显示可能的视图列表。

例如，要获取所有空间视图的列表：

```
/** Get a list of Spatial views from an iModel. */
public static async getSpatialViews(): Promise<IModelConnection.ViewSpec[]> {
  return this._iModel.views.getViewList({ from: SpatialViewState.classFullName });
}
```

要获取所有工程视图的列表，请执行以下操作：

```
/** Get a list of all Drawing views from an iModel. */
public static async getDrawingViews(): Promise<IModelConnection.ViewSpec[]> {
  return this._iModel.views.getViewList({ from: DrawingViewState.classFullName });
}
```

从列表中选择一个视图后，它可以加载：

```
/** Stub for a real UI that would present the user with the list and choose one entry */
public static async pickView(views: IModelConnection.ViewSpec[]): Promise<string> {
  // ...real ui code here showing view[].name list, returning chosenView...
  const chosenView = 0;

  // return the id of the chosen view
  return views[chosenView].id;
}

/** Load the list of spatial views from our iModel, let the user pick one, and return a Promise for the ViewState of the selected view. */
public static async loadOneView(): Promise<ViewState> {
  // first get the list of spatial views
  const views: IModelConnection.ViewSpec[] = await this.getSpatialViews();

  // ask the user to pick one from the list, returning its Id
  const viewId: string = await this.pickView(views);

  // return a promise for the ViewState of the selected view. Note that caller will have to await this method
  return this._iModel.views.load(viewId);
}
```

然后，您可能希望更改其中一个现有视图，以显示现在加载的视图的内容。例如，切换ViewManager.selectedView要显示它，请使用如下代码：

```
/** Show a list of spatial views, allow the user to select one, load its ViewState, and then change the selected ScreenViewport to show it. */
public static async showOneView(): Promise<void> {
  const viewstate = await this.loadOneView();
  const vp = IModelApp.viewManager.selectedView;
  if (undefined !== vp)
    vp.changeView(viewstate);
}
```

注意：在上面的示例中，getSpatialViews、loadOneView和showOneView是异步的，必须等待它们执行。

### 修改由二维视图显示的模型

Viewports始终显示一个ViewState。如果ViewState碰巧是ViewState2d，我们有时称之为“2d视图”。由于ViewState2d显示一个且只有一个2d模型，因此有时需要“切换模型”现有2d视图，而不是加载一个新的ViewState2d。

这个Viewport.changeViewedModel2d方法可用于实现此目的：

```
/** Change the displayed 2d Model of the selected view, if it is currently showing a 2d Model
   * @note the categories and displayStyle are unchanged. View is fitted to new model extents.
   */
public static async change2dModel(newModelId: Id64String): Promise<void> {
  const vp = IModelApp.viewManager.selectedView;
  if (undefined !== vp)
    return vp.changeViewedModel2d(newModelId, { doFit: true });
}
```











