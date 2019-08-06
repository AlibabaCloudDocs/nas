# DeleteAutoSnapshotPolicy {#doc_api_NAS_DeleteAutoSnapshotPolicy .reference}

DeleteAutoSnapshotPolicy 用于删除一条自动快照策略。如果目标自动快照策略已经被应用到文件系统上，删除自动快照策略后，这些文件系统不再执行该策略。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=DeleteAutoSnapshotPolicy&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AutoSnapshotPolicyId|String|是|sp-extreme-233e6ylv0|自动快照策略 ID。您可以调用 DescribeAutoSnapshotPolicies 查看您可用的自动快照策略。

 |
|Action|String|否|DeleteAutoSnapshotPolicy|系统规定参数。取值：DeleteAutoSnapshotPolicy。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteAutoSnapshotPolicy
&AutoSnapshotPolicyId=sp-extreme-6i0brwewjt0gfylh0
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

