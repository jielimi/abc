# iModel.js后端RPC接口

### SnapshotIModelRpcInterface

该接口用于snapshot \* iModels，且适用于桌面应用程序和移动产品。 不鼓励Web产品注册此接口。

| 接口 | 描述 |
| :---: | :---: |
| openFile\(filePath: string\): Promise&lt;IModelConnectionProps&gt; |  |
| openRemote\(key: string\): Promise&lt;IModelConnectionProps&gt; |  |
| close\(iModelProps: IModelRpcProps\): Promise&lt;boolean&gt; |  |

### NativeAppRpcInterface

该接口提供特定于本机应用程序的Rpc功能。本机应用程序是一个iModel.js应用程序，其中前端和后端进程之间存在一对一的关系。两个进程都在同一设备上执行，这可以启用离线工作流程。这样的应用可以针对特定平台-例如Electron，iOS，Android。相比之下，基于浏览器的iModel.js应用程序与平台无关，支持多个同时的前端连接，并且需要网络连接。

| 接口 | 描述 |
| :---: | :---: |
| log\(\_timestamp: number, \_level: LogLevel, \_category: string, \_message: string, \_metaData?: any\): Promise&lt;void&gt; | \*\*将前端日志发送到后端。                                                                @param            \_level指定日志级别                                               @param      \_category指定日志类别                                         @param  \_message指定日志信息                                           @param \_metaData （如果有） |
| fetchEvents\(\_iModelToken: IModelRpcProps, \_maxToFetch: number\): Promise&lt;QueuedEvent\[\]&gt; | 从后端获取指定iModel的队列事件列表，直到指定的最大事件数。 |
| checkInternetConnectivity\(\): Promise&lt;InternetConnectivityStatus&gt; | 检查互联网是否可以访问以及如何访问。 |
| overrideInternetConnectivity\(\_overriddenBy: OverriddenBy, \_status?: InternetConnectivityStatus\): Promise&lt;void&gt; | 手动覆盖Internet可达性以进行测试。 |
| getConfig\(\): Promise&lt;any&gt; | 从后端返回配置 |
| cancelTileContentRequests\(\_iModelToken: IModelRpcProps, \_contentIds: TileTreeContentIds\[\]\): Promise&lt;void&gt; | 取消当前待处理或活动生成的图块内容。 |
| requestDownloadBriefcase\(\_requestProps: RequestBriefcaseProps, \_downloadOptions: DownloadBriefcaseOptions, \_reportProgress: boolean\): Promise&lt;BriefcaseProps&gt; | 要求下载Briefcase。 该接口需要互联网连接，并且必须具有有效的令牌。 |
| downloadRequestCompleted\(\_key: BriefcaseKey\): Promise&lt;void&gt; | 完成Briefcase的下载。 该接口需要互联网连接，并且必须具有有效的令牌。 |
| requestCancelDownloadBriefcase\(\_key: BriefcaseKey\): Promise&lt;boolean&gt; | 取消先前请求的Briefcase下载 |
| openBriefcase\(\_key: BriefcaseKey, \_openOptions?: OpenBriefcaseOptions\): Promise&lt;IModelProps&gt; | 打开磁盘上的Briefcase-此api可以用为离线 |
| closeBriefcase\(\_key: BriefcaseKey\): Promise&lt;void&gt; | 关闭磁盘上的Briefcase-此api可以用为离线 |
| deleteBriefcase\(\_key: BriefcaseKey\): Promise&lt;void&gt; | 删除以前下载的Briefcase。 必须先关闭Briefcase。 |
| getBriefcases\(\): Promise&lt;BriefcaseProps\[\]&gt; | 获取以前要求下载或完全下载的所有Briefcase |
| storageMgrOpen\(\_storageId: string\): Promise&lt;string&gt; |  |
| storageMgrClose\(\_storageId: string, \_deleteIt: boolean\): Promise&lt;void&gt; |  |
| storageMgrNames\(\): Promise&lt;string\[\]&gt; |  |
| storageGet\(\_storageId: string, \_key: string\): Promise&lt;StorageValue \| undefined&gt; |  |
| storageSet\(\_storageId: string, \_key: string, \_value: StorageValue\): Promise&lt;void&gt; |  |
| storageRemove\(\_storageId: string, \_key: string\): Promise&lt;void&gt; |  |
| storageKeys\(\_storageId: string\): Promise&lt;string\[\]&gt; |  |
| storageRemoveAll\(\_storageId: string\): Promise&lt;void&gt; |  |

---

# IModelReadRpcInterface

该接口用于从iModel读取信息，所有操作仅需要读访问权限\(此接口通常不直接使用，有关从前端访问iModel的更高级，更方便的API参见IModelConnection\)。

