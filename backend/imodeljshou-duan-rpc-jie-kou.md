# iModel.js后端RPC接口

### DevToolsRpcInterface

此类的目的是为开发人员工具提供辅助RPC方法，请注意，这不应在生产环境中使用。

| 接口 | 描述 |
| :---: | :---: |
| ping\(\_iModelToken: IModelRpcProps\): Promise&lt;boolean&gt; | 发送ping，如果后端收到ping，则返回true |
| stats\(\_iModelToken: IModelRpcProps, \_options: DevToolsStatsOptions\): Promise&lt;any&gt; | 返回具有后端性能和内存统计信息的JSON对象 |
| versions\(\_iModelToken: IModelRpcProps\): Promise&lt;any&gt; | 返回后端版本（应用程序和iModelJs）的JSON对象 |
| setLogLevel\(\_iModelToken: IModelRpcProps, \_loggerCategory: string, \_logLevel: LogLevel\): Promise&lt;LogLevel \| undefined&gt; | 为指定的类别设置新的日志级别并返回旧的日志级别 |



