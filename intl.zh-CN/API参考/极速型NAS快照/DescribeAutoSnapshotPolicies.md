# DescribeAutoSnapshotPolicies {#doc_api_NAS_DescribeAutoSnapshotPolicies .reference}

DescribeAutoSnapshotPolicies 用于查询您已创建的自动快照策略。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=DescribeAutoSnapshotPolicies&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAutoSnapshotPolicies|系统规定参数。取值：DescribeAutoSnapshotPolicies。

 |
|FileSystemType|String|是|extreme|文件系统类型，可选值：extreme。

 |
|AutoSnapshotPolicyId|String|否|sp-extreme-233e6ylv0|自动快照策略 ID。

 |
|PageNumber|Integer|否|1|自动快照策略返回结果分多页展示。 起始值：1，默认值：1。

 |
|PageSize|Integer|否|10| 

 分页展示返回的自动快照策略时的每页行数。 最大值：100，默认值：10。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoSnapshotPolicies| | |自动快照策略详情，AutoSnapshotPolicyType 组成的集合。

 |
|AutoSnapshotPolicyId|String|FinanceJoshua|自动快照策略 ID。

 |
|AutoSnapshotPolicyName|String|p-23f2i9s4t|自动快照策略的名称。

 |
|CreateTime|String|2014-04-21T12:08:52Z|创建时间。按照 [ISO8601](https://www.iso.org/iso-8601-date-and-time-format.html) 标准表示，并需要使用UTC时间，格式为 yyyy-MM-ddTHH:mm:ssZ。

 |
|FileSystemNums|Integer|2|启用该策略的文件系统数量。

 |
|RegionId|String|cn-hangzhou|自动快照策略所属的地域 ID。

 |
|RepeatWeekdays|String|1,5|指定自动快照的重复日期。选定周一到周日中需要创建快照的日期，参数为 1~7 的数字，如：1 表示周一。允许选择多个日期。

 |
|RetentionDays|Integer|30|指定自动快照的保留时间，单位为天。

 -   -1：永久保存
-   1~65536：指定保存天数

 |
|Status|String|Available|自动快照策略状态，取值：Creating、Available。

 |
|TimePoints|String|4,19|自动快照的创建时间点。最小单位为小时，从 00:00~23:00 共 24 个时间点可选，参数为 0~23 的数字，如：1 代表在01:00时间点。最多 24 个时间点，用半角逗号（,）隔开。

 |
|PageNumber|Integer|1|自动快照策略列表的页码。

 |
|PageSize|Integer|10|分页展示返回的自动快照策略时的每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|TotalCount|Integer|2|自动快照策略的总个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeAutoSnapshotPolicies
&FileSystemType=extreme
&<公共请求参数>
…

```

正常返回示例

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"AutoSnapshotPolicies":{
		"AutoSnapshotPolicy":[
			{
				"AutoSnapshotPolicyName":"",
				"RetentionDays":-1,
				"TimePoints":"0,1,2",
				"FileSystemNums":0,
				"AutoSnapshotPolicyId":"sp-extreme-6i0brwewjt0gfylh0",
				"RepeatWeekdays":"1,2"
			}
		]
	},
	"PageSize":10,
	"RequestId":"B208E2EA-E9CC-40E3-BE0B-4FFDDD9CB54B"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

