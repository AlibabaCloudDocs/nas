# DescribeTags {#doc_api_NAS_DescribeTags .reference}

查询已有标签。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=DescribeTags&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeTags|系统规定参数。取值：DescribeTags。

 |
|FileSystemId|String|否|0addcw13cd|文件系统ID。

 |
|PageNumber|Integer|否|1|列表的分页页码，从1开始计数 。

 |
|PageSize|Integer|否|1|每个分页包含的标签数，默认值：10。

 |
|Tag.N.Key|String|否|keyN|当前第N组标签键（TagKey）。需要查询的标签，包括标签键（TagKey）和标签值（TagValue），单次最多支持传入10组值。标签键（TagKey）不能为空，标签值（TagValue）可以为空。

 |
|Tag.N.Value|String|否|valueN|当前第N组标签值（TagValue）。需要查询的标签，包括标签键（TagKey）和标签值（TagValue），单次最多支持传入10组值。标签键（TagKey）不能为空，标签值（TagValue）可以为空。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|列表的分页页码。

 |
|PageSize|Integer|1|每个分页包含的文件系统个数。

 |
|RequestId|String|035B3A3A-E514-4B41-B906-5D906CFBD65F|请求ID。

 |
|Tags| | |满足所有筛选条件的标签。

 |
|FileSystemIds| |109c042666|绑定的文件系统ID。

 |
|Key|String|key1|标签键。

 |
|Value|String|value1|标签值。

 |
|TotalCount|Integer|1|文件系统总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeTags
&FileSystemId=109c042666
&<公共请求参数>

```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/NAS)查看更多错误码。

