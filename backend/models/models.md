# Model

_注意Model在此译为模型，在imodel.js中用Model表示元素类。_

模型是一个容器，用于在iModel中持久保存相关元素的集合。模型也是一种细分和组织整个存储库的方法，所有这些元素都是从单个视角进行的。那些元素共同地对某个实体建模，该实体比“模型”中包含的元素所建模的实体“更大”。例如，一个包含PhysicalElements的PhysicalModel，该PhysicalElements对汽车零件的物理形式进行建模。它们共同对整个汽车的物理实体进行建模。

#### 基本概念

模型是一个容器，用于在iModel中持久保存相关元素的集合。模型也是一种细分和组织整个存储库的方法，所有这些元素都是从单个视角进行的。那些元素共同地对某个实体建模，该实体比“模型”中包含的元素所建模的实体“更大”。例如，一个包含PhysicalElements的PhysicalModel，该PhysicalElements对汽车零件的物理形式进行建模。它们共同对整个汽车的物理实体进行建模。

---

#### 基本属性

| 属性 | 描述 |
| :---: | :---: |
| classFullName | 模型的ECClass,格式:Schema:ClassName |
| parentModel | 模型的父模型的Id |
| modeledElement | 模型的父模型 |

1. ---
2. 核心模型类型
3. 基本接口

# 



