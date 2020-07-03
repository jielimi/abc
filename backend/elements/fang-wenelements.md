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

---

# 查询Element示例

根据元素Id可以从iModel数据文件中查询到指定的元素\(如果存在\)。具体查询方式如下所示：

```js
查询元素方式一
const elementId = "0x4a";//元素Id
const e = this.imodelDb.elements.tryGetElement(elementId);
if (e) {
    //显示元素的基本特性;
    console.log(e.model); //显示包含此元素的模型的id。
    console.log(e.code.value); //显示此元素的code的codevalue值。
    console.log(e.classFullName); //显示此元素的ECClassFullName。

    //显示元素的特有属性，首先需要将element向下转换到指定的子类。
    const e2: DisplayStyle3d = e as DisplayStyle3d;
      if (e2) {
        const set = e2.settings;
        console.log(set.lights.numCels);
        console.log(set.backgroundColor.name);
      }
}

//查询元素方式二
const elementId = "0x4a";//元素Id
const e: DisplayStyle3d | undefined = this.imodelDb.elements.tryGetElement<DisplayStyle3d>(elementId);
if (e) {
    //显示元素的基本特性;
    console.log(e.model); //显示包含此元素的模型的id。
    console.log(e.code.value); //显示此元素的code的codevalue值。
    console.log(e.classFullName); //显示此元素的ECClassFullName。

    //显示元素的特有属性。
    const set = e2.settings;
    console.log(set.lights.numCels);
    console.log(set.backgroundColor.name);
}
```



