# CreateAccessRule {#doc_api_NAS_CreateAccessRule .reference}

You can call this operation to create permission rules.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=CreateAccessRule) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description |
|---------|----|--------|-------|------------|
|AccessGroupName|String |Yes|classic-test|The name of the permission group.

 |
|SourceCidrIp|String | Yes|10.0.0.1/32|An IP address or a CIDR notation. For example, 12.1.1.1 or 13.1.1.1/25.

 |
|Action|String |No|CreateAccessRule|The operation that you want to perform. Set the value to CreateAccessRule.

 |
|FileSystemType|String|No|standard|The type of file system. Valid values: standard and extreme. Default value: standard.

 |
|Priority|Integer|No|1|The priority of the rule. Valid values: 1 to 100. Default value: 1.

 |
|RWAccessType|String|No|RDWR|The type of permission. Valid values: RDWR and RDONLY. Default value: RDWR.

 |
|UserAccessType|String|No|no\_squash|The type of user permission. Valid values: no\_squash, root\_squash, and all\_squash. Default value: no\_squash.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description |
|---------|----|-------|------------|
|AccessRuleId|String|1|The rule ID.

 |
|RequestId|String|A323836B-5BC6-45A6-8048-60675C23EE2A|The request ID.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessRule
&AccessGroupName=classic-test
&SourceCidrIp=10.0.0.1/8
&<Common request parameters>

```

Sample success response

`XML` format

``` {#xml_return_success_demo}
<CreateAccessRuleResponse>
  <AccessRuleId>1</AccessRuleId>
  <RequestId>A323836B-5BC6-45A6-8048-60675C23EE2A</RequestId>
</CreateAccessRuleResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"AccessRuleId": "1"
	"RequestId": "A323836B-5BC6-45A6-8048-60675C23EE2A",
}
```

## Error codes { .section}

