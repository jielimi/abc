# **IModelDb**

**iModel.js**中表示iModel数据库文件的类。



**IModelDb**具有三个子类，其中：

* **BriefcaseDb**: 该类表示来自iModelHub的iModel的本地副本。BriefcaseDb引发一组事件，以允许应用程序和子系统跟踪其对象的生命周期，包括onOpen，onOpened等。



* **SnapshotDb**: 该类表示iModel\(快照\)数据库文件，通常用于存档和数据传输目的。



* **StandaloneDb**: 该类表示的iModel数据库文件既不由iModelHub管理也不由ImodelHub进行同步读写文件。一般应用于团队协作中可能不重要单独场景。但是，StandaloneDb的设计与BriefcaseDb的API相似且一致，从而使得用户可以很容易将其升级到iModelHub。



