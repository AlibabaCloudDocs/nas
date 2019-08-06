# ModifyAutoSnapshotPolicy {#doc_api_NAS_ModifyAutoSnapshotPolicy .reference}

You can call this operation to modify an automatic snapshot policy. After you modify an automatic snapshot policy that is applied to some file systems, the updated policy takes immediate effect on the file systems.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=ModifyAutoSnapshotPolicy&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|AutoSnapshotPolicyId|String|Yes|sp-extreme-233e6ylv0|The ID of the automatic snapshot policy. You can call the DescribeAutoSnapshotPolicies operation to view your available automatic snapshot policies.

 |
|Action|String|No|ModifyAutoSnapshotPolicy|The operation that you want to perform. Set this parameter to ModifyAutoSnapshotPolicy.

 |
|AutoSnapshotPolicyName|String|No|FinanceJoshua|The name of the automatic snapshot policy. The policy is only modified if this parameter is specified.

 |
|RepeatWeekdays|String|No|1,7|The days of a week on which automatic snapshots are created. Valid values: 1 to 7. For example, 1 indicates Monday. You can specify multiple days if you want to create automatic snapshots on multiple days during the week.

 -   You can specify up to 7 days over a one week period.
-   You must separate each day with a comma \(,\).

 |
|RetentionDays|Integer|No|30|The retention period of automatic snapshots. Unit: days. Default value: -1. Valid values:

 -   -1: Automatic snapshots are permanently retained.
-   1-65536: Each automatic snapshot is retained for the specified number of days.

 |
|TimePoints|String|No|0,1|The time at which automatic snapshots are created, measured in hours. Valid values: 0 to 23. The values indicate a total of 24 hours from 00:00 to 23:00. For example, 1 indicates 01:00. When you want to create multiple automatic snapshots on a specific day,

 -   you can specify up to 24 hours.
-   You must separate each hour with a comma \(,\).

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description |
|---------|----|-------|------------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. The request ID is returned, regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAutoSnapshotPolicy
&AutoSnapshotPolicyId=sp-extreme-6i0brwewjt0gfylh0
&AutoSnapshotPolicyName=xoxo
&<Common request parameters>
...

```

Sample success response

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"12FA778B-C8D3-4D2B-88AD-C10ED0326C57"
}
```

## Error codes { .section}

