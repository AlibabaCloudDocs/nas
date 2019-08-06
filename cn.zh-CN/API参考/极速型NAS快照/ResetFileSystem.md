# ResetFileSystem {#doc_api_NAS_ResetFileSystem .reference}

使用文件系统的历史快照回滚至某一阶段的文件系统状态。

## 接口说明 {#description .section}

-   文件系统的状态必须为正常的状态。
-   指定的参数SnapshotId必须是由 FileSystemId 创建的历史快照。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=ResetFileSystem&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|FileSystemId|String|是|extreme-012ddfsdf|指定的文件系统 ID。

 |
|snapshotId|String|是|s-extreme-snapshotid1|需要恢复到某一文件系统阶段的历史快照 ID。

 |
|Action|String|否|ResetFileSystem|系统规定参数。取值：ResetFileSystem。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ResetFileSystem
&FileSystemId=extreme-xoxo
&SnapshotId=s-extreme-67pxwk9aevrkrwwj8
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

