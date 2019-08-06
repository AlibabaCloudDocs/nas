# CreateSnapshot {#doc_api_NAS_CreateSnapshot .reference}

You can call this operation to create a snapshot.

## Description {#description .section}

-   You can create a maximum of 64 snapshots for each file system.
-   The instance on which the file system is mounted must be in the normal status. Otherwise, snapshots cannot be created.
-   You can only create one snapshot for a file system at a time.
-   If the file system expires while a snapshot is being created, the snapshot is deleted when the file system is released.
-   Creating a snapshot may temporarily reduce I/O performance of the file system. We recommend that you do not create snapshots during peak hours.
-   A snapshot only records the data of the file system at a specific time point. It does not record the incremental data generated while the snapshot is being created.
-   Snapshots you create always exist unless you delete them. We recommend that you regularly delete unnecessary snapshots to prevent extra fees incurred by increasing snapshot storage.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=CreateSnapshot&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|FileSystemId|String|Yes|Extreme-01ddddfc| The ID of the file system.

 |
|Action|String|Yes|CreateSnapshot| The operation that you want to perform. Set this parameter to CreateSnapshot.

 |
|Description|String|No|FinanceDepet| The description of the snapshot. The description must be 2 to 256 characters in length. It cannot start with http:// or https://. Default value: empty string.

 |
|RetentionDays|Integer|No|30| The retention period of the snapshot. Unit: day. The snapshot is automatically deleted when its retention period ends. Default value: -1.

 Valid values:

 -   -1: The snapshot is permanently retained.
-   1-65536: The snapshot is retained for the specified number of days.

 |
|SnapshotName|String|No|FinanceJoshua| The name of the snapshot. The name must be 2 to 128 characters in length. It must start with a letter but cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It cannot start with auto because a name that starts with auto may conflict with the names of automatic snapshots.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|SnapshotId|String|s-extreme-snapshotid1| The ID of the snapshot.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateSnapshot
&FileSystemId=1ca404a348
&<Common request parameters>
...

```

Sample success response

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"AB78A546-A85A-44E7-B4A3-C0AAA77B89AF",
	"SnapshotId":"s-extreme-6tmsbas6ljhwhlkh9"
}
```

## Error codes {#section_nu8_cbw_eiy .section}

