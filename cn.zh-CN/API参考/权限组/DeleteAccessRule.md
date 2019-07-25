# DeleteAccessRule {#doc_api_NAS_DeleteAccessRule .reference}

DeleteAccessRule用于删除已有权限规则。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=DeleteAccessRule&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|是|classic-test|权限组名称

 |
|AccessRuleId|String|是|1|规则序号

 |
|Action|String|否|DeleteAccessRule|操作接口名，系统规定参数，取值：DeleteAccessRule

 |
|FileSystemType|String|否|standard|文件系统类型，可选值：standard、extreme，默认值：standard

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|5B4511A7-C99E-4071-AA8C-32E2529DA963|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessRule
&AccessGroupName=classic-test
&AccessRuleId=1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteAccessRuleResponse>
    <RequestId>5B4511A7-C99E-4071-AA8C-32E2529DA963</RequestId>
</DeleteAccessRuleResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"5B4511A7-C99E-4071-AA8C-32E2529DA963"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

