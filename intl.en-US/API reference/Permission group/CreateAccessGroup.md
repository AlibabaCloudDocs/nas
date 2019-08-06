# CreateAccessGroup {#doc_api_NAS_CreateAccessGroup .reference}

You can call this operation to create permission groups.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=CreateAccessGroup) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|AccessGroupName|String|Yes|classic-test| The name of the permission group.

 The name of the permission group. The name must be 3 to 64 characters in length. The name must start with a letter and contain letters, numbers, underscores \(\_\), and hyphens \(-\). The name of a new permission group must be different from built-in permission groups, including DEFAULT\_VPC\_GROUP\_NAME and DEFAULT\_CLASSIC\_GROUP\_NAME.|
|AccessGroupType|String|Yes|Classic| The type of permission group. Valid values: Vpc and Classic.

 |
|Action|String|Yes|CreateAccessGroup| The operation that you want to perform. Set the value to CreateAccessGroup.

 |
|Description|String|No|classictestaccessgroup| The description of the permission group. By default, the description of the permission group is the same as the name of the permission group. The description must be 2 to 128 characters in length. The description must start with a letter and cannot start with http:// or https://. The description can contain letters, numbers, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |
|FileSystemType|String|No|standard| The type of file system. Valid values: standard and extreme. Default value: standard.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AccessGroupName|String|classic-test| The name of the permission group.

 |
|RequestId|String|55C5FFD6-BF99-41BD-9C66-FFF39189F4F8| The request ID.

 |

## Examples {#demo .section}

Sample requests:

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessGroup
&AccessGroupName=classic-test
&AccessGroupType=Classic
&Description=classic test access group
&<Common request parameters>

```

Sample success response

`XML` format

``` {#xml_return_success_demo}
<CreateAccessGroupResponse>
  <RequestId>55C5FFD6-BF99-41BD-9C66-FFF39189F4F8</RequestId>
  <AccessGroupName>classic-test</AccessGroupName>
</CreateAccessGroupResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"55C5FFD6-BF99-41BD-9C66-FFF39189F4F8",
	"AccessGroupName ":"classic-test"
}
```

## Error codes {#section_teu_791_mvh .section}

For more information, see [Error codes](https://error-center.alibabacloud.com/status/product/NAS).

