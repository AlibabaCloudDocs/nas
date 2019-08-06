# CreateAutoSnapshotPolicy {#doc_api_NAS_CreateAutoSnapshotPolicy .reference}

You can call this operation to create an automatic snapshot policy. After a policy is created, you can call the ApplyAutoSnapshotPolicy operation to apply the policy to one or more file systems and call the ModifyAutoSnapshotPolicy operation to modify the policy.

## Description {#description .section}

-   You can use an Alibaba Cloud account to create a maximum of 100 automatic snapshot policies for one region.
-   The creation of an automatic snapshot is canceled if the scheduled time for creating the snapshot is reached but the previous automatic snapshot is still being created. This may occur if the file system stores a large volume of data. For example, you have scheduled snapshots to be created at 09:00, 10:00, 11:00, and 12:00. A snapshot starts to be created at 09:00. The creation is completed at 10:20. The process of creating the snapshot requires 80 minutes because the file system has a large volume of data. A snapshot is not created at 10:00, and the next snapshot starts to be created at 11:00.
-   A file system has a maximum of 64 snapshots. If the number of snapshots reaches the maximum, the earliest automatic snapshots are deleted. This rule does not apply to manual snapshots.
-   A change of the snapshot retention period in an automatic snapshot policy only affects new snapshots, and the retention period of snapshots that are already created is not updated.
-   If you want to manually create a snapshot for a file system when an automatic snapshot is being created, you need to wait until the automatic snapshot is created.
-   You cannot apply automatic snapshot policies to an abnormal file system.
-   The format of an automatic snapshot name is auto\_yyyyMMdd\_X. auto indicates an automatic snapshot, which is used to differentiate between automatic and manual snapshots. yyyyMMdd indicates the date when the snapshot is created, where yyyy indicates the year, MM indicates the month, and dd indicates the day. X indicates a unique number to identify the automatic snapshot for the specified day. For example, auto\_20140418\_1 indicates the first automatic snapshot created on April 18, 2014.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=CreateAutoSnapshotPolicy&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|FileSystemType|String|Yes|extreme| The type of the file system. Valid value: extreme.

 |
|RepeatWeekdays|String|Yes|1,2,3| The days of a week on which automatic snapshots are created. Valid values: 1 to 7. For example, 1 indicates Monday. You can specify multiple days if you want to create automatic snapshots on multiple days during the week.

 -   You can specify up to 7 days over a one week period.
-   Separate each day with a comma \(,\).

 |
|TimePoints|String|Yes|0,1,...,23| The time at which automatic snapshots are created, measured in hours. Valid values: 0 to 23. The values indicate a total of 24 hours from 00:00 to 23:00. For example, 1 indicates 01:00. If you want to create multiple automatic snapshots on a specific day, you can specify a maximum of 24 hours.

 |
|Action|String|Yes|CreateAutoSnapshotPolicy| The operation that you want to perform. Set this parameter to CreateAutoSnapshotPolicy.

 |
|AutoSnapshotPolicyName|String|No|FinanceJoshua| The name of the automatic snapshot policy. The name must be 2 to 128 characters in length. It must start with a letter but cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). Default value: empty string.

 |
|RetentionDays|Integer|No|30| The retention period of automatic snapshots. Unit: days. Default value: -1. Valid values:

 -   -1: Automatic snapshots are permanently retained.
-   1-65536: Each automatic snapshot is retained for the specified number of days.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AutoSnapshotPolicyId|String|sp-extreme-233e6ylv0| The ID of the automatic snapshot policy.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateAutoSnapshotPolicy
&FileSystemType=extreme
&RepeatWeekdays=1,2,3
&TimePoints=0,1,2,3,4
&<Common request parameters>
...

```

Sample success response

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"12FA778B-C8D3-4D2B-88AD-C10ED0326C57",
	"AutoSnapshotPolicyId":"sp-extreme-6i0brwewjt0gfylh0"
}
```

## Error codes {#section_yqp_96z_llv .section}

