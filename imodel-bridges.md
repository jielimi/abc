# iModel Bridges {#imodel bridges}

通常，在iModel中创建的模型的是由另一种格式存储其数据的应用程序创建的。iModel Bridges的存在是为了将这些其他应用程序中的数据转换为iModelHub/iModelBank中的iModel。

iModel Bridges会将源数据转换为iModel中基于BIS的数据，针对每种不同格式的模型源文件，我们会提供不同的iModel Bridge来进行转换。包括下面所列出的bridges



* MicroStation \(.dgn\)

* AutoCAD \(.dwg\)

* Revit \(.rvt\)

* OpenBuilding Designer
* OpenPlant
* OpenRail Designer
* OpenRoads Designer
* ProStructures
* SmartPlant
* Substation
* ISM
* etc.

## 安装

![](/assets/mstnbridge.png)

每个bridge都是一个可执行文件，直接点击安装即可，这里以MicroStation \(.dgn\)为例：

![](/assets/bridge1.png)

每一步直接点击“next”，即可完成安装。

在Computer\HKEY\_LOCAL\_MACHINE\SOFTWARE\Bentley\iModelBridges\IModelBridgeForMstn路径下，如果显示如下配置，则表示安装成功。

![](/assets/bridge3.png)

