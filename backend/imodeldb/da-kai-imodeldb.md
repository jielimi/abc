# 打开 BriefcaseDb文件

BriefcaseManager类提供了一种下载BriefcaseDb文件（即iModel的本地副本）的方法。下载之后，BriefcaseDb类提供了用于打开，关闭和访问该副本文件的方法。其中BriefcaseDb实例表示内存中该iModel的本地副本。

1. 使用BriefcaseManager.download下载公文包。
2. 使用BriefcaseDb.open打开公文包。
3. 使用BriefcaseDb.close关闭本地公文包。

---

# 打开 SnapshotDb 文件

SnapshotDb类还提供了用于打开，关闭和访问iModel快照的方法。快照iModel是与iModelHub断开连接的文件，因此没有更改时间表。创建快照后，快照iModel是只读的，无法更改。这使快照iModel成为归档或数据传输目的的理想选择。

1. 使用SnapshotDb.openFile打开现有的快照iModel。
2. 使用SnapshotDb.close关闭快照iModel。

创建一个SnapShotDb本地文件并插入一个元素代码示例:

```
	//创建一个模型
   const imodel = SnapshotDb.createEmpty(iModelPath, { rootSubject: { name: "UrlLinkTest" } });
    const linkProps: RepositoryLinkProps = {
      description: "This is a test repository link",
      url: "http://imodeljs.org",
      repositoryGuid: Guid.createValue(),
      classFullName: RepositoryLink.classFullName,
      code: RepositoryLink.createCode(imodel, IModel.repositoryModelId, "MyTestValue"),
      model: IModel.repositoryModelId,
    };

    const linkElement = imodel.elements.createElement(linkProps);
    const id = imodel.elements.insertElement(linkElement);
    assert.isTrue(Id64.isValidId64(id), "insert worked");
    imodel.saveChanges();

    // 验证插入的元素属性
    const actualValue = imodel.elements.getElementProps<RepositoryLink>(id);
    assert.equal(actualValue.url, linkProps.url, "Repository link url not set as expected");
    assert.equal(actualValue.description, linkProps.description, "Repository link description not set as expected");
    assert.equal(actualValue.repositoryGuid, linkProps.repositoryGuid, "Repository link guid not set as expected.");
```

---

# 打开 StandaloneDb 文件

# 