| 接口 | 描述 |
| :---: | :---: |
| openForRead\(\_iModelToken: IModelRpcProps\): Promise&lt;IModelConnectionProps&gt; |  |
| close\(\_iModelToken: IModelRpcProps\): Promise&lt;boolean&gt; |  |
| queryRows\(\_iModelToken: IModelRpcProps, \_ecsql: string, \_bindings?: any\[\] \| object, \_limit?: QueryLimit, \_quota?: QueryQuota, \_priority?: QueryPriority\): Promise&lt;QueryResponse&gt; |  |
| getModelProps\(\_iModelToken: IModelRpcProps, \_modelIds: Id64String\[\]\): Promise&lt;ModelProps\[\]&gt; |  |
| queryModelRanges\(\_iModelToken: IModelRpcProps, \_modelIds: Id64String\[\]\): Promise&lt;Range3dProps\[\]&gt; |  |
| queryModelProps\(\_iModelToken: IModelRpcProps, \_params: EntityQueryParams\): Promise&lt;ModelProps\[\]&gt; |  |
| getElementProps\(\_iModelToken: IModelRpcProps, \_elementIds: Id64String\[\]\): Promise&lt;ElementProps\[\]&gt; |  |
| queryEntityIds\(\_iModelToken: IModelRpcProps, \_params: EntityQueryParams\): Promise&lt;Id64String\[\]&gt; |  |
| getClassHierarchy\(\_iModelToken: IModelRpcProps, \_startClassName: string\): Promise&lt;string\[\]&gt; |  |
| getAllCodeSpecs\(\_iModelToken: IModelRpcProps\): Promise&lt;any\[\]&gt; |  |
| getViewStateData\(\_iModelToken: IModelRpcProps, \_viewDefinitionId: string\): Promise&lt;ViewStateProps&gt; |  |
| readFontJson\(\_iModelToken: IModelRpcProps\): Promise&lt;any&gt; |  |
| getToolTipMessage\(\_iModelToken: IModelRpcProps, \_elementId: string\): Promise&lt;string\[\]&gt; |  |
| getViewThumbnail\(\_iModelToken: IModelRpcProps, \_viewId: string\): Promise&lt;Uint8Array&gt; |  |
| getDefaultViewId\(\_iModelToken: IModelRpcProps\): Promise&lt;Id64String&gt; |  |
| requestSnap\(\_iModelToken: IModelRpcProps, \_sessionId: string, \_props: SnapRequestProps\): Promise&lt;SnapResponseProps&gt; |  |
| cancelSnap\(\_iModelToken: IModelRpcProps, \_sessionId: string\): Promise&lt;void&gt; |  |
| getMassProperties\(\_iModelToken: IModelRpcProps, \_props: MassPropertiesRequestProps\): Promise&lt;MassPropertiesResponseProps&gt; |  |
| getIModelCoordinatesFromGeoCoordinates\(\_iModelToken: IModelRpcProps, \_props: string\): Promise&lt;IModelCoordinatesResponseProps&gt; |  |
| getGeoCoordinatesFromIModelCoordinates\(\_iModelToken: IModelRpcProps, \_props: string\): Promise&lt;GeoCoordinatesResponseProps&gt; |  |
| getGeometrySummary\(\_iModelToken: IModelRpcProps, \_props: GeometrySummaryRequestProps\): Promise&lt;string&gt; |  |

---

### IModelWriteRpcInterface

该接口用于写入iModel，所有操作都需要读写访问。  
\(此接口通常不直接使用。 有关从前端访问iModel的更高级，更方便的API，请参见IModelConnection。  
\)

