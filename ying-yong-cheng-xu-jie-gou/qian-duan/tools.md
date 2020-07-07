# iModel.js Tools {#imodel.js tools}

代表用户执行操作的JavaScript类。有两个主要的工具类别，即时工具和交互工具。

### Immediate Tools

即时工具立即执行分配的任务，无需进一步输入。它们不会成为活动工具，而是作为工具的直接子类实现。

### Interactive Tools

有三种交互式工具分类，每种分类都是通过将InteractiveTool子类化来实现的，以最好地服务于特定的目的。

| name | description |
| :--- | :--- |
| ViewTool | 用于实现诸如平移、缩放和旋转等查看操作。执行时暂停激活的工具，完成后恢复激活的工具，前端包提供了一套全面的查看工具；大多数iModel.js应用程序不需要实现自己的 |
| InputCollector | 用于通过捕捉或定位iModel中的元素来收集当前基本体工具的输入。 |
| PrimitiveTool | 用于与iModel的图形交互的基本工具。当被调用时，它们成为活动工具，对用户输入（如数据点、鼠标移动、触摸、击键和重置）做出反应。 |

如何编写一个PrimitiveTool，参考[https://www.imodeljs.org/learning/frontend/primitivetools/](https://www.imodeljs.org/learning/frontend/primitivetools/)

## Classes

| name | description |
| :--- | :--- |
| ExtensionTool | 一种立即启动加载进程的工具iModel.js扩展。 |
| FitViewTool |  |
| FlyViewTool |  |
| FuzzySearch | 模糊搜索。 |
| FuzzySearchResults | 返回模糊搜索的结果。 |
| IdleTool |  |
| InteractiveTool |  |
| LookAndMoveTool | 使用鼠标+键盘或触摸控制执行漫游操作的工具。 |
| LookViewTool |  |
| panViewTool |  |
| PrimitiveTool | PrimitiveTool类可用于实现创建或修改几何元素的工具。 |
| RotateViewTool | 执行旋转视图操作的工具。 |
| ScrollViewTool | 执行滚动操作的工具。 |
| StandardViewTool | 将视图旋转到标准视图之一的工具。 |
| ViewManip | 操纵视区视锥的工具的基类。 |
| ViewRedoTool | 执行视图重做操作的工具。 |
| ViewToggleCameraTool | 在空间视图中打开/关闭相机的工具。 |
| ViewTool | 操纵视图的交互式工具。 |
| ViewUndoTool | 执行视图撤消操作的工具。 |
| WalkViewTool | 执行漫游操作的工具。 |
| WindowAreaTool | 执行窗口区域视图操作的工具。 |
| ZoomViewTool | 执行缩放操作的工具。 |



