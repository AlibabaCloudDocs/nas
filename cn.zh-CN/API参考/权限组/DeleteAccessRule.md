# DeleteAccessRule {#doc_api_NAS_DeleteAccessRule .reference}

DeleteAccessRule用于删除已有权限规则。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=DeleteAccessRule)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

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
|RequestId|String|5B4511A7-C99E-4071-AA8C-32E2529DA963|请求ID

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

