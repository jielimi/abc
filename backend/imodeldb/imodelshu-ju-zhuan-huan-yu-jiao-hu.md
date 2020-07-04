## IModelExporter类

当ETL工作流程中的源数据包含在iModel中时，将使用IModelExporter和IModelExportHandler基类。尽管可以使用标准IModelDb API从iModel导出数据，但IModelExporter和IModelExportHandler基类提供以下功能：

1. 访客模式的实现，可以轻松地按规定的顺序迭代iModel，以尝试在依赖项之前访问依赖项/先决条件。
2. 使用IModelExporter.exportAll访问整个iModel。
3. 使用IModelExporter.exportChanges仅访问更改的实体。
4. 使用IModelExporter.exportModel，IModelExporter.exportModelContents或IModelExporter.exportElement访问iModel的子集。
5. 使用IModelExporter.excludeElementCategory，IModelExporter.excludeElementClass或。
6. IModelExporter.excludeElementAspectClass轻松排除某些实体类型以过滤导出内容。
7. 与IModelTransformer集成。

以下是使用IModelExporter和IModelExportHandler从iModel导出所有Code值的示例：

    import { CodeSpec } from "@bentley/imodeljs-common";
    import { Element, IModelDb, IModelExporter, IModelExportHandler, IModelJsFs as fs, SnapshotDb } from "@bentley/imodeljs-backend";

    /** CodeExporter creates a CSV output file containing all Codes from the specified iModel. */
    class CodeExporter extends IModelExportHandler {
      public outputFileName: string;

      /** Initiate the export of codes. */
      public static exportCodes(iModelDb: IModelDb, outputFileName: string): void {
        const exporter = new IModelExporter(iModelDb);
        const exportHandler = new CodeExporter(outputFileName);
        exporter.registerHandler(exportHandler);
        exporter.exportAll();
      }

      /** Construct a new CodeExporter */
      private constructor(outputFileName: string) {
        super();
        this.outputFileName = outputFileName;
      }

      /** Override of IModelExportHandler.onExportElement that outputs a line of a CSV file when the Element has a Code. */
      protected onExportElement(element: Element, isUpdate: boolean | undefined): void {
        const codeValue: string = element.code.getValue();
        if ("" !== codeValue) { // only output when Element has a Code
          const codeSpec: CodeSpec = element.iModel.codeSpecs.getById(element.code.spec);
          fs.appendFileSync(this.outputFileName, `${element.id}, ${codeSpec.name}, ${codeValue}\n`);
        }
        super.onExportElement(element, isUpdate);
      }
    }

## IModelImporter类

当ETL工作流程中的目标是iModel时，将使用IModelImporter基类。尽管可以使用标准IModelDb API将数据导入到iModel中，但IModelImporter类提供以下功能：

1. 当使用IModelImporter插入，更新或删除实体时，将进行回调。只需重写受保护的onInsert \*，onUpdate \*或onDelete \*方法。
2. （可选）在导入过程中自动扩展IModel.projectExtents
3. 与IModelTransformer集成

## IModelCloneContext类

ModelCloneContext类提供了iModel转换所需的核心克隆功能。它还维护sourceId-&gt;targetId映射，这是成功将Entity实例从源iModel克隆到目标iModel所必需的。iModel实体彼此高度相关。因此，克隆实体意味着复制对象图并将其源引用（Id）重新映射到其他目标实体。

## IModelTransformer类







