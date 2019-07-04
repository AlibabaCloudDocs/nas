# DescribeAccessGroups {#doc_api_NAS_DescribeAccessGroups .reference}

DescribeAccessGroups用于返回权限组描述信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=DescribeAccessGroups)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|否|classic-test|权限组名称

 |
|Action|String|否|DescribeAccessGroups|操作接口名，系统规定参数，取值：DescribeAccessGroups

 |
|FileSystemType|String|否|standard|文件系统类型，可选值：standard、extreme，默认值：standard

 |
|PageNumber|Integer|否|1|列表的分页页码（从1开始计数）

 |
|PageSize|Integer|否|2|每个分页包含的权限组个数（默认10）

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AccessGroups| | |权限组描述信息

 |
|AccessGroupName|String|classic-test|权限组名称

 |
|AccessGroupType|String|Classic|权限组类型，包括 Vpc 和 Classic

 |
|Description|String|This is a classic test access group~|权限组描述信息

 |
|MountTargetCount|Integer|0|引入此权限组的挂载点数

 |
|RuleCount|Integer|0|此权限组中包含的权限规则数

 |
|PageNumber|Integer|1|列表的分页页码

 |
|PageSize|Integer|2|每个分页包含的权限组个数

 |
|RequestId|String|2514F97E-FFF0-4A1F-BF04-729CEAC64B6F|请求ID

 |
|TotalCount|Integer|2|权限组的总个数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeAccessGroups
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAccessGroupsResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>2</TotalCount>
  <PageSize>2</PageSize>
  <RequestId>3E569F4A-F743-490B-AC01-A8088F5C17A1</RequestId>
  <AccessGroups>
    <AccessGroup>
      <Description>DEFAULT ACCESS GROUP NAME</Description>
      <RuleCount>1</RuleCount>
      <AccessGroupType>Vpc</AccessGroupType>
      <AccessGroupName>DEFAULT_VPC_GROUP_NAME</AccessGroupName>
      <MountTargetCount>8</MountTargetCount>
    </AccessGroup>
    <AccessGroup>
      <Description>This is a classic test access group~</Description>
      <RuleCount>0</RuleCount>
      <AccessGroupType>Classic</AccessGroupType>
      <AccessGroupName>classic-test</AccessGroupName>
      <MountTargetCount>0</MountTargetCount>
    </AccessGroup>
  </AccessGroups>
</DescribeAccessGroupsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"PageSize":2,
	"RequestId":"2514F97E-FFF0-4A1F-BF04-729CEAC64B6F",
	"AccessGroups":{
		"AccessGroup":[
			{
				"Description":"DEFAULT ACCESS GROUP NAME",
				"RuleCount":1,
				"AccessGroupType":"Vpc",
				"AccessGroupName":"DEFAULT_VPC_GROUP_NAME",
				"MountTargetCount":8
			},
			{
				"Description":"This is a classic test access group~",
				"RuleCount":0,
				"AccessGroupType":"Classic",
				"AccessGroupName":"classic-test",
				"MountTargetCount":0
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

