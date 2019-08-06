# DescribeAutoSnapshotPolicies {#doc_api_NAS_DescribeAutoSnapshotPolicies .reference}

You can call this operation to query the automatic snapshot policies you have created.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=DescribeAutoSnapshotPolicies&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|FileSystemType|String|Yes|extreme| The type of the file system. Valid value: extreme.

 |
|Action|String|Yes|DescribeAutoSnapshotPolicies| The operation that you want to perform. Set this parameter to DescribeAutoSnapshotPolicies.

 |
|AutoSnapshotPolicyId|String|No|sp-extreme-233e6ylv0| The ID of the automatic snapshot policy.

 |
|PageNumber|Integer|No|1| The page number that you query, which starts from 1. Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries on each page. Maximum value: 100. Default value: 10.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AutoSnapshotPolicies| | | The details of the automatic snapshot policies.

 |
|AutoSnapshotPolicyId|String|FinanceJoshua| The ID of the automatic snapshot policy.

 |
|AutoSnapshotPolicyName|String|p-23f2i9s4t| The name of the automatic snapshot policy.

 |
|CreateTime|String|2014-04-21T12:08:52Z| The time when the automatic snapshot policy was created. The time follows the [ISO 8601](https://help.aliyun.com/document_detail/25696.html) standard in the format of yyyy-MM-ddTHH:mm:ssZ. The time is displayed in UTC.

 |
|FileSystemNums|Integer|2| The number of file systems to which the automatic snapshot policy applies.

 |
|RegionId|String|cn-hangzhou| The ID of the region to which the automatic snapshot policy belongs.

 |
|RepeatWeekdays|String|1,5| The days of a week on which automatic snapshots are created. Valid values: 1 to 7. For example, 1 indicates Monday. One or more days can be specified.

 |
|RetentionDays|Integer|30| The retention period of automatic snapshots. Unit: days. Default value: -1. Valid values: -1 and 1-65536.

-   The value -1 indicates that automatic snapshots are permanently retained.
-   A value in the range of 1 to 65536 indicates that each automatic snapshot is retained for the specified number of days.

 |
|Status|String|Available| The status of the snapshot. Valid values: Creating and Available.

 |
|TimePoints|String|4,19| The time at which automatic snapshots are created, measured in hours. Valid values: 0 to 23. The values indicate a total of 24 hours from 00:00 to 23:00. For example, 1 indicates 01:00. Up to 24 hours can be specified. such as 0,1,...,23. Each hour is separated with a comma \(,\).

 |
|PageNumber|Integer|1| The number of the page that you query.

 |
|PageSize|Integer|10| The number of entries on each page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TotalCount|Integer|2| The total number of automatic snapshot policies.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeAutoSnapshotPolicies
&FileSystemType=extreme
&<Common request parameters>
...

```

Sample success response

`JSON` format

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

## Error codes {#section_7cx_7qc_3vu .section}

