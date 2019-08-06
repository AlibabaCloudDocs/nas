# CancelAutoSnapshotPolicy {#doc_api_NAS_CancelAutoSnapshotPolicy .reference}

You can call this operation to disable automatic snapshot policies for one or more file systems.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=CancelAutoSnapshotPolicy&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|FileSystemIds|String|Yes|extreme-233e6ylv0,extreme-23vbpbi03,extreme-23vasz3ds| The IDs of file systems. You can specify a maximum of 100 file system IDs at a time. If you want to disable automatic snapshot policies for multiple file systems, separate each ID with a comma \(,\).

 |
|Action|String|Yes|CancelAutoSnapshotPolicy| The operation that you want to perform. Set this parameter to CancelAutoSnapshotPolicy.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. The request ID is returned, regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CancelAutoSnapshotPolicy
&FileSystemIds=extreme-xxx
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

## Error codes {#section_klf_fdl_jqr .section}

