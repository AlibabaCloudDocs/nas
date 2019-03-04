# CreateMountTarget {#doc_api_1038390 .reference}

CreateMountTarget用于创建挂载点。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=CreateMountTarget)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|是|classic-test|权限组名称

 |
|Action|String|是|CreateMountTarget|操作接口名，系统规定参数，取值：CreateMountTarget

 |
|FileSystemId|String|是|174494b666|文件系统 ID

 |
|NetworkType|String|是|vpc|网络类型，包括Vpc和Classic

 |
|VSwitchId|String|否|vsw-2zevmwkwyztjuoffgdiwl|交换机 ID

 |
|VpcId|String|否|vpc-2zesj9afh3y518k9oe86q|VPC 网络 ID

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|MountTargetDomain|String|174494b666-xog95.cn-hangzhou.nas.aliyuncs.com|挂载点域名

 |
|RequestId|String|70EACC9C-D07A-4A34-ADA4-77506C42B023|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?Action=CreateMountTarget
&AccessGroupName=classic-test
&FileSystemId=174494b666
&NetworkType=vpc
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateMountTargetResponse>
  <RequestId>70EACC9C-D07A-4A34-ADA4-77506C42B023</RequestId>
  <MountTargetDomain>174494b666-xog95.cn-hangzhou.nas.aliyuncs.com</MountTargetDomain>
</CreateMountTargetResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"70EACC9C-D07A-4A34-ADA4-77506C42B023",
	"MountTargetDomain":"174494b666-xog95.cn-hangzhou.nas.aliyuncs.com"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/NAS)

