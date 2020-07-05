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



