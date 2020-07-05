# ECSQL

ECSQL是基于文本的命令语言，用于对iModel或ECDb文件中的业务数据进行CRUD（创建，读取，更新，删除）操作。ECSQL是SQL的一种实现，SQL是一种行之有效的，被广泛采用的基于文本的命令语言。它尽可能地遵守标准SQL（SQL-92和SQL-99）。尤其是SQL-99标准还具有ECSchemas的许多功能：布尔值，日期时间，二进制数据类型，结构，数组，多态性。这使得ECSQL仅在极少数例外情况下偏离标准SQL。任何熟悉SQL的人都应该直观地理解ECSQL。ECSQL和SQL之间的主要区别在于ECSQL的目标是逻辑schema，而不是基础数据库的持久性schema。

![](/assets/CSQL.png)

以下所有的ECSQL示例均引用BisCore ECSchema中的类和关系（除非另有说明）。:

注意：ECSQL中使用的类必须通过其schema完全限定，语法:&lt;Schema name or alias&gt;.&lt;Class name&gt;

也可以使用‘ : ’作为schema和类名之间的分隔符。

以下代码是等效的:

```
SELECT Model, CodeValue, Parent FROM BisCore.Element
//这个使用schema别名：
SELECT Model, CodeValue, Parent FROM bis.Element
```

### ECSQL参数

在准备好后将值绑定到ECSQL语句时，支持以下参数占位符。

| 参数类型 | 描述 |
| :---: | :---: |
| ? | 位置参数, 它的索引比ECSQL语句中的上一个参数大1。 |
| :aaa | 命名参数，这允许将相同的值绑定到多个占位符。 |

示例:

```
SELECT ECInstanceId FROM bis.GeometricElement3d WHERE Model=? AND LastMod>=?
SELECT ECInstanceId FROM bis.GeometricElement3d LIMIT :pagesize OFFSET (:pageno * :pagesize)
```

### ECInstanceId and ECClassId

ECSQL定义了一组内置系统属性,它们不必在ECSchemas中定义。

| 属性 | 描述 |
| :---: | :---: |
| ECInstanceId | 是ECInstance的唯一标识符。 |
| ECClassId | 引用ECClass的ECClassId，它在iModel中唯一地标识ECClass。 |

示例：

```
SELECT Parent, ECClassId FROM bis.Element WHERE ECInstanceId=123
```

### ECSQL中的基本数据类型

ECSQL支持EC内置的所有原始类型。这意味着，除了SQL-92中的基本数字和字符串数据类型外，ECSQL还支持布尔值，BLOB，日期时间和点。

| 类型 | 描述 |
| :--- | :--- |
| Boolean | 对于布尔类型，ECSQL支持文字True和False。 |
| DateTime | 无时间日期DATE 有时间日期TIMESTAMP 无日期时间TIME |
| Basic functions | CURRENT\_DATE CURRENT\_TIMESTAMP CURRENT\_TIME |
| Points  | Point是ECSchemas中的内置基本类型，在ECSQL中也支持。 |
| Structs | 在ECSQL中,您可以整体引用结构ECProperty,也可以仅引用其某些成员。在ECSQL中引用结构成员的运算符为“.”。 |
| Arrays | 在ECSQL中，您只能整体引用Array ECProperties。 |



