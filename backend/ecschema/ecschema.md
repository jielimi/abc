# ECSchema

ECSchema是所有其他ECObject项的根容器，并为其包含的每个项提供名称空间。一个schema可以由另一个schema引用，但不能嵌入另一个schema内。因此，ECObjects中的名称空间没有层次结构。

---

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

---

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

---

# ECSchemaReference {#ecschemareference}

包含所有信息以标识引用的schema，不支持循环引用，这将导致无法以循环方式加载schema。

**属性**

**name   **被引用的ECSchema的名称,必须与引用schema的schema名称匹配。

**version   **被参考的ECSchema版本。使用“最新兼容匹配”来定位参考的schema，在该版本中，读取和写入版本必须匹配，并且所定位schema的次要版本必须等于或大于schema参考中列出的版本。

**alias  **从引用的schema引用项目时要使用的别名。此别名通常与引用的schema中定义的别名匹配，但是可以不同。如果不同，则仅在包含ECSchemaReference的schema的上下文中有效。

# ECClass {#ecclass}

#### 基本概念

**ECObject**中有5种类型的**ECClass**，**ECEntityClass**，**ECMixinClass**，**ECStructClass**，**ECCustomAttributeClass**和**ECRelationshipClass**。

###### 每种类类型都对不同类型的对象建模。

**ECEntityClass **对业务对象进行建模，这些业务对象可以单独实例化并具有一个ID。

**ECStructClass **对复杂的属性类型进行建模，通常称为结构。

**ECCustomAttributeClass **对应用于其他架构元素以提供其他元数据的对象进行建模。

**ECRelationshipClass **对 **ECEntityClass **之间的连接进行建模。

所有类都在其自己的类类型中支持继承。

因此，一个**ECEntityClass**可以将另一个**ECEntityClass**作为其基类，但是不能将**ECStructClass**作为其基类。

**ECRelationshipClass**仅支持单继承，而**ECEntityClass**支持使用'mixins'的有限形式的多继承。

#### 通用属性

**typeName **定义此ECClass的名称。必须是有效的ECName，并且在schame中的所有其他项中必须唯一。

**description  **面向用户的类描述，已本地化，并可能显示在UI中。

**displayLabel **本地化的显示标签，将代替GUI中的名称使用。如果未设置，将使用类的类型名称。

**modifier **将类标识为抽象或密封。

              有效选项包括：

                        1.无（默认）–普通的，可实例化的类。对于ECRelationshipClass类型无效。

                        2.抽象–抽象类，无法实例化。

                        3.密封的–普通的，可实例化的类，但不能用作基础类或有子类



