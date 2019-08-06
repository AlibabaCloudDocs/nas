# DeleteSnapshot {#doc_api_NAS_DeleteSnapshot .reference}

You can call this operation to delete a snapshot. If you call this operation to delete a snapshot that is being created, the task of creating the snapshot is canceled.

## Description {#description .section}

If the specified snapshot ID does not exist, the request is discarded.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=DeleteSnapshot&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|SnapshotId|String|Yes|s-extreme-snapshotid1| The ID of the snapshot.

 |
|Action|String|Yes|DeleteSnapshot| The operation that you want to perform. Set this parameter to DeleteSnapshot.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. The request ID is returned, regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteSnapshot
&SnapshotId=s-extreme-6tmsbas6ljhwhlkh9
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

## Error codes {#section_cd2_6zh_rrm .section}

