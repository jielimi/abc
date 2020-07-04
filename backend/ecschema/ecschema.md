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



