# IModelDb.Views

该类表示iModel数据文件中所有view的集合，使用该类可以对指定view执行相关具体操作。

通过IModelDb.views即可访问该接口。

主要包含以下方法\(_**仅供参考，若需要了解更多，请查看相关源码，见文件IModelDb.d.ts或IModelDb.ts**_\):

---

```
//查询指定类的ViewDefinitionProps数组，并与指定的IsPrivate设置匹配。
queryViewDefinitionProps(className?: string, limit?: number, offset?: number, wantPrivate?: boolean): ViewDefinitionProps[];

//迭代所有与提供的查询匹配的ViewDefinition。
iterateViews(params: ViewQueryParams, callback: (view: ViewDefinition) => boolean): boolean;

//查询指定的viewDefinitionId的ViewStateProps
 getViewStateData(viewDefinitionId: string): ViewStateProps;

//获取视图的缩略图。
getThumbnail(viewDefinitionId: Id64String): ThumbnailProps | undefined;

//保存视图的缩略图。
saveThumbnail(viewDefinitionId: Id64String, thumbnail: ThumbnailProps): number;

//设置iModel的默认视图属性
setDefaultViewId(viewId: Id64String): void;
```



