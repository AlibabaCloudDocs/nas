# DeleteSnapshot {#doc_api_NAS_DeleteSnapshot .reference}

DeleteSnapshot用于删除指定的快照。如果需要取消正在创建的快照，也可以调用该接口删除快照，即取消创建快照任务。

## 接口说明 {#description .section}

如果指定的快照ID不存在，请求将被忽略。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=DeleteSnapshot&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|SnapshotId|String|是|s-extreme-snapshotid1|快照 ID。

 |
|Action|String|否|DeleteSnapshot|系统规定参数。取值：DeleteSnapshot。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteSnapshot
&SnapshotId=s-extreme-6tmsbas6ljhwhlkh9
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

访问[错误中心](https://error-center.aliyun.com/status/product/NAS)查看更多错误码。

