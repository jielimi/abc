## IModelExporter类

当ETL工作流程中的源数据包含在iModel中时，将使用IModelExporter和IModelExportHandler基类。尽管可以使用标准IModelDb API从iModel导出数据，但IModelExporter和IModelExportHandler基类提供以下功能：

1.  访客模式的实现，可以轻松地按规定的顺序迭代iModel，以尝试在依赖项之前访问依赖项/先决条件。
2.  使用IModelExporter.exportAll访问整个iModel。
3.  使用IModelExporter.exportChanges仅访问更改的实体。
4.  使用IModelExporter.exportModel，IModelExporter.exportModelContents或IModelExporter.exportElement访问iModel的子集。
5.  使用IModelExporter.excludeElementCategory，IModelExporter.excludeElementClass或。
6. IModelExporter.excludeElementAspectClass轻松排除某些实体类型以过滤导出内容。
7.  与IModelTransformer集成。

  


  


以下是使用IModelExporter和IModelExportHandler从iModel导出所有Code值的示例：

