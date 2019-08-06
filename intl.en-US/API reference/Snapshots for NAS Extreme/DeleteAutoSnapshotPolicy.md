# DeleteAutoSnapshotPolicy {#doc_api_NAS_DeleteAutoSnapshotPolicy .reference}

You can call this operation to delete an automatic snapshot policy. If an automatic snapshot policy is applied to a file system, the policy no longer affects the file system after the policy is deleted.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=DeleteAutoSnapshotPolicy&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|AutoSnapshotPolicyId|String|Yes|sp-extreme-233e6ylv0| The ID of the automatic snapshot policy. You can call the DescribeAutoSnapshotPolicies operation to view available automatic snapshot policies.

 |
|Action|String|Yes|DeleteAutoSnapshotPolicy| The operation that you want to perform. Set this parameter to DeleteAutoSnapshotPolicy.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. The request ID is returned, regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteAutoSnapshotPolicy
&AutoSnapshotPolicyId=sp-extreme-6i0brwewjt0gfylh0
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

## Error codes {#section_xca_fwz_gz0 .section}

