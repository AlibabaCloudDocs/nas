# DescribeMountTargets {#doc_api_1038864 .reference}

DescribeMountTargets用于返回挂载点描述信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeMountTargets|操作接口名，系统规定参数，取值：DescribeMountTargets

 |
|FileSystemId|String|是|1ca404a666|文件系统 ID

 |
|MountTargetDomain|String|否|1ca404a666-xog95.cn-hangzhou.nas.aliyuncs.com|挂载点域名

 |
|PageNumber|Integer|否|1|列表的分页页码（从1开始计数）

 |
|PageSize|Integer|否|1|每个分页包含的挂载点个数（默认 10）

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|MountTargets| | |挂载点描述信息

 |
|└AccessGroup|String|DEFAULT\_VPC\_GROUP\_NAME|权限组

 |
|└MountTargetDomain|String|1ca404a666-wxa89.cn-hangzhou.nas.aliyuncs.com|挂载点域名

 |
|└NetworkType|String|Vpc|网络类型 ，包括 Vpc 和 Classic

 |
|└Status|String|Active|状态，包括 Active、Inactive 和 Creating

 |
|└VpcId|String|vpc-2zesj9afh3y518k9oe86q|VPC 网络 ID

 |
|└VswId|String|vsw-2zevmwkwyztjuoffgdiwl|交换机 ID

 |
|PageNumber|Integer|1|列表的分页页码

 |
|PageSize|Integer|1|每个分页包含的挂载点个数

 |
|RequestId|String|3BAB90FD-B4A0-48DA-9F09-2B963510A0EF|请求ID

 |
|TotalCount|Integer|1|挂载点的总个数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GEThttps://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeMountTargets
&FileSystemId=1ca404a666
&<公共请求参数>…

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeMountTargetsResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>1</TotalCount>
  <PageSize>1</PageSize>
  <RequestId>3BAB90FD-B4A0-48DA-9F09-2B963510A0EF</RequestId>
  <MountTargets>
    <MountTarget>
      <Status>Active</Status>
      <NetworkType>Vpc</NetworkType>
      <VswId>vsw-2zevmwkwyztjuoffgdiwl</VswId>
      <VpcId>vpc-2zesj9afh3y518k9oe86q</VpcId>
      <MountTargetDomain>1ca404a666-wxa89.cn-hangzhou.nas.aliyuncs.com</MountTargetDomain>
      <AccessGroup>DEFAULT_VPC_GROUP_NAME</AccessGroup>
    </MountTarget>
  </MountTargets>
</DescribeMountTargetsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":1,
	"RequestId":"3BAB90FD-B4A0-48DA-9F09-2B963510A0EF",
	"MountTargets":{
		"MountTarget":[
			{
				"NetworkType":"Vpc",
				"Status":"Active",
				"VswId":"vsw-2zevmwkwyztjuoffgdiwl",
				"MountTargetDomain":"1ca404a666-wxa89.cn-hangzhou.nas.aliyuncs.com",
				"VpcId":"vpc-2zesj9afh3y518k9oe86q",
				"AccessGroup":"DEFAULT_VPC_GROUP_NAME"
			}
		]
	}
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/NAS)

