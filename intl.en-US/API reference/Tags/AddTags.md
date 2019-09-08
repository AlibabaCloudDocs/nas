# AddTags {#doc_api_NAS_AddTags .reference}

You can call this operation to add one or multiple tags to a file system.

## Description {#description .section}

-   Each tag is composed of a key \(TagKey\) and a value \(TagValue\).
-   The placeholders at the start or end of the TagKey and TagValue, such as \\t, \\n, and \\r are automatically deleted.
-   A TagKey cannot be an empty string, but a TagValue can be an empty string.
-   A TagKey and TagValue are case insensitive.
-   A TagKey can contain a maximum of 64 characters. A TagValue can contain a maximum of 128 characters.
-   You can add a maximum of 10 tags to a file system at a time. If you specify two tags with the same TagKey, the second tag added to the file system will replace the first tag.
-   If a tag is removed from all file systems, the tag itself is automatically deleted.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=AddTags&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AddTags| The operation that you want to perform. Set this parameter to AddTags.

 |
|FileSystemId|String|Yes|0addcw13cd| The ID of the file system.

 |
|Tag.N.Key|String|No|keyN| The key \(TagKey\) of Tag N. The tag you want to add to a file system is composed of a TagKey and TagValue. You can specify a maximum of 10 tags at a time. A TagKey cannot be an empty string, but a TagValue can be an empty string.

 |
|Tag.N.Value|String|No|valueN| The value \(TagValue\) of Tag N. The tag you want to add to a file system is composed of a TagKey and TagValue. You can specify a maximum of 10 tags at a time. A TagKey cannot be an empty string, but a TagValue can be an empty string.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|98696EF0-1607-4E9D-B01D-F20930B68845| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=AddTags
&FileSystemId=109c042666
&Tag.1.Key=test_key
&Tag.1.Value=test_value
&<Common request parameters>

```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<AddTagsResponse>
    <RequestId>98696EF0-1607-4E9D-B01D-F20930B68845</RequestId>
</AddTagsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"98696EF0-1607-4E9D-B01D-F20930B68845"
}
```

## Error codes {#section_py8_fcf_aih .section}

