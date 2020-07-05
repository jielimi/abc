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
| Points | Point是ECSchemas中的内置基本类型，在ECSQL中也支持。 |
| Structs | 在ECSQL中,您可以整体引用结构ECProperty,也可以仅引用其某些成员。在ECSQL中引用结构成员的运算符为“.”。 |
| Arrays | 在ECSQL中，您只能整体引用Array ECProperties。 |

_备注:_

_DATE 'yyyy-mm-dd'    
_

_TIMESTAMP 'yyyy-mm-dd hh:mm:ss\[.nnn\]\[Z\]'    
_

_TIME 'hh:mm:ss\[.nnn\]'_

在ECSQL Point的上下文中，ECProperty解释为由以下系统属性组成的结构：

X     X Point2d或Point3d的坐标

Y     Y Point2d或Point3d的坐标

Z     Z Point3d的坐标

---

Boolean示例:

```
//使用True和False
SELECT ECInstanceId, Model, CodeValue FROM bis.ViewDefinition3d WHERE IsCameraOn = True
SELECT ECInstanceId, Model, CodeValue FROM bis.ViewDefinition3d WHERE IsCameraOn = False
//布尔属性或表达式不需要与True和False比较，因为它们已经返回了布尔值。 所以上面的例子也可以这样写：
SELECT ECInstanceId, Model, CodeValue FROM bis.ViewDefinition3d WHERE IsCameraOn
SELECT ECInstanceId, Model, CodeValue FROM bis.ViewDefinition3d WHERE NOT IsCameraOn
```

---

Date示例:

    <ECEntityClass typeName="CalenderEntry">
      <ECProperty propertyName="startTime" typeName="dateTime">
        <ECCustomAttributes>
          <DateTimeInfo xmlns="CoreCustomAttributes.01.00.01">
            <DateTimeComponent>TimeOfDay</DateTimeComponent>
          </DateTimeInfo>
        </ECCustomAttributes>
      </ECProperty>
      <ECProperty propertyName="endTime" typeName="dateTime">
        <ECCustomAttributes>
          <DateTimeInfo xmlns="CoreCustomAttributes.01.00.01">
            <DateTimeComponent>TimeOfDay</DateTimeComponent>
          </DateTimeInfo>
        </ECCustomAttributes>
      </ECProperty>
    </ECEntityClass>

    SELECT ECInstanceId, Model, CodeValue FROM bis.ViewDefinition3d WHERE IsCameraOn = True
    SELECT ECInstanceId, Model, CodeValue FROM bis.Element WHERE LastMod > DATE '2018-01-01'
    SELECT ECInstanceId, Model, CodeValue FROM bis.Element WHERE LastMod < TIMESTAMP '2017-07-15T12:00:00.000Z'`
    SELECT ECInstanceId, Model, CodeValue FROM bis.Element WHERE LastMod BETWEEN :startperiod AND :endperiod`
    SELECT ECInstanceId FROM myschema.CalenderEntry WHERE startTime >= TIME '08:30:00' AND startTime <= TIME '09:00:00'

---

Point示例:

```
SELECT ECInstanceId, Model, CodeValue FROM bis.GeometricElement3d
WHERE Origin.X BETWEEN 3500000.0 AND 3500500.0 AND
Origin.Y BETWEEN 5700000.0 AND 5710000.0 AND
Origin.Z BETWEEN 0 AND 100.0
```

---

Sturcts示例:

```
<ECStructClass typeName="Address">
  <ECProperty propertyName="Street" typeName="string" />
  <ECProperty propertyName="City" typeName="string" />
  <ECProperty propertyName="Zip" typeName="int" />
</ECStructClass>
<ECEntityClass typeName="Company">
  <ECProperty propertyName="Name" typeName="string" />
  <ECArrayProperty propertyName="Location" typeName="Address" />
</ECEntityClass>

SELECT Location FROM myschema.Company WHERE Name='ACME'//整体返回Location struct属性
SELECT Name,Location.Street,Location.City FROM myschema.Company WHERE ECInstanceId=?//返回Location结构属性的Street和City成员
SELECT Name FROM myschema.Company WHERE Location=?//返回与绑定的Location值匹配的行。 该位置必须作为一个整体进行绑定。
SELECT Name FROM myschema.Company WHERE Location.Zip=12314//返回与位置的Zip成员值匹配的行
```

Array示例:

```
<ECEntityClass typeName="Company">
  <ECProperty propertyName="Name" typeName="string" />
  <ECArrayProperty propertyName="PhoneNumbers" typeName="string" />
</ECEntityClass>

SELECT PhoneNumbers FROM myschema.Company WHERE Name='ACME'//返回ACME公司的PhoneNumbers数组
SELECT Name FROM myschema.Company WHERE PhoneNumbers=?//返回与绑定的PhoneNumber数组匹配的公司。 该数组必须绑定为一个整体。
```

