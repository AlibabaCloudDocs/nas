# ModifyFileSystem {#doc_api_1037010 .reference}

ModifyFileSystem用于修改文件系统的信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=ModifyFileSystem)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyFileSystem|操作接口名，系统规定参数，取值：ModifyFileSystem

 |
|FileSystemId|String|是|1ca404a666|文件系统 ID

 |
|Description|String|否|空|描述信息（不可用空格符）

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GEThttps://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyFileSystem
&FileSystemId=1ca404a666
&<公共请求参数>…

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyFileSystemResponse>
  <RequestId>5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8</RequestId>
</ModifyFileSystemResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/NAS)

