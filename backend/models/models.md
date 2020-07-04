# Model

_注意Model在此译为模型，在imodel.js中用Model表示元素类。_

#### 基本概念

模型是BIS模型的内存表示形式，模型是一个容器，用于在iModel中持久保存相关元素的集合。模型也是一种细分和组织整个存储库的方法，所有这些元素都是从单个视角进行的。那些元素共同地对某个实体建模，该实体比“模型”中包含的元素所建模的实体“更大”。例如，一个包含PhysicalElements的PhysicalModel，该PhysicalElements对汽车零件的物理形式进行建模。它们共同对整个汽车的物理实体进行建模。

---

#### 基本属性

Model是iModel中所有模型的基类，其基本属性如下所示:

| 属性 | 描述 |
| :---: | :---: |
| classFullName | 模型的ECClass,格式:Schema:ClassName |
| parentModel | 模型的父模型的Id |
| modeledElement | 模型的父模型 |

---

#### 核心模型类型

具体的核心模型都为Model的子类

| 核心模型子类 | 包含的元素类型 |
| :---: | :---: |
| PhysicalModel | PhysicalElements和SpatialLocationElements |
| SpatialLocationModel | SpatialLocationElements |
| DrawingModel | GeometricElement2d elements |
| DefinitionModel | DefinitionElements |
| InformationRecordModel | InformationRecordElements |
| GroupInformationModel | GroupInformationElements |
| DocumentListModel | Document element |

---

#### 基本接口

它具有查找模型ID和加载模型对象的方法。  
通常不需要将Model对象加载到内存中。  
模型对象不包含属性。  
模型的属性由关联的建模元素保留。  
IModelDb.Models.getSubModel和IModelDb.Models.tryGetSubModel是通过建模元素的ID，代码或Guid查找模型的便捷方法。  
Element.model是包含元素的模型的ID。

其主要包含以下方法\(_**仅供参考，若需要了解更多，请查看相关源码，见文件IModel.d.ts或IModel.ts**_\):

```
/** 将此模型插入到iModel中 */
insert(): string;
/**在iModel中更新此模型. */
update(): void;
/** 从iModel删除此模型. */
delete(): void;
```

# 