### 导航属性

导航属性是指向相关对象的ECProperty.它们始终由ECRelationshipClass支持。在ECSQL的上下文中，导航属性被解释为由以下系统属性组成的结构：

| 属性 | 描述 |
| :---: | :---: |
| Id | 相关实例的ECInstanceId |
| RelECClassId | 支持导航属性的ECRelationshipClass的ECClassId。当ECRelationshipClass具有子类时,它与其相关。 |

示例:

```
SELECT Parent FROM bis.Element WHERE ECInstanceId=?//整体返回Parent导航属性（包括Id和RelECClassId）
SELECT Parent.Id FROM bis.Element WHERE ECInstanceId=?//仅返回父级导航属性的Id成员
SELECT Parent.Id, Parent.RelECClassId FROM bis.Element WHERE ECInstanceId=?//ECInstanceId =？ 以两个单独的列的形式返回ID和Parent导航属性的RelECClassId成员
```

### ECRelationshipClasses

由于ECRelationshipClasses也是ECClass，因此可以像ECClasses一样在ECSQL中使用它们。这些系统属性表示它们的附加关系语义。

| 属性 | 描述 |
| :---: | :---: |
| SourceECInstanceId | 关系的源端上的实例的ECInstanceId |
| SourceECClassId | 关系的源端上的实例的ECClassId |
| TargetECInstanceId | 关系目标端上的实例的ECInstanceId |
| TargetECClassId | 关系的目标端上的实例的ECClassId |

_备注:如果ECRelationshipClass由Navigation属性支持，则在ECSQL中使用Navigation属性通常比ECRelationshipClass容易得多。执行SELECT \* FROM语句或不带属性名称列表的INSERT INTO语句时，将跳过SourceECClassId和TargetECClassId。_

示例:

```
//返回驱动绑定到第一个参数的元素的所有元素的ECInstanceId
SELECT SourceECInstanceId FROM bis.ElementDrivesElement WHERE TargetECInstanceId=? AND Status=?

//返回绑定到参数的Model所包含的所有Elements的ECInstanceId和ECClassId
SELECT TargetECInstanceId,TargetECClassId FROM bis.ModelHasElements WHERE SourceECInstanceId=?
```

### Joins

ECClass之间的连接使用标准SQL连接语法（JOIN ... ON ...或theta样式）指定。在ECSchemas中，ECRelationshipClasses用于关联两个ECClass。 因此，ECRelationshipClasses可以看作是这两个类之间的虚拟链接表。 如果要通过它们的ECRelationshipClass加入两个ECClass，则需要将第一个类加入关系类，然后再将关系类加入第二个类。如果为ECRelationship类定义了导航属性，请使用导航属性代替联接。

示例:

```
//没有导航属性（需要2个JOIN）：
SELECT e.CodeValue,e.UserLabel FROM bis.Element driver JOIN bis.ElementDrivesElement ede ON driver.ECInstanceId=ede.SourceECInstanceId JOIN bis.Element driven ON driven.ECInstanceId=ede.TargetECInstanceId WHERE driven.ECInstanceId=? AND ede.Status=?

//具有导航属性（Element.Model）：
//返回具有指定条件（需要1 JOIN）的Model中所有元素的CodeValue和UserLabel：
SELECT e.CodeValue,e.UserLabel FROM bis.Element e JOIN bis.Model m ON e.Model.Id=m.ECInstanceId WHERE m.Name=?
//返回具有指定条件的元素的模型（无需连接）：
SELECT Model FROM bis.Element WHERE ECInstanceId=?
```

### 多态查询

默认情况下，对ECSQL的FROM子句中的任何ECClass进行多态处理，即也考虑其所有子类。 如果对ECClass进行非多态处理，即仅考虑类本身而不考虑其子类，则在其前面添加ONLY关键字。这也适用于Mixins。 Mixins从技术上讲是ECClass（准确地说是抽象实体ECClass）。 因此，您可以简单地针对mixin类进行查询，而无需知道哪些类实际实现了mixin。

示例:

    `SELECT ECInstanceId FROM bis.Element WHERE Model=?``//返回指定模型中任何子类的所有元素返回指定模型中任何子类的所有元素
    `SELECT ECInstanceId FROM bis.SpatialViewDefinition WHERE ModelSelector=?``//为指定的ModelSelector返回SpatialViewDefinitions行及其子类的行
    `SELECT ECInstanceId FROM ONLY bis.SpatialViewDefinition WHERE ModelSelector=?``//仅返回指定ModelSelect的SpatialViewDefinitions行，而不返回其子类的行。



