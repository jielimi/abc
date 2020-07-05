# iModel.js后端RPC接口

### SnapshotIModelRpcInterface

该接口用于snapshot \* iModels，且适用于桌面应用程序和移动产品。 不鼓励Web产品注册此接口。

| 接口 | 描述 |
| :---: | :---: |
| openFile\( string\) |  |
| openRemote\( string\) |  |
| close\( IModelRpcProps\) |  |

---

### NativeAppRpcInterface

该接口提供特定于本机应用程序的Rpc功能。本机应用程序是一个iModel.js应用程序，其中前端和后端进程之间存在一对一的关系。两个进程都在同一设备上执行，这可以启用离线工作流程。这样的应用可以针对特定平台-例如Electron，iOS，Android。相比之下，基于浏览器的iModel.js应用程序与平台无关，支持多个同时的前端连接，并且需要网络连接。

| 接口 | 描述 |
| :---: | :---: |
| log\( number,  LogLevel,  string,  string,  any\) | 将前端日志发送到后端。                                                           |
| fetchEvents\( IModelRpcProps,  number\) | 从后端获取指定iModel的队列事件列表，直到指定的最大事件数。 |
| checkInternetConnectivity\(\) | 检查互联网是否可以访问以及如何访问。 |
| overrideInternetConnectivity\( OverriddenBy, ?: InternetConnectivityStatus\) | 手动覆盖Internet可达性以进行测试。 |
| getConfig\(\) | 从后端返回配置 |
| cancelTileContentRequests\( IModelRpcProps,  TileTreeContentIds\[\]\) | 取消当前待处理或活动生成的图块内容。 |
| requestDownloadBriefcase\( RequestBriefcaseProps,  DownloadBriefcaseOptions,  boolean\) | 要求下载Briefcase。 该接口需要互联网连接，并且必须具有有效的令牌。 |
| downloadRequestCompleted\(BriefcaseKey\) | 完成Briefcase的下载。 该接口需要互联网连接，并且必须具有有效的令牌。 |
| requestCancelDownloadBriefcase\(BriefcaseKey\) | 取消先前请求的Briefcase下载 |
| openBriefcase\( BriefcaseKey, OpenBriefcaseOptions\): | 打开磁盘上的Briefcase-此api可以用为离线 |
| closeBriefcase\( BriefcaseKey\) | 关闭磁盘上的Briefcase-此api可以用为离线 |
| deleteBriefcase\( BriefcaseKey\) | 删除以前下载的Briefcase。 必须先关闭Briefcase。 |
| getBriefcases\(\) | 获取以前要求下载或完全下载的所有Briefcase |
| storageMgrOpen\( string\) |  |
| storageMgrClose\( string,  boolean\) |  |
| storageMgrNames\(\) |  |
| storageGet\( string,  string\) |  |
| storageSet\(string,  string,  StorageValue\) |  |
| storageRemove\( string,  string\) |  |
| storageKeys\( string\) |  |
| storageRemoveAll\( string\) |  |

---

# IModelReadRpcInterface

该接口用于从iModel读取信息，所有操作仅需要读访问权限\(此接口通常不直接使用，有关从前端访问iModel的更高级，更方便的API参见IModelConnection\)。

| 接口 | 描述 |
| :---: | :---: |
| openForRead\( IModelRpcProps\) |  |
| close\( IModelRpcProps\) | 关闭 |
| queryRows\( IModelRpcProps,  string,  any\[\] \| object, \_limit?: QueryLimit, :QueryQuota, QueryPriority\) |  |
| getModelProps\( IModelRpcProps,  Id64String\[\]\) | 查询指定id的模型的属性。 |
| queryModelRanges\( IModelRpcProps,  Id64String\[\]\) |  |
| queryModelProps（IModelRpcProps,  EntityQueryParams\) |  |
| getElementProps\( IModelRpcProps,  Id64String\[\]\) |  |
| queryEntityIds\( IModelRpcProps, EntityQueryParams\) |  |
| getClassHierarchy\( IModelRpcProps,  string\) |  |
| getAllCodeSpecs\( IModelRpcProps\) |  |
| getViewStateData\( IModelRpcProps,  string\) |  |
| readFontJson\( IModelRpcProps\) |  |
| getToolTipMessage\( IModelRpcProps,  string\) |  |
| getViewThumbnail\( IModelRpcProps,  string\) |  |
| getDefaultViewId\(: IModelRpcProps\) |  |
| requestSnap\( IModelRpcProps,  string,  SnapRequestProps\) |  |
| cancelSnap\( IModelRpcProps,  string\) |  |
| getMassProperties\( IModelRpcProps,  MassPropertiesRequestProps\) |  |
| getIModelCoordinatesFromGeoCoordinates\( IModelRpcProps, string\) |  |
| getGeoCoordinatesFromIModelCoordinates\( IModelRpcProps,  string\) |  |
| getGeometrySummary\( IModelRpcProps,  GeometrySummaryRequestProps\) |  |

