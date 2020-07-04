# 读写iModelDb

IModelDb还用作暂存区域，后端可以在其中更改iModel的内容，然后将更改提交给iModelHub。

后端可以进行以下几种更改：

创建或更新元素

创建或更新模型

储备码

  
使用IModelDb.saveChanges可以在本地提交更改。

IModelDb.txns管理本地事务，它支持本地撤消/重做。



# 将更改推送到iModelHub

使用BriefcaseDb.pushChanges将本地更改作为更改集推送到iModelHub，以便其他人可以看到它们。将变更集推送到iModelHub后，它将成为iModel永久时间轴的一部分。此方法自动从iModelHub中提取并合并新的ChangeSet。一次只有一个应用程序可以推送到iModelHub。IModelDb.pushChanges自动重试，以在出现适当的故障时进行推送。但是，如果同时有很多其他应用程序推送，则所有重试尝试都可能失败。在这种情况下，应稍后再尝试按下。修改模型，元素或代码的应用必须使用ConcurrencyControl\(并发控制\)与其他用户进行协调。



