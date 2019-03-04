# ModifyMountTarget {#doc_api_1038870 .reference}

ModifyMountTarget用于修改挂载点信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=ModifyMountTarget)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyMountTarget|操作接口名，系统规定参数，取值：ModifyMountTarget

 |
|FileSystemId|String|是|1ca404a666|文件系统 ID

 |
|MountTargetDomain|String|是|1ca404a666-wxa89.cn-hangzhou.nas.aliyuncs.com|挂载点域名

 |
|AccessGroupName|String|否|classic-test|权限组名称

 |
|Status|String|否|Inactive|状态，包括 Active 和 Inactive

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FF387D95-34C4-4879-B65A-99D1FA1B65CD|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=ModifyMountTarget
&FileSystemId=1ca404a666
&MountTargetDomain=1ca404a666-wxa89.cn-hangzhou.nas.aliyuncs.com
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyMountTargetResponse>
  <RequestId>FF387D95-34C4-4879-B65A-99D1FA1B65CD</RequestId>
</ModifyMountTargetResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"FF387D95-34C4-4879-B65A-99D1FA1B65CD"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/NAS)

