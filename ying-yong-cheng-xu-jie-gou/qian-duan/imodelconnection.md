# IModelConnection

前端用来访问iModel的主要类\(应用程序的前端不会直接打开briefcase\(存放iModel副本的文件。它包含来自变更集和本地变更的数据。只要修改briefcase，就会创建变更集，并反映一段时间内所有添加、删除和修改的联合。\) ，而是远程“连接”到由后端管理的briefcase 。\)

## Classes

| name | description |
| :--- | :--- |
| IModelConnection | 托管于后端的IModelDb的连接 |
| IModelConnection.CodeSpecs | IModelConnection的代码规范实体的集合 |
| IModelConnection.Elements | IModelConnection的元素集合 |
| IModelConnection.Models | IModelConnection中已加载的ModelState对象的集合 |
| IModelConnection.Views | IModelConnection的视图集合 |
| RemoteBriefcaseConnection | 到托管于远程后端BriefcaseDb数据库的连接，通常用于web应用程序 |
| SnapshotConnection | 到托管于后端的SnapshotDb的连接 |
| SnapshotConnection.CodeSpecs | IModelConnection的代码规范实体的集合 |
| SnapshotConnection.Elements | IModelConnection的元素集合 |
| SnapshotConnection.Models | 为IModelConnection加载的ModelState对象的集合 |
| SnapshotConnection.Views | IModelConnection的视图集合 |
| SnapshotConnection.Views | IModelConnection的视图集合 |
| Tiles | 提供对与IModelConnection关联的tileTree的访问 |



