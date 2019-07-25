# CreateMountTarget {#doc_api_NAS_CreateMountTarget .reference}

CreateMountTarget用于创建挂载点。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=CreateMountTarget&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|是|classic-test|权限组名称

 |
|FileSystemId|String|是|174494b666|文件系统 ID

 |
|NetworkType|String|是|vpc|网络类型，包括 VPC 和 Classic

 |
|Action|String|否|CreateMountTarget|操作接口名，系统规定参数，取值：CreateMountTarget

 |
|VSwitchId|String|否|vsw-2zevmwkwyztjuoffgdiwl|交换机 ID

 |
|VpcId|String|否|vpc-2zesj9afh3y518k9oe86q|VPC 网络 ID

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|MountTargetDomain|String|174494b666-xog95.cn-hangzhou.nas.aliyuncs.com|挂载点域名

 |
|RequestId|String|70EACC9C-D07A-4A34-ADA4-77506C42B023|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateMountTarget
&AccessGroupName=classic-test
&FileSystemId=174494b666
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

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

