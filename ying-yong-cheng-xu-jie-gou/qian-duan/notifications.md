# Notifications

向用户提供感兴趣的事件元素等的反馈。

## Classes

| name | description |
| :--- | :--- |
| ActivityMessageDetails | 指定要向用户显示的活动消息的详细信息 |
| NotificationManager | NotificationManager控制与用户的交互，以获得提示、错误消息和警报对话框。 |
| NotifyMessageDetails | 描述要向用户显示的消息。 |

## ActivityMessageDetails

###### Methods

| name | description |
| :--- | :--- |
| constructor\(showProgressBar: boolean, showPercentInMessage: boolean, supportsCancellation: boolean, showDialogInitially: boolean = true\): ActivityMessageDetails | 构造函数 |
| onActivityCancelled\(\): void | 当用户取消活动时从NotificationAdmin调用。 |
| onActivityCompleted\(\): void | 当活动成功完成时从NotificationAdmin调用。 |

###### Properties

| name | type | description |
| :--- | :--- | :--- |
| showDialogInitially | boolean | 指示是否最初显示“活动消息”对话框。 |
| showPercentInMessage | boolean | 指示是否在活动消息文本中显示完成百分比。 |
| showProgressBar | boolean | 指示是否在“活动消息”对话框中显示进度条。 |
| supportsCancellation | boolean | 指示是否显示“取消”按钮，使用户能够取消操作。 |
| wasCancelled | boolean |  |

### Defined in 

[core/frontend/src/NotificationManager.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/NotificationManager.ts#L151)



## NotificationManager

NotificationManager控制与用户的交互，以获得提示、错误消息和警报对话框。NotificationManager的实现可能以不同的方式显示信息。例如，在非交互式会话中，这些消息可以保存到日志文件中，也可以直接丢弃。

###### Methods

| name | description |
| :--- | :--- |
| \_showToolTip\(\_htmlElement: HTMLElement, \_message: HTMLElement \| string, \_location?: XAndY, \_options?: ToolTipOptions\): void | 实现在指定位置显示工具提示消息。 |
| clearToolTip\(\): void | 如果工具提示当前处于打开状态，请将其清除。 |
| closeInputFieldMessage\(\): void | 关闭用OutputMessageType.InputField创建的消息会话。 |
| closePointerMessage\(\): void | 关闭用OutputMessageType.Pointer创建的消息会话。 |
| endActivityMessage\(\_reason: ActivityMessageEndReason\): boolean | 结束活动消息。 |
| openMessageBox\(\_mbType: MessageBoxType, \_message: HTMLElement \| string, \_icon: MessageBoxIconType\): Promise&lt;MessageBoxValue&gt; | 输出MessageBox并等待用户的响应。 |
| openToolTip\(htmlElement: HTMLElement, message: HTMLElement \| string, location?: XAndY, options?: ToolTipOptions\): void | 显示工具提示窗口。 |
| outputActivityMessage\(\_messageText: HTMLElement \| string, \_percentComplete: number\): boolean | 向用户输出活动消息。 |
| outputMessage\(\_message: NotifyMessageDetails\): void | 向用户输出消息和/或警报。 |
| outputPrompt\(\_prompt: string\): void | 向用户输出本地化的提示。 |
| outputPromptByKey\(key: string\): void | 输出一个提示，给定一个i18n key。 |
| setToolAssistance\(instructions: ToolAssistanceInstructions \| undefined\): void | 工具的设置工具帮助说明。 |
| setupActivityMessage\(\_details: ActivityMessageDetails\): boolean | 设置活动消息。 |
| updatePointerMessage\(\_displayPoint: XAndY, \_relativePosition: RelativePosition = RelativePosition.TopRight\): void | 用创建的更新消息位置OutputMessageType.Pointer. |

###### Properties

| name | type | description |
| :--- | :--- | :--- |
| isToolTipOpen | boolean | 如果工具提示当前处于打开状态，则返回true。 |
| isToolTipSupported  | boolean | 如果\_showTooltip具有实现并将显示工具提示，则返回true。 |
| toolTipLocation | Point2d |  |

### Defined in

[core/frontend/src/NotificationManager.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/NotificationManager.ts#L174)

## NotifyMessageDetails

###### Methods

| name | decscription |
| :--- | :--- |
| constructor\(priority: OutputMessagePriority, briefMessage: HTMLElement \| string, detailedMessage?: HTMLElement \| string, msgType: OutputMessageType = OutputMessageType.Toast, openAlert: OutputMessageAlert = OutputMessageAlert.None\): NotifyMessageDetails | 构造函数 |
| setInputFieldTypeDetails\(inputField: HTMLElement\): void | 设置OutputMessageType.InputField消息详细信息。 |
| setPointerTypeDetails\(viewport: HTMLElement, displayPoint: XAndY, relativePosition: RelativePosition = RelativePosition.TopRight\): void | 设置OutputMessageType.Pointer消息详细信息。 |

###### Properties

| name | type | description |
| :--- | :--- | :--- |
| briefMessage | HTMLElement \| string | 传达对问题最简单解释的简短信息。 |
| detailedMessage  | HTMLElement \| string | 详细解释问题并可能提供解决方案的全面信息。 |
| displayPoint | undefined \| Point2d |  |
| displayTime | BeDuration |  |
| inputField | undefined \| HTMLElement |  |
| msgType | OutputMessageType | 消息的类型。 |
| openAlert   | OutputMessageAlert | 是否应显示警报框，如果是，应显示何种类型。 |
| priority | OutputMessagePriority | NotificationManager应赋予此消息的优先级。 |
| relativePosition | RelativePosition |  |
| viewport |  |  |

### Defined in

[core/frontend/src/NotificationManager.ts](https://github.com/imodeljs/imodeljs/tree/master/core/frontend/src/NotificationManager.ts#L110)



