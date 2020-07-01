## 打开iModelBank模型：

`IModelConnection.open`

`通过ScreenViewport.create()创建一个viewport`

`通过IModelApp.viewManager.addViewport(this.theViewPort);将创建的的viewport添加到渲染列表中`



IModelConnection: 前端用来访问iModel的主要类\(应用程序的前端不会直接打开briefcase\(存放iModel副本的文件。它包含来自变更集和本地变更的数据。只要修改briefcase，就会创建变更集，并反映一段时间内所有添加、删除和修改的联合。\) ，而是远程“连接”到由后端管理的briefcase 。\)

IModelApp: 使用IModelApp进行前端管理

IModelApp的实例提供（ViewManager管理图形视图，Tools工具和绘图辅助工具等）一系列前端所需要的服务。

viewManager: 视图管理器

保存打开的视图列表，并且提供打开，关闭视图等操作方法：

打开视图：viewManager.addViewport\(\);

关闭视图：viewManager.dropViewport\(\);