| openForWrite\(\_iModelToken: IModelRpcProps\): Promise&lt;IModelConnectionProps&gt; |  |
| :--- | :--- |
| saveChanges\(\_iModelToken: IModelRpcProps, \_description?: string\): Promise&lt;void&gt; |  |
| hasUnsavedChanges\(\_iModelToken: IModelRpcProps\): Promise&lt;boolean&gt; |  |
| hasPendingTxns\(\_iModelToken: IModelRpcProps\): Promise&lt;boolean&gt; |  |
| updateProjectExtents\(\_iModelToken: IModelRpcProps, \_newExtents: AxisAlignedBox3dProps\): Promise&lt;void&gt; |  |
| saveThumbnail\(\_iModelToken: IModelRpcProps, \_val: Uint8Array\): Promise&lt;void&gt; |  |
| requestResources\(\_tokenProps: IModelRpcProps, \_elementIds: Id64Array, \_modelIds: Id64Array, \_opcode: DbOpcode\): Promise&lt;void&gt; |  |
| doConcurrencyControlRequest\(\_tokenProps: IModelRpcProps\): Promise&lt;void&gt; |  |
| lockModel\(\_tokenProps: IModelRpcProps, \_modelId: Id64String, \_level: LockLevel\): Promise&lt;void&gt; |  |
| synchConcurrencyControlResourcesCache\(\_tokenProps: IModelRpcProps\): Promise&lt;void&gt; |  |
| pullMergePush\(\_tokenProps: IModelRpcProps, \_comment: string, \_doPush: boolean\): Promise&lt;GuidString&gt; |  |
| getModelsAffectedByWrites\(\_tokenProps: IModelRpcProps\): Promise&lt;Id64String\[\]&gt; |  |
| getParentChangeset\(\_iModelToken: IModelRpcProps\): Promise&lt;string&gt; |  |
| deleteElements\(\_tokenProps: IModelRpcProps, \_ids: Id64Array\): Promise&lt;void&gt; |  |
| createAndInsertPhysicalModel\(\_tokenProps: IModelRpcProps, \_newModelCode: CodeProps, \_privateModel: boolean\): Promise&lt;Id64String&gt; |  |
| createAndInsertSpatialCategory\(\_tokenProps: IModelRpcProps, \_scopeModelId: Id64String, \_categoryName: string, \_appearance: SubCategoryAppearance.Props\): Promise&lt;Id64String&gt; |  |

---

### IModelTileRpcInterface

| 接口 | 属性 |
| :---: | :---: |
| getTileCacheContainerUrl\(\_tokenProps: IModelRpcProps, \_id: CloudStorageContainerDescriptor\): Promise&lt;CloudStorageContainerUrl&gt; |  |
| requestTileTreeProps\(\_tokenProps: IModelRpcProps, \_id: string\): Promise&lt;TileTreeProps&gt; |  |
| requestTileContent\(iModelToken: IModelRpcProps, treeId: string, contentId: string, isCanceled?: \(\) =&gt; boolean, guid?: string\): Promise&lt;Uint8Array&gt; |  |
| async purgeTileTrees\(\_tokenProps: IModelRpcProps, \_modelIds: Id64Array \| undefined\): Promise&lt;void&gt; |  |

---

# Editor3dRpcInterface

该接口用于在iModel中编辑Spatial和其他3D元素和模型，所有操作都需要读写访问权限。

| 接口 | 描述 |
| :---: | :---: |
| start\(\_tokenProps: IModelRpcProps, \_editorId: GuidString\): Promise&lt;void&gt; |  |
| end\(\_tokenProps: IModelRpcProps, \_editorId: GuidString\): Promise&lt;void&gt; |  |
| writeAllChangesToBriefcase\(\_tokenProps: IModelRpcProps, \_editorId: GuidString\): Promise&lt;void&gt; |  |
| startModifyingElements\(\_tokenProps: IModelRpcProps, \_editorId: GuidString, \_elementIds: Id64Array\): Promise&lt;void&gt; |  |
| createElement\(\_tokenProps: IModelRpcProps, \_editorId: GuidString, \_props: GeometricElement3dProps, \_origin?: Point3d, \_angles?: YawPitchRollAngles, \_geometry?: any\): Promise&lt;void&gt; |  |
| applyTransform\(\_tokenProps: IModelRpcProps, \_editorId: GuidString, \_tprops: TransformProps\) |  |
| pushState\(\_tokenProps: IModelRpcProps, \_editorId: GuidString\): Promise&lt;void&gt; |  |
| popState\(\_tokenProps: IModelRpcProps, \_editorId: GuidString\): Promise&lt;void&gt; |  |

---

### DevToolsRpcInterface

此类的目的是为开发人员工具提供辅助RPC方法，请注意，这不应在生产环境中使用。

| 接口 | 描述 |
| :---: | :---: |
| ping\(\_iModelToken: IModelRpcProps\): Promise&lt;boolean&gt; | 发送ping，如果后端收到ping，则返回true |
| stats\(\_iModelToken: IModelRpcProps, \_options: DevToolsStatsOptions\): Promise&lt;any&gt; | 返回具有后端性能和内存统计信息的JSON对象 |
| versions\(\_iModelToken: IModelRpcProps\): Promise&lt;any&gt; | 返回后端版本（应用程序和iModelJs）的JSON对象 |
| setLogLevel\(\_iModelToken: IModelRpcProps, \_loggerCategory: string, \_logLevel: LogLevel\): Promise&lt;LogLevel \| undefined&gt; | 为指定的类别设置新的日志级别并返回旧的日志级别 |



