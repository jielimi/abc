## SelectionSet

当前为IModelConnection选择的一组元素。选定元素在视口中以可自定义的hilite效果显示。

参考：[https://www.imodeljs.org/reference/imodeljs-common/rendering/hilite/hilite.settings/](https://www.imodeljs.org/reference/imodeljs-common/rendering/hilite/hilite.settings/) 查看hilite效果的定制。

##### Methods

| name | description |
| :--- | :--- |
| constructor\(iModel: IModelConnection\): SelectionSet | 构造函数。 |
| add\(elem: Id64Arg\): boolean | 向当前选择集中添加一个或多个ID。 |
| addAndRemove\(adds: Id64Arg, removes: Id64Arg\): boolean | 添加一组ID，然后删除另一组ID。 |
| emptyAll\(\): void | 清除当前选择集。 |
| has\(elemId?: string\): boolean | 如果elemId在此SelectionSet中，则返回true。 |
| invert\(elem: Id64Arg\): boolean | 在SelectionSet中反转一组ID的状态 |
| isSelected\(elemId?: Id64String\): boolean | 查询Id是否在选择集中。 |
| remove\(elem: Id64Arg\): boolean | 从当前选择集中删除一个或多个ID。 |
| replace\(elem: Id64Arg\): void | 将选择集更改为给定的ID集。 |

##### Properties

| name | type | description |
| :--- | :--- | :--- |
| elements | Set&lt;string&gt; | 选定元素的ID集合。 |
| iModel | IModelConnection |  |
| isActive | boolean | 检查是否有任何选定的元素。 |
| onChanged | BeEvent&lt;\(ev: SelectionSetEvent\) =&gt; void&gt; | 每当从此SelectionSet添加或删除元素时调用 |
| size | number | 获取此选择集的条目数。 |

### Defined in

[core/frontend/src/SelectionSet.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/SelectionSet.ts#L227)



