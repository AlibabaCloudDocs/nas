# ResetFileSystem {#doc_api_NAS_ResetFileSystem .reference}

You can call this operation to restore a file system to the status when a snapshot was created.

## Description {#description .section}

-   The file system must be functioning as expected.
-   The specified snapshot ID must be the ID of a snapshot that was created for the file system.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=ResetFileSystem&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|FileSystemId|String|Yes|extreme-012ddfsdf| The ID of the file system.

 |
|snapshotId|String|Yes|s-extreme-snapshotid1| The ID of the snapshot to which the file system is restored.

 |
|Action|String|Yes|ResetFileSystem| The operation that you want to perform. Set this parameter to ResetFileSystem.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ResetFileSystem
&FileSystemId=extreme-xoxo
&SnapshotId=s-extreme-67pxwk9aevrkrwwj8
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

## Error codes {#section_6uv_5y4_kw3 .section}

