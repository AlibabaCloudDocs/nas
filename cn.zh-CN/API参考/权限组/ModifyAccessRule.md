# ModifyAccessRule {#doc_api_1038894 .reference}

ModifyAccessRule用于修改权限规则。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=ModifyAccessRule)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|是|classic-test|权限组名称

 |
|AccessRuleId|String|是|1|规则序号

 |
|Action|String|是|ModifyAccessRule|操作接口名，系统规定参数，取值：ModifyAccessRule

 |
|Priority|Integer|否|1|优先级，范围 1-100，默认值为 1

 |
|RWAccessType|String|否|RDWR|读写权限类型

 |
|SourceCidrIp|String|否|192.168.0.1|地址或地址段

 |
|UserAccessType|String|否|all\_squash|用户权限类型

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|6299428C-3861-435D-AE54-9B330A0007C8|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GEThttps://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAccessRule
&AccessGroupName=classic-test
&AccessRuleId=1
&SourceCidrIp=192.168.0.1
&RWAccessType=RDWR
&UserAccessType=all_squash
&<公共请求参数>…

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyAccessRuleResponse>
  <RequestId>6299428C-3861-435D-AE54-9B330A0007C8</RequestId>
</ModifyAccessRuleResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"6299428C-3861-435D-AE54-9B330A0007C8"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/NAS)

