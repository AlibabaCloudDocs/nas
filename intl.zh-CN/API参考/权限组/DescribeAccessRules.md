# DescribeAccessRules {#doc_api_NAS_DescribeAccessRules .reference}

DescribeAccessRules用于返回权限规则描述。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=DescribeAccessRules&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|是|classic-test|权限组名称

 |
|Action|String|是|DescribeAccessRules|操作接口名，系统规定参数，取值：DescribeAccessRules

 |
|AccessRuleId|String|否|1|规则序号

 |
|FileSystemType|String|否|standard|文件系统类型，可选值：standard、extreme，默认值：standard

 |
|PageNumber|Integer|否|1|列表的分页页码（从 1 开始计数）

 |
|PageSize|Integer|否|1|每个分页包含的权限规则个数（默认 10）

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AccessRules| | |权限规则描述信息

 |
|AccessRuleId|String|1|权限规则ID

 |
|Priority|Integer|1|优先级，范围 1-100，默认值为 1

 |
|RWAccess|String|RDWR|读写权限类型：RDWR（默认）和 RDONLY

 |
|SourceCidrIp|String|10.0.0.1/32|地址或地址段

 |
|UserAccess|String|no\_squash|用户权限类型：no\_squash（默认）、root\_squash 和 all\_squash

 |
|PageNumber|Integer|1|列表的分页页码

 |
|PageSize|Integer|1|每个分页包含的权限规则个数

 |
|RequestId|String|86D89E82-4297-4343-8E1E-A2495B35CC70|请求 ID

 |
|TotalCount|Integer|1|权限规则的总个数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeAccessRules
&AccessGroupName=classic-test
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAccessRulesResponse>
    <AccessRules>
        <AccessRule>
            <SourceCidrIp>10.0.0.1/32</SourceCidrIp>
            <AccessRuleId>1</AccessRuleId>
            <RWAccess>RDWR</RWAccess>
            <UserAccess>no_squash</UserAccess>
            <Priority>1</Priority>
        </AccessRule>
    </AccessRules>
    <PageNumber>1</PageNumber>
    <TotalCount>1</TotalCount>
    <PageSize>1</PageSize>
    <RequestId>86D89E82-4297-4343-8E1E-A2495B35CC70</RequestId>
</DescribeAccessRulesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"AccessRules":{
		"AccessRule":[
			{
				"SourceCidrIp":"10.0.0.1/32",
				"AccessRuleId":"1",
				"RWAccess":"RDWR",
				"UserAccess":"no_squash",
				"Priority":1
			}
		]
	},
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":1,
	"RequestId":"86D89E82-4297-4343-8E1E-A2495B35CC70"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

