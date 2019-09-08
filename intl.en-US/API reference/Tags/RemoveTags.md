# RemoveTags {#doc_api_NAS_RemoveTags .reference}

You can call this operation to remove one or multiple tags from a file system.

## Description {#description .section}

A request ID is returned even if the tag that you want to remove or the associated file system does not exist. For example, if the associated file system does not exist, or the TagKey and TagValue cannot be found, a request ID is returned.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=RemoveTags&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RemoveTags|The operation that you want to perform. Set this parameter to RemoveTags.

 |
|FileSystemId|String|Yes|0addcw13cd|The ID of the file system.

 |
|Tag.N.Key|String|No|keyN|The key \(TagKey\) of Tag N. Each tag that you want to remove includes a TagKey and TagValue. You can specify 1 to 10 tags at a time. A TagKey cannot be an empty string, but a TagValue can be an empty string.

 |
|Tag.N.Value|String|No|valueN|The value \(TagValue\) of Tag N. Each tag that you want to remove includes a TagKey and TagValue. You can specify a maximum of 5 tags at a time. A TagKey cannot be an empty string, but a TagValue can be an empty string.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|98696EF0-1607-4E9D-B01D-F20930B68845|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=RemoveTags
&FileSystemId=109c042666
&Tag.1.Key=test_key
&<Common request parameters>

```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<RemoveTagsResponse>
    <RequestId>98696EF0-1607-4E9D-B01D-F20930B68845</RequestId>
</RemoveTagsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"98696EF0-1607-4E9D-B01D-F20930B68845"
}
```

## Error codes { .section}

