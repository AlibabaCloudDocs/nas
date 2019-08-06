# CancelAutoSnapshotPolicy {#doc_api_NAS_CancelAutoSnapshotPolicy .reference}

CancelAutoSnapshotPolicy 用于取消一个或者多个文件系统的自动快照策略。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=CancelAutoSnapshotPolicy&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|FileSystemIds|String|是|extreme-233e6ylv0,extreme-23vbpbi03,extreme-23vasz3ds|目标文件系统 ID。一次最多指定 100 个文件系统 ID，当您需要取消多个文件系统的自动快照策略时，多个文件系统 ID 之间用半角逗号（,）隔开。

 |
|Action|String|否|CancelAutoSnapshotPolicy|系统规定参数。取值：CancelAutoSnapshotPolicy。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CancelAutoSnapshotPolicy
&FileSystemIds=extreme-xxx
&<公共请求参数>
…

```

正常返回示例

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"12FA778B-C8D3-4D2B-88AD-C10ED0326C57"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

