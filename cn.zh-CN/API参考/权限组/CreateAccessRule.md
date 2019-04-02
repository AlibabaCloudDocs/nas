# CreateAccessRule {#doc_api_1039803 .reference}

CreateAccessRule用于创建权限规则。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=CreateAccessRule)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|是|classic-test|权限组名称

 |
|Action|String|是|CreateAccessRule|操作接口名，系统规定参数，取值：CreateAccessRule

 |
|SourceCidrIp|String|是|10.0.0.1/32|地址或地址段

 |
|Priority|Integer|否|1|优先级，范围 1-100，默认值为1

 |
|RWAccessType|String|否|RDWR|读写权限类型：RDWR（默认）和 RDONLY

 |
|UserAccessType|String|否|no\_squash|用户权限类型：no\_squash（默认）、root\_squash和all\_squash

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AccessRuleId|String|1|规则序号

 |
|RequestId|String|A323836B-5BC6-45A6-8048-60675C23EE2A|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GEThttps://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessRule
&AccessGroupName=classic-test
&SourceCidrIp=10.0.0.1/32
&<公共请求参数>…

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateAccessRuleResponse>
  <AccessRuleId>1</AccessRuleId>
  <RequestId>A323836B-5BC6-45A6-8048-60675C23EE2A</RequestId>
</CreateAccessRuleResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"AccessRuleId":"1",
	"RequestId":"A323836B-5BC6-45A6-8048-60675C23EE2A"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/NAS)

