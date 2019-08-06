# ApplyAutoSnapshotPolicy {#doc_api_NAS_ApplyAutoSnapshotPolicy .reference}

You can call this operation to apply an automatic snapshot policy to one or more file systems. If an automatic snapshot policy is applied to a file system, you can call this operation to change the policy.

## Description {#description .section}

-   You can only apply one automatic snapshot policy to each file system.
-   An automatic snapshot policy can be applied to multiple file systems.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=ApplyAutoSnapshotPolicy&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|AutoSnapshotPolicyId|String|Yes|sp-extreme-233e6ylv0| The ID of the automatic snapshot policy.

 |
|FileSystemIds|String|Yes|extreme-233e6ylv0,extreme-23vbpbi03,extreme-23vasz3ds| The IDs of the file systems. You can specify a maximum of 100 file system IDs at a time. You must separate each ID with a comma \(,\).

 |
|Action|String|Yes|ApplyAutoSnapshotPolicy| The operation that you want to perform. Set this parameter to ApplyAutoSnapshotPolicy.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ApplyAutoSnapshotPolicy
&AutoSnapshotPolicyId=sp-extreme-6i0brwewjt0gfylh0
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

## Error codes {#section_2f3_swy_boc .section}

