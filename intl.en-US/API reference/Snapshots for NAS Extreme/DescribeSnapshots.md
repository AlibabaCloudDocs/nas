# DescribeSnapshots {#doc_api_NAS_DescribeSnapshots .reference}

You can call this operation to query the list of all snapshots of the file system.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=DescribeSnapshots&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|FileSystemType|String|Yes|extreme| The type of the file system. Valid value: extreme.

 |
|Action|String|No|DescribeSnapshots| The operation that you want to perform. Set this parameter to DescribeSnapshots.

 |
|FileSystemId|String|No|extreme-22fd123| The ID of the file system.

 |
|PageNumber|Integer|No|1| The page number that you query in the snapshot list, which starts from 1. Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries on each page. Maximum value: 100. Default value: 10.

 |
|SnapshotIds|String|No|s-extreme-xxxxxxxxx,s-extreme-yyyyyyyyy,s-extreme-zzzzzzzzz| The IDs of snapshots. You can specify a maximum of 100 snapshot IDs at a time. You must separate each snapshot ID with a comma \(,\).

 |
|SnapshotName|String|No|FinanceJoshua| The name of the snapshot.

 |
|SnapshotType|String|No|all| The type of the snapshot. Default value: all. Valid values:

 -   auto: automatic snapshots.
-   user: manual snapshots.
-   all: either automatic or manual snapshots.

 |
|Status|String|No|all| The status of the snapshot. Default value: all. Valid values:

 -   progressing: The snapshot is being created.
-   accomplished: The snapshot is created.
-   failed: The snapshot creation failed.
-   all: The status of the snapshot is progressing, accomplished, or failed.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1| The page number that you query in the snapshot list.

 |
|PageSize|Integer|10| The number of entries on each page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|Snapshots| | | The details of snapshots.

 |
|CreateTime|String|2014-07-24T13:00:52Z| The time when the snapshot is created. The time is displayed in UTC. The time follows the [ISO 8601](https://help.aliyun.com/document_detail/25696.html) standard in the format of yyyy-MM-ddThh:mmZ.

 |
|Description|String|FinanceDept| The description of the snapshot.

 |
|Progress|String|100| The progress of a snapshot being created. Unit: percent \(%\).

 |
|RemainTime|Integer|38| The remaining time until a snapshot is created. Unit: seconds.

 |
|RetentionDays|Integer|30| The number of days that an automatic snapshot is retained.

 |
|SnapshotId|String|s-extreme-snapshotid1| The ID of the snapshot.

 |
|SnapshotName|String|FinanceJoshua| The name of the snapshot. This parameter is returned if a name was specified for the snapshot during creation.

 |
|SourceFileSystemId|String|extreme-012321d| The ID of the source file system. After the source file system of a snapshot is deleted, this parameter remains the same.

 |
|SourceFileSystemSize|Long|2000| The capacity of the source file system. Unit: GB.

 |
|Status|String|accomplished| The status of the snapshot. Valid values: progressing, accomplished, and failed.

 |
|TotalCount|Integer|36| The total number of snapshots.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeSnapshots
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
	"PageSize":10,
	"RequestId":"DBECAD38-CFA8-4799-A746-BAEF6ABA0C4F",
	"Snapshots":{
		"Snapshot":[
			{
				"Status":"progressing ",
				"Description":"",
				"SnapshotName":"xoxo ",
				"CreateTime":"1563791255 ",
				"RemainTime":0,
				"SnapshotId":"s-extreme-67pxwk9aevrkrwwj8 ",
				"SourceFileSystemSize":1,
				"RetentionDays":-1,
				"SourceFileSystemId":"extreme-06d8cac6",
				"Progress":"0"
			}
		]
	}
}
```

## Error codes {#section_30v_opo_62a .section}

