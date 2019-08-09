# ModifyAccessGroup {#doc_api_NAS_ModifyAccessGroup .reference}

ModifyAccessGroup用于修改权限组。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=ModifyAccessGroup&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|是|classic-test|权限组名称

 |
|Action|String|是|ModifyAccessGroup|操作接口名，系统规定参数，取值：ModifyAccessGroup

 |
|Description|String|否|classic-test|权限组描述，默认和名称相同，长度为 2~128 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）

 |
|FileSystemType|String|否|standard|文件系统类型，可选值：standard、extreme，默认值：standard

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|ED2AE737-9D50-4CA4-B0DA-31BD610C2363|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAccessGroup
&AccessGroupName=classic-test
&Description=classic-test
&<公共请求参数>…

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyAccessGroupResponse>
    <RequestId>ED2AE737-9D50-4CA4-B0DA-31BD610C2363</RequestId>
</ModifyAccessGroupResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"ED2AE737-9D50-4CA4-B0DA-31BD610C2363"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