---

### IModelWriteRpcInterface

该接口用于写入iModel，所有操作都需要读写访问。  
\(此接口通常不直接使用。 有关从前端访问iModel的更高级，更方便的API，请参见IModelConnection）

| 接口 | 描述 |
| :---: | :---: |
| openForWrite\( IModelRpcProps\) |  |
| saveChanges\( IModelRpcProps,  string\) | 保存更改。 |
| hasUnsavedChanges\( IModelRpcProps\) |  |
| hasPendingTxns\(IModelRpcProps\) |  |
| updateProjectExtents\( IModelRpcProps, AxisAlignedBox3dProps\) |  |
| saveThumbnail\( IModelRpcProps, Uint8Array\) | 保存缩略图。 |
| requestResources\(IModelRpcProps,  Id64Array,  Id64Array,  DbOpcode\) |  |
| doConcurrencyControlRequest\( IModelRpcProps\) |  |
| lockModel\(IModelRpcProps,  Id64String,  LockLevel\) |  |
| synchConcurrencyControlResourcesCache\(IModelRpcProps\) |  |
| pullMergePush\( IModelRpcProps,  string,  boolean\) |  |
| getModelsAffectedByWrites\( IModelRpcProps\) |  |
| getParentChangeset\( IModelRpcProps\) |  |
| deleteElements\( IModelRpcProps, Id64Array\) | 删除指定的element。 |
| createAndInsertPhysicalModel\( IModelRpcProps, CodeProps,  boolean\) |  |
| createAndInsertSpatialCategory\( IModelRpcProps,  Id64String,  string,  SubCategoryAppearance.Props\) |  |

---

### IModelTileRpcInterface

| 接口 | 属性 |
| :---: | :---: |
| getTileCacheContainerUrl\( IModelRpcProps, CloudStorageContainerDescriptor\) |  |
| requestTileTreeProps\( IModelRpcProps,  string\) | 请求。 |
| requestTileContent\( IModelRpcProps,  string,  string,  \(\) =&gt; boolean, guid?: string\) |  |
| purgeTileTrees\( IModelRpcProps,  Id64Array \| undefined\) |  |

---

### WipRpcInterface

此接口的目的是容纳WIP RPC方法。 例如：

\*-签名或行为仍在变化的WIP方法

\*将这些WIP RPC方法与已声明兼容性目标的其他RpcInterfaces隔离开来。

\*一旦稳定，目标就是将方法转移到他们应有的地方。

\*应用程序/服务应了解注册此RpcInterface所暗示的\* flux \*，并且在考虑使用它之前，还应同时控制客户端和服务器。

| 接口 | 描述 |
| :---: | :---: |
| placeholder\( IModelRpcProps\) |  |
| isChangeCacheAttached\( IModelRpcProps\) |  |
| attachChangeCache\( IModelRpcProps\) | 附加更改的缓存。 |
| detachChangeCache\( IModelRpcProps\) |  |
| getChangedElements\(IModelRpcProps, string,  string\) |  |
| isChangesetProcessed\( IModelRpcProps,  string\) |  |

---

### Editor3dRpcInterface

该接口用于在iModel中编辑Spatial和其他3D元素和模型，所有操作都需要读写访问权限。

| 接口 | 描述 |
| :---: | :---: |
| start\( IModelRpcProps, GuidString\) |  |
| end\(IModelRpcProps,  GuidString\) |  |
| writeAllChangesToBriefcase\(IModelRpcProps, GuidString\) |  |
| startModifyingElements\(IModelRpcProps, GuidString, Id64Array\) |  |
| createElement\( IModelRpcProps, GuidString,  GeometricElement3dProps, Point3d,  YawPitchRollAngles,  any\) |  |
| applyTransform\(IModelRpcProps, GuidString, TransformProps\) | 应用矩阵变换。 |
| pushState\( IModelRpcProps,  GuidString\) |  |
| popState\(IModelRpcProps, GuidString\) |  |

---

### DevToolsRpcInterface

此类的目的是为开发人员工具提供辅助RPC方法，请注意，这不应在生产环境中使用。

| 接口 | 描述 |
| :---: | :---: |
| ping\(IModelRpcProps\) | 发送ping，如果后端收到ping，则返回true |
| stats\(IModelRpcProps,  DevToolsStatsOptions\) | 返回具有后端性能和内存统计信息的JSON对象 |
| versions\(\_iModelToken: IModelRpcProps\) | 返回后端版本（应用程序和iModelJs）的JSON对象 |
| setLogLevel\( IModelRpcProps, string,  LogLevel\) | 为指定的类别设置新的日志级别并返回旧的日志级别 |



