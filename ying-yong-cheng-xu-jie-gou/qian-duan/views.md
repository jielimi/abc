# Using Views in iModel.js {#using views in imodel.js}

视图在web浏览器中渲染来自iModel的一个或多个模型的几何体。iModel.js应用程序可以通过htmldivelment在网页上的任何位置嵌入视图并与之交互。

视图由ViewManager类管理，使用IModelApp.viewManager。

多个视图可以在同一个网页上同时可见，每个视图都有自己的htmldivelment，并由ViewManager协调。

### ViewDefinition Elements

视图作为ViewDefinition类的元素保存在iModel中。ViewDefinitions包含在会话中显示相同内容所需的所有信息。这包括相机位置、显示的模型、类别选择器、要使用的显示样式，以及任何其他特定于视图的设置。

### The ViewState Class

ViewDefinition类（实际上所有元素类）只存在于后端，因为它们的目的是在iModel中读写这些元素。在前端，对显示视图所需的元素的访问由ElementState类提供。ElementState类只保存元素的状态，而不保存从数据库中读写元素的方法。

通过将ViewDefinition加载到ViewState对象中来打开视图。他们开始显示保存在iModel中的内容，但用户可以使用查看工具修改所看到的内容。这些更改只是临时的（在内存中），除非通过将它们保存回iModelIModelDb.Elements.updateElement.

ViewState对象在前端保存ViewDefinition（在视图中显示的内容）的状态。内存中ViewState的实例保存对其他几个对象的引用，包括CategorySelectorState、DisplayStyle3dState和ModelSelectorState（用于空间视图）。由于这些对象中的每一个都必须异步加载到前端，因此有一个异步方法称为IModelConnection.Views.load当ViewState和显示视图所需的所有其他状态对象就绪时，返回一个promise。Viewport类需要加载的ViewState对象。

### Types of ViewDefinitions

ViewDefinition的子类以各种方式显示不同类型的模型。以下是几个重要的子类：

| 类名 | 描述 |
| :--- | :--- |
| SpatialViewDefinition | 显示一个或多个三维空间模型的视图 |
| DrawingViewDefinition | 显示单个二维绘图模型的视图 |
| SheetViewDefinition | 显示单个二维图纸模型的视图 |

对于xxxViewDefinition的每个子类，前端都有一个相应的xxxViewState类。

