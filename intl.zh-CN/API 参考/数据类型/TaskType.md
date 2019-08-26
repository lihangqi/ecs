# TaskType {#TaskType .reference}

任务类型。

## 节点名 {#section_zdc_2sp_ydb .section}

TaskSetType

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TaskId|String|任务ID|
|Action|String|操作接口名称|
|TaskStatus|String|任务状态可选值：-   Finished 已完成
-   Processing 运行中

|
|SupportCancel|String|是否支持取消任务可选值：-   True
-   False

|
|CreationTime|String|任务创建时间，时间类型按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mmZ。|
|FinishedTime|String|任务完成时间，时间类型按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mmZ。|

