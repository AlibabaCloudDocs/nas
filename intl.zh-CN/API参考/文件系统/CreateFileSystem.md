# CreateFileSystem {#doc_api_NAS_CreateFileSystem .reference}

CreateFileSystem用于创建新的文件系统。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=CreateFileSystem)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ProtocolType|String|是|NFS|使用的协议类型，目前包含 NFS和SMB

 |
|StorageType|String|是|Performance|文件系统类别，目前包含 Performance（性能型）和 Capacity（容量型）

 |
|Action|String|否|CreateFileSystem|操作接口名，系统规定参数，取值：CreateFileSystem

 |
|Description|String|否|balabala|文件系统描述（不可用空格符）

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|FileSystemId|String|1ca404a666|创建成的文件系统 ID

 |
|RequestId|String|98696EF0-1607-4E9D-B01D-F20930B68845|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateFileSystem
&StorageType=Performance
&ProtocolType=NFS
&Description=balabala
&<公共请求参数>…

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateFileSystemResponse>
  <FileSystemId>1ca404a666</FileSystemId>
  <RequestId>98696EF0-1607-4E9D-B01D-F20930B68845</RequestId>
</CreateFileSystemResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"FileSystemId":"1ca404a666",
	"RequestId":"98696EF0-1607-4E9D-B01D-F20930B68845"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

