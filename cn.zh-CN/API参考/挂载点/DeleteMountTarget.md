# DeleteMountTarget {#doc_api_NAS_DeleteMountTarget .reference}

DeleteMountTarget 用于删除已有挂载点。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=DeleteMountTarget&type=RPC&version=2017-06-26)

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
|RequestId|String|5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8|请求 ID

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

