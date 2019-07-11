# DescribeRegions {#doc_api_NAS_DescribeRegions .reference}

DescribeRegions用于返回所有 RegionId。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=DescribeRegions)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeRegions|操作接口名，系统规定参数，取值：DescribeRegions

 |
|FileSystemType|String|否|standard|文件系统类型，可选值：standard、extreme，默认值：standard

 |
|PageNumber|Integer|否|1|列表的分页页码（从 1 开始计数）

 |
|PageSize|Integer|否|2|每个分页包含的区域个数（默认 10）

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|列表的分页页码

 |
|PageSize|Integer|2|每个分页包含的区域个数

 |
|Regions| | |区域的描述信息

 |
|LocalName|String|华东1|Region名称

 |
|RegionEndpoint|String|nas.cn-hangzhou.aliyuncs.com|对应地域的服务入口地址

 |
|RegionId|String|cn-hangzhou|RegionID

 |
|RequestId|String|A70BEE5D-76D3-49FB-B58F-1F398211A5C3|请求ID

 |
|TotalCount|Integer|4|返回区域信息的总个数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeRegions
&PageSize=2
&PageNumber=1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeRegionsResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>4</TotalCount>
  <PageSize>2</PageSize>
  <RequestId>A70BEE5D-76D3-49FB-B58F-1F398211A5C3</RequestId>
  <Regions>
    <Region>
      <RegionId>cn-hangzhou</RegionId>
      <RegionEndpoint>nas.cn-hangzhou.aliyuncs.com</RegionEndpoint>
      <LocalName>华东1</LocalName>
    </Region>
    <Region>
      <RegionId>cn-shanghai</RegionId>
      <RegionEndpoint>nas.cn-shanghai.aliyuncs.com</RegionEndpoint>
      <LocalName>华东2</LocalName>
    </Region>
  </Regions>
</DescribeRegionsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":4,
	"PageSize":2,
	"RequestId":"A70BEE5D-76D3-49FB-B58F-1F398211A5C3",
	"Regions":{
		"Region":[
			{
				"RegionId":"cn-hangzhou",
				"RegionEndpoint":"nas.cn-hangzhou.aliyuncs.com",
				"LocalName":"华东1"
			},
			{
				"RegionId":"cn-shanghai",
				"RegionEndpoint":"nas.cn-shanghai.aliyuncs.com",
				"LocalName":"华东2"
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

