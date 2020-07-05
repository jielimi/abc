# iModel.js后端RPC接口

# Editor3dRpcInterface

该接口用于在iModel中编辑Spatial和其他3D元素和模型，所有操作都需要读写访问权限。

| 接口 | 描述 |
| :--- | :--- |
| start\(\_tokenProps: IModelRpcProps, \_editorId: GuidString\): Promise&lt;void&gt;  |  |
| end\(\_tokenProps: IModelRpcProps, \_editorId: GuidString\): Promise&lt;void&gt; |  |
| writeAllChangesToBriefcase\(\_tokenProps: IModelRpcProps, \_editorId: GuidString\): Promise&lt;void&gt; |  |
| startModifyingElements\(\_tokenProps: IModelRpcProps, \_editorId: GuidString, \_elementIds: Id64Array\): Promise&lt;void&gt; |  |
| createElement\(\_tokenProps: IModelRpcProps, \_editorId: GuidString, \_props: GeometricElement3dProps, \_origin?: Point3d, \_angles?: YawPitchRollAngles, \_geometry?: any\): Promise&lt;void&gt; |  |
| applyTransform\(\_tokenProps: IModelRpcProps, \_editorId: GuidString, \_tprops: TransformProps\) |  |
| pushState\(\_tokenProps: IModelRpcProps, \_editorId: GuidString\): Promise&lt;void&gt; |  |
| popState\(\_tokenProps: IModelRpcProps, \_editorId: GuidString\): Promise&lt;void&gt; |  |

### DevToolsRpcInterface

此类的目的是为开发人员工具提供辅助RPC方法，请注意，这不应在生产环境中使用。

| 接口 | 描述 |
| :---: | :---: |
| ping\(\_iModelToken: IModelRpcProps\): Promise&lt;boolean&gt; | 发送ping，如果后端收到ping，则返回true |
| stats\(\_iModelToken: IModelRpcProps, \_options: DevToolsStatsOptions\): Promise&lt;any&gt; | 返回具有后端性能和内存统计信息的JSON对象 |
| versions\(\_iModelToken: IModelRpcProps\): Promise&lt;any&gt; | 返回后端版本（应用程序和iModelJs）的JSON对象 |
| setLogLevel\(\_iModelToken: IModelRpcProps, \_loggerCategory: string, \_logLevel: LogLevel\): Promise&lt;LogLevel \| undefined&gt; | 为指定的类别设置新的日志级别并返回旧的日志级别 |



