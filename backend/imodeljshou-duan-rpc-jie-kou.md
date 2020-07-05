# iModel.js后端RPC接口

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
| getViewThumbnail\(\_iModelToken: IModelRpcProps, \_viewId: string\): Promise&lt;Uint8Array&gt;  |  |
| getDefaultViewId\(\_iModelToken: IModelRpcProps\): Promise&lt;Id64String&gt; |  |
| requestSnap\(\_iModelToken: IModelRpcProps, \_sessionId: string, \_props: SnapRequestProps\): Promise&lt;SnapResponseProps&gt; |  |
| cancelSnap\(\_iModelToken: IModelRpcProps, \_sessionId: string\): Promise&lt;void&gt; |  |
| getMassProperties\(\_iModelToken: IModelRpcProps, \_props: MassPropertiesRequestProps\): Promise&lt;MassPropertiesResponseProps&gt; |  |
| getIModelCoordinatesFromGeoCoordinates\(\_iModelToken: IModelRpcProps, \_props: string\): Promise&lt;IModelCoordinatesResponseProps&gt; |  |
| getGeoCoordinatesFromIModelCoordinates\(\_iModelToken: IModelRpcProps, \_props: string\): Promise&lt;GeoCoordinatesResponseProps&gt; |  |
| getGeometrySummary\(\_iModelToken: IModelRpcProps, \_props: GeometrySummaryRequestProps\): Promise&lt;string&gt; |  |

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



