# Element

_注意element在此译为元素，在imodel.js中用element表示元素类。_

元素是用于在iModel中对现实世界建模的最小可识别的构建基块。每个元素代表现实世界中的一个实体。元素集合\(包含在Model中\)用于对表示更大范围的真实世界实体的其他元素进行建模。使用这种递归建模策略，元素可以表示任何规模的实体，实体可以表示物理事物或抽象概念或仅仅是信息记录。

每个元素都有一个64位id\\(从Entity继承\\)，以在iModel中唯一标识，每个元素还具有一个“code”，以标识其在现实世界中的含义。此外，元素可能还具有“federationGuid”来保存GUID。iModel数据库保证id，code，federationGuid的唯一性。

元素可以拥有子元素，这对于建模装配关系或建模一个元素独占控制其他元素生命周期的情况非常有用。按照定义，一个元素可以0个或1个父元素。没有父元素的元素被认为是顶层元素。具有父元素的元素被认为是子元素。这些层次结构可以深入N层，这意味着元素可以同时包含父元素和子元素。

---

iModel.js中主要包含三类元素：

**PhysicalElement**：即物理元素，是一个空间定位的元素，有质量，并且可以被“触摸”。

**RoleElement**：角色元素，当一组外部环境定义了一个重要的角色（值得跟踪的角色），而该角色不是扮演该角色的实体的固有角色时，真实世界实体被建模为角色元素。例如，一个人可以扮演老师的角色，一块石头可以扮演界碑的角色。

**InformationContentElement**：信息内容元素，是建模纯信息实体的抽象基类，只有核心框架应该直接从信息内容元素子类化。行业和应用程序开发人员应该从该类最合适的子类开始使用。

_更多Element子类请参考源码Element.ts文件。_

# IModelDb.Elements

该类表示iModel数据文件中所有element的集合，使用该类可以对指定element执行创建，查询，更改，删除等具体操作。通过IModelDb.elements即可访问该接口。

其主要包含以下方法\(_**仅供参考，若需要了解更多，请查看相关源码，见文件IModelDb.d.ts或IModelDb.ts**_\):

---

```
//以JSON的形式从iModel读取元素数据
getElementJson<T extends ElementProps>(elementIdArg: string): T;

//通过Id，FederationGuid或代码获取Element的属性
getElementProps<T extends ElementProps>(elementId: Id64String | GuidString | Code | ElementLoadProps): T;

//通过Id，FederationGuid或代码获取Element的属性
tryGetElementProps<T extends ElementProps>(elementId: Id64String | GuidString | Code | ElementLoadProps): T | undefined;

//通过Id，FederationGuid或代码获取元素
getElement<T extends Element>(elementId: Id64String | GuidString | Code | ElementLoadProps): T;

//通过Id，FederationGuid或代码获取元素
tryGetElement<T extends Element>(elementId: Id64String | GuidString | Code | ElementLoadProps): T | undefined;

//查询具有指定代码的元素的ID。
queryElementIdByCode(code: Code): Id64String | undefined;

//查询指定元素的上次修改时间。
queryLastModifiedTime(elementId: Id64String): string;

//创建一个元素的新实例。
createElement<T extends Element>(elProps: ElementProps): T;

//将新元素插入到iModel中。
insertElement(elProps: ElementProps): Id64String;

//更新现有元素的某些属性。
updateElement(elProps: ElementProps): void;

//从此iModel中删除一个或多个元素。
deleteElement(ids: Id64Arg): void;

//查询指定元素的子元素。
queryChildren(elementId: Id64String): Id64String[];

//如果指定的Element具有子模型，则返回true。
hasSubModel(elementId: Id64String): boolean;

//获取根主元素
getRootSubject(): Subject;

//查询与此元素关联的特定类的方面（多态）。
getAspect(aspectInstanceId: Id64String): ElementAspect;

//获取指定元素拥有的ElementAspect实例。
getAspects(elementId: Id64String, aspectClassFullName?: string): ElementAspect[];

//将新的ElementAspect插入到iModel中。
insertAspect(aspectProps: ElementAspectProps): void;

//更新iModel中现有的ElementAspect。
updateAspect(aspectProps: ElementAspectProps): void;

//从此iModel删除一个或多个ElementAspects。
deleteAspect(aspectInstanceIds: Id64Arg): void;
```



