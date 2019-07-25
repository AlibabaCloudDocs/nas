# ModifyMountTarget {#doc_api_NAS_ModifyMountTarget .reference}

ModifyMountTarget用于修改挂载点信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=ModifyMountTarget&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|FileSystemId|String|是|1ca404a666|文件系统 ID

 |
|MountTargetDomain|String|是|1ca404a666-wxa89.cn-hangzhou.nas.aliyuncs.com|挂载点域名

 |
|AccessGroupName|String|否|classic-test|权限组名称

 |
|Action|String|否|ModifyMountTarget|操作接口名，系统规定参数，取值：ModifyMountTarget

 |
|Status|String|否|Inactive|挂载点状态，枚举值包括：Active（表示启用），Inactive（表示禁用）

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FF387D95-34C4-4879-B65A-99D1FA1B65CD|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyMountTarget
&FileSystemId=1ca404a666
&MountTargetDomain=1ca404a666
&Status=Inactive
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

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

