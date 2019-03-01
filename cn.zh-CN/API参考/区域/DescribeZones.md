# DescribeZones {#doc_api_1037012 .reference}

DescribeZones用于查询某个 Region 下的所有可用区及可用区所支持的 NAS 类型。

只发布国内站

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=DescribeZones)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeZones|操作接口名，系统规定参数，取值：DescribeZones

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|A70BEE5D-76D3-49FB-B58F-1F398211A5C3|请求ID

 |
|Zones| | |每个元素是一个Zone

 |
|└Capacity| |1|容量型存储

 |
|└Performance| |0|性能型存储

 |
|└ZoneId|String|cn-hangzhou-b|可用区ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeZones
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeZones>
  <RequestId>A70BEE5D-76D3-49FB-B58F-1F398211A5C3</RequestId>
  <Zones>
    <Zone>
      <Performance/>
      <Capacity>
        <Protocol>nfs</Protocol>
        <Protocol>smb</Protocol>
        <Protocol>nasplus</Protocol>
      </Capacity>
      <ZoneId>cn-hangzhou-b</ZoneId>
    </Zone>
    <Zone>
      <Performance>
        <Protocol>nfs</Protocol>
        <Protocol>smb</Protocol>
      </Performance>
      <Capacity>
        <Protocol>nfs</Protocol>
        <Protocol>smb</Protocol>
        <Protocol>nasplus</Protocol>
      </Capacity>
      <ZoneId>cn-hangzhou-g</ZoneId>
    </Zone>
    <Zone>
      <Performance>
        <Protocol>nfs</Protocol>
        <Protocol>smb</Protocol>
        <Protocol>newnfs</Protocol>
      </Performance>
      <Capacity/>
      <ZoneId>cn-hangzhou-f</ZoneId>
    </Zone>
  </Zones>
</DescribeZones>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"A70BEE5D-76D3-49FB-B58F-1F398211A5C3",
	"Zones":{
		"Zone":[
			{
				"ZoneId":"cn-hangzhou-b",
				"Capacity":{
					"Protocol":[
						"nfs",
						"smb",
						"nasplus"
					]
				},
				"Performance":{
					"Protocol":[]
				}
			},
			{
				"ZoneId":"cn-hangzhou-g",
				"Capacity":{
					"Protocol":[
						"nfs",
						"smb",
						"nasplus"
					]
				},
				"Performance":{
					"Protocol":[
						"nfs",
						"smb"
					]
				}
			},
			{
				"ZoneId":"cn-hangzhou-f",
				"Capacity":{
					"Protocol":[]
				},
				"Performance":{
					"Protocol":[
						"nfs",
						"smb",
						"newnfs"
					]
				}
			}
		]
	}
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/NAS)

