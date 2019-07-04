# DeleteFileSystem {#doc_api_NAS_DeleteFileSystem .reference}

DeleteFileSystem用于删除已有的文件系统。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=DeleteFileSystem)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|FileSystemId|String|是|1ca404a348|要删除的文件系统 ID

 |
|Action|String|否|DeleteFileSystem|操作接口名，系统规定参数，取值：DeleteFileSystem

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|9E15E394-38A6-457A-A62A-D9797C9A0262|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteFileSystem
&FileSystemId=1ca404a348
&<公共请求参数>…

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteFileSystemResponse>
  <RequestId>9E15E394-38A6-457A-A62A-D9797C9A0262</RequestId>
</DeleteFileSystemResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"9E15E394-38A6-457A-A62A-D9797C9A0262"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

