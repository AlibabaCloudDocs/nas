# CreateSnapshot {#doc_api_NAS_CreateSnapshot .reference}

CreateSnapshot 用于创建快照。

## 接口说明 {#description .section}

-   一个文件系统最多能创建 64 份快照。
-   文件系统挂载的实例必须处于正常状态，否则无法创建快照。
-   如果创建快照还未完成，您无法为该文件系统再次创建快照。
-   若创建快照时文件系统正好达到过期释放时间，文件系统会被释放的同时也会删除创建中（Creating）的快照。
-   创建快照可能会轻微降低文件系统的性能，I/O 性能短暂变慢，您需要避开业务高峰。
-   快照只会备份某一时刻的数据，创建快照期间，操作文件系统产生的增量数据不会同步到快照中。
-   您自行创建的快照会一直保留，请定期删除不再需要的快照，避免快照容量持续扣费。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=CreateSnapshot&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|FileSystemId|String|是|Extreme-01ddddfc|文件系统 ID。

 |
|Action|String|否|CreateSnapshot|系统规定参数。对于您自行拼凑 HTTP/HTTPS URL 发起的 API 请求，Action 为必选参数。取值：CreateSnapshot

 |
|Description|String|否|FinanceDepet|快照的接口说明。长度为 2~256 个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

 |
|RetentionDays|Integer|否|30|设置快照的保留时间，单位为天。保留时间到期后快照会被自动释放。默认值：-1。

 取值范围：

 -   -1：永久保存
-   1~65536：指定保存天数

 |
|SnapshotName|String|否|FinanceJoshua|快照的显示名称。长度为 2~128 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。为防止和自动快照的名称冲突，不能以 auto 开头。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|SnapshotId|String|s-extreme-snapshotid1|快照 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateSnapshot
&FileSystemId=1ca404a348
&<公共请求参数>
…

```

正常返回示例

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"AB78A546-A85A-44E7-B4A3-C0AAA77B89AF",
	"SnapshotId":"s-extreme-6tmsbas6ljhwhlkh9"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

