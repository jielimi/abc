# Model

在BIS中，只有3种机制可用来创建层次结构：

1. 模型可以包含元素
2. 元素可以拥有子元素
3. 元素可以通过子模型建模

模型是元素的容器，模型是一种细分和组织整个存储库的方法。所有这些元素都是从单个视角进行的。那些元素共同地对某个实体建模，该实体比“模型”中包含的元素所建模的实体“更大”。例如，一个包含PhysicalElements的PhysicalModel，该PhysicalElements对汽车零件的物理形式进行建模。它们共同对整个汽车的物理实体进行建模。

# IModelDb.Models

该类表示iModel数据文件中所有model的集合，使用该类可以对指定model执行创建，查询，更改，删除等具体操作。

通过IModelDb.models即可访问该接口。

其主要包含以下方法\(_**仅供参考，若需要了解更多，请查看相关源码，见文件IModelDb.d.ts或IModelDb.ts**_\):

---

```js
//获取具有指定标识符的ModelProps。
getModelProps<T extends ModelProps>(modelId: Id64String): T

//获取具有指定标识符的ModelProps。
tryGetModelProps<T extends ModelProps>(modelId: Id64String): T | undefined

//查询指定模型的上次修改时间。
queryLastModifiedTime(modelId: Id64String): string

//获取具有指定标识符的模型。
getModel<T extends Model>(modelId: Id64String): T

//获取具有指定标识符的模型。
tryGetModel<T extends Model>(modelId: Id64String): T

//将模型的属性读取为json字符串。
getModelJson(modelIdArg: string): string

//将模型的属性读取为json字符串。
tryGetModelJson(modelIdArg: string): string | undefined

//获取指定Element的子模型。
getSubModel<T extends Model>(modeledElementId: Id64String | GuidString | Code): T

//获取指定Element的子模型。
tryGetSubModel<T extends Model>(modeledElementId: Id64String | GuidString | Code): T | undefined

//在内存中创建一个新模型。
createModel<T extends Model>(modelProps: ModelProps): T

//插入新模型。
insertModel(props: ModelProps): Id64String

//更新现有模型。
updateModel(props: UpdateModelOptions): void

//删除一个或多个现有模型。
deleteModel(ids: Id64Arg): void
```



