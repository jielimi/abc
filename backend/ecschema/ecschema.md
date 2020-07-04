# ECSchema

ECSchema是所有其他ECObject项的根容器，并为其包含的每个项提供名称空间。一个schema可以由另一个schema引用，但不能嵌入另一个schema内。因此，ECObjects中的名称空间没有层次结构。

属性

**schemaName **schema名称和schema各项的名称空间。在给定的系统中，ECName必须唯一，尽量避免缩写，方便人类阅读。

**alias **当schemaName太长时可以使用alias\(别名\)以简化。其中，别名遵循与schema名称相同的命名规则：在给定的系统中必须保持唯一。如果别名与另一个别名冲突，将需要添加一个数字以确保在当前上下文中的唯一性。_注意：schema名称始终是唯一的，但是别名在某些情况下可能会更改。_

