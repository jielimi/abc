# ViewManager（视图管理器）

Viewport类负责显示由其ViewState定义的视图。但是，通常显示视图的目的是允许用户修改视图本身，或者与其内容交互。为了实现这一点，需要通过将浏览器的事件系统与Viewports连接起来IModelApp.viewManager.

```
/** Open a Viewport on the supplied div element. */
public static async openView(viewDiv: HTMLDivElement) {
  const viewState = await this.loadOneView();
  const viewPort = ScreenViewport.create(viewDiv, viewState);
  IModelApp.viewManager.addViewport(viewPort);
}
```

将视口添加到ViewManager后，其画布的所有HTML事件都由ToolAdmin定向到活动工具类。

### The "Selected" View

有时需要从代码内部选择一个对用户输入做出反应的视口。如果没有其他方法来确定要使用哪个视口，iModel.js应用程序通常默认为ViewManager.selectedView. 这将是用户单击的最后一个屏幕视口。ViewManager.selectedView通常是工具的目标视口。

`注意：如果只有一个视口可见，则该视口将始终是ViewManager.selectedView. 如果没有可见的视口，ViewManager.selectedView可以是未定义的。`

## Viewing Tools（视图工具）

iModel.js库提供的控件允许用户通过ViewTool类修改视图中显示的内容。您可以创建所提供类的实例（例如WindowAreaTool、FitViewTool、WalkViewTool、RotateViewTool等），也可以为特殊的查看操作创建自己的子类。

### View Decorators（视图装饰器）

Viewport类负责在视图中显示持久数据（例如模型、真实数据、地图等）。然而，通常工具希望显示额外的、非持久的信息，以传达上下文或引起对感兴趣的部分内容的注意。这是通过视图装饰器实现的。



