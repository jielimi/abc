# ECSchema

ECSchema是所有其他ECObject项的根容器，并为其包含的每个项提供名称空间。一个schema可以由另一个schema引用，但不能嵌入另一个schema内。因此，ECObjects中的名称空间没有层次结构。

#### 属性

**schemaName     **schema名称和schema各项的名称空间。在给定的系统中，ECName必须唯一，尽量避免缩写，方便人类阅读。

**alias       **当schemaName太长时可以使用alias\(别名\)以简化。其中，别名遵循与schema名称相同的命名规则：在给定的系统中必须保持唯一。如果别名与另一个别名冲突，将需要添加一个数字以确保在当前上下文中的唯一性。_注意：schema名称始终是唯一的，但是别名在某些情况下可能会更改。_

**version       **格式RR.WW.mm，即Read.Write.Minor。Read版本号增加表示无法使用旧schema读取新格式的数据；Write版本号增加表示仍然可以使用旧的schema读取数据，但无法写入数据。Minor版本号增加表示对schema的更改是完全不间断的。

**description       **对schema的可选且本地化的纯文本描述。

**displayLabel    **对schema的可选且本地化的纯文本描述。

**displayLabel    **用于在UI中显示的schema的可选且本地化的标签。

示例代码

依赖@bentley/ecschema-metadata 和@bentley/ecschema-locaters

```
    const SchemaFilePath = "SchemaA.02.00.02.ecschema.xml";
    const locater = new StubSchemaXmlFileLocater();
    const schema: Schema = locater.loadSchema(SchemaFilePath);//加载schema xml文件
    if (schema) {
    //查看schema属性
      console.log(schema.alias);
      console.log(schema.description);
      console.log(schema.readVersion);
      console.log(schema.writeVersion);
      console.log(schema.minorVersion);
    }
```

#### Sub-Elements

schema中可以包含以下内容：

| 项 | 描述 |
| :---: | :---: |
| ECSchemaReference | \(0..\*\) |
| ECCustomAttributes | \(0..1\) |
| ECEntityClass | \(0..\*\) |
| ECMixinClass | \(0..\*\) |
| ECStructClass | \(0..\*\) |
| ECCustomAttributeClass | \(0..\*\) |
| ECRelationshipClass | \(0..\*\) |
| ECEnumeration | \(0..\*\) |
| KindOfQuantity | \(0..\*\) |
| PropertyCategory | \(0..\*\) |

_注意：\(0..\*\)表示0个或者多个，\(0..1\)表示0个或者1个。_

# ECSchemaReference {#ecschemareference}

包含所有信息以标识引用的schema，不支持循环引用，这将导致无法以循环方式加载schema。

**属性**

**name   **被引用的ECSchema的名称,必须与引用schema的schema名称匹配。

**version   **被参考的ECSchema版本。使用“最新兼容匹配”来定位参考的schema，在该版本中，读取和写入版本必须匹配，并且所定位schema的次要版本必须等于或大于schema参考中列出的版本。

**alias  **从引用的schema引用项目时要使用的别名。此别名通常与引用的schema中定义的别名匹配，但是可以不同。如果不同，则仅在包含ECSchemaReference的schema的上下文中有效。

  


  




