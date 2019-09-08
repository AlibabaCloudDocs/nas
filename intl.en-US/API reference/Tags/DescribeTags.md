# DescribeTags {#doc_api_NAS_DescribeTags .reference}

You can call this operation to search by tags added to a specific file system.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=NAS&api=DescribeTags&type=RPC&version=2017-06-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeTags|The operation that you want to perform. Set this parameter to DescribeTags.

 |
|FileSystemId|String|No|0addcw13cd|The ID of the file system.

 |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

 |
|PageSize|Integer|No|1|The number of tags to return on each page. Default value: 10.

 |
|Tag.N.Key|String|No|keyN|The key \(TagKey\) of Tag N. The tag that you want to search by includes a TagKey and TagValue. You can specify a maximum of 10 tags at a time. A TagKey cannot be an empty string, but a TagValue can be an empty string.

 |
|Tag.N.Value|String|No|valueN|The value \(TagValue\) of Tag N. The tag that you want to search by includes a TagKey and TagValue. You can specify a maximum of 10 tags at a time. A TagKey cannot be an empty string, but a TagValue can be an empty string.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The number of the page to return.

 |
|PageSize|Integer|1|The number of file systems to return on each page.

 |
|RequestId|String|035B3A3A-E514-4B41-B906-5D906CFBD65F|The ID of the request.

 |
|Tags| | |The tags that match all the filtering conditions.

 |
|FileSystemIds| |109c042666|The IDs of the file systems with added tags.

 |
|Key|String|key1|The key of the tag.

 |
|Value|String|value1|The value of the tag.

 |
|TotalCount|Integer|1|The total number of file systems.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeTags
&FileSystemId=109c042666
&<Common request parameters>

```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<DescribeTagsResponse>
    <Tags>
        <Tag>
            <Key>key1</Key>
            <Value>value1</Value>
            <FileSystemIds>
                <FileSystemId>109c042666</FileSystemId>
            </FileSystemIds>
        </Tag>
    </Tags>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TotalCount>1</TotalCount>
    <RequestId>035B3A3A-E514-4B41-B906-5D906CFBD65F</RequestId>
</DescribeTagsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"Tags":{
		"Tag":[
			{
				"FileSystemIds":{
					"FileSystemId":[
						"109c042666"
					]
				},
				"Value":"value1",
				"Key":"key1"
			}
		]
	},
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"035B3A3A-E514-4B41-B906-5D906CFBD65F"
}
```

## Error codes { .section}

