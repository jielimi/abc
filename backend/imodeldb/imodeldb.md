# **IModelDb**

**iModel.js**中表示iModel数据库文件的类。

iModel.js类维护着一个IModelJsNative.DgnDb对象（通过nativeDb（）接口可以访问），iModel.js对外提供的大多数操作都是委托给该对象去完成。

---

其中，每个IModelDb对象包含如下重要数据成员:

| models | IModelDb中的某型集合 |
| :---: | :---: |
| elements | IModelDb中的element集合 |
| views | IModelDb中的视图集合 |
| tiles | IModelDb中的瓦片集合 |

---

**IModelDb**具有三个子类，其中：

* **BriefcaseDb**: 该类表示来自iModelHub的iModel的本地副本。BriefcaseDb引发一组事件，以允许应用程序和子系统跟踪其对象的生命周期，包括onOpen，onOpened等。

* **SnapshotDb**: 该类表示iModel\(快照\)数据库文件，通常用于存档和数据传输目的。

* **StandaloneDb**: 该类表示的iModel数据库文件既不由iModelHub管理也不由ImodelHub进行同步读写文件。一般应用于团队协作中可能不重要单独场景。但是，StandaloneDb的设计与BriefcaseDb的API相似且一致，从而使得用户可以很容易将其升级到iModelHub。

因此，根据不同的需要，可以选择使用不同的子类。

