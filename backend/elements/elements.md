# Element

_注意element在此译为元素，在imodel.js中用element表示元素类。_

#### 基本概念

一个BIS元素代表了现实世界种的一个实体，例如泵，梁，合同，公司，流程，要求，文件，人员等。元素是用于在iModel中对现实世界建模的最小可识别的构建基块。每个元素代表现实世界中的一个实体。元素集合\(包含在Model中\)用于对表示更大范围的真实世界实体的其他元素进行建模。使用这种递归建模策略，元素可以表示任何规模的实体，实体可以表示物理事物或抽象概念或仅仅是信息记录。

每个元素都有一个64位id\(从Entity继承\)，以在iModel中唯一标识，每个元素还具有一个“code”，以标识其在现实世界中的含义。此外，元素可能还具有“federationGuid”来保存GUID。iModel数据库保证id，code，federationGuid的唯一性。

元素可以拥有子元素，这对于建模装配关系或建模一个元素独占控制其他元素生命周期的情况非常有用。按照定义，一个元素可以0个或1个父元素。没有父元素的元素被认为是顶层元素。具有父元素的元素被认为是子元素。这些层次结构可以深入N层，这意味着元素可以同时包含父元素和子元素。

---

#### 基本属性

Element类是iModel中所有元素的基类，其基本属性如下所示:

| 属性 | 描述 |
| :---: | :---: |
| model | 包含此元素的模型的ID |
| code | 元素的code |
| classFullName | 元素的ECClass，格式：Schema:ClassName |
| RelatedElement | 元素的父元素\(如果存在\) |

#### 基本种类

iModel.js中主要包含三类元素：  
**PhysicalElement**：即物理元素，是一个空间定位的元素，有质量，并且可以被“触摸”。

**RoleElement**：角色元素，当一组外部环境定义了一个重要的角色（值得跟踪的角色），而该角色不是扮演该角色的实体的固有角色时，真实世界实体被建模为角色元素。例如，一个人可以扮演老师的角色，一块石头可以扮演界碑的角色。

**InformationContentElement**：信息内容元素，是建模纯信息实体的抽象基类，只有核心框架应该直接从信息内容元素子类化。行业和应用程序开发人员应该从该类最合适的子类开始使用。

_更多Element子类请参考源码Element.ts文件。_

---

#### 基本接口

iModel.js元素是BIS元素的内存表示形式。使用Element对象可以轻松访问一组属性和方面。IModelDb.elements表示iModel中Elements的集合。每个iModel都包含一个“ root” Subject元素，它是所有分区的父级。可通过名为IModelDb.Elements.getRootSubject的特殊函数来访问它。您可以通过各种方式查找所有其他元素。如BIS元素基础中所述，元素由唯一ID标识，并且可能还具有代码和/或FederationGuid。如果您知道这些标识符之一，则可以非常有效地查找元素。IModelDb.Elements.getElement方法使此操作变得容易。您可以使用ECSQL查询其他属性或空间查询来发现元素ID。

其主要包含以下方法\(_**仅供参考，若需要了解更多，请查看相关源码，见文件Element.d.ts或IElement.ts**_\):

```
//获取此元素的显示标签。 默认情况下返回userLabel（如果存在），否则返回代码值。
getDisplayLabel(): string;
//将此元素插入到iModel中。
insert(): string;
//在iModel中更新此元素。
update(): void;
//从iModel删除此元素。
delete(): void;
```

# 



