# DeleteMountTarget {#doc_api_NAS_DeleteMountTarget .reference}

DeleteMountTarget用于删除已有挂载点。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=DeleteMountTarget)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|FileSystemId|String|是|174494b666|文件系统 ID

 |
|MountTargetDomain|String|是|174494b666-xog95.cn-hangzhou.nas.aliyuncs.com|挂载点域名

 |
|Action|String|否|DeleteMountTarget|操作接口名，系统规定参数，取值：DeleteMountTarget

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteMountTarget
&FileSystemId=174494b666
&MountTargetDomain=174494b666-xog95.cn-hangzhou.nas.aliyuncs.com
&<公共请求参数>…

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteMountTargetResponse>
  <RequestId>5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8</RequestId>
</DeleteMountTargetResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

