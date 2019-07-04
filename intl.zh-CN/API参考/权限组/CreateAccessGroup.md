# CreateAccessGroup {#doc_api_NAS_CreateAccessGroup .reference}

CreateAccessGroup用于创建权限组。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=CreateAccessGroup)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|是|classic-test|权限组名称

 |
|AccessGroupType|String|是|Classic|权限组类型，包括 Vpc和 Classic

 |
|Action|String|否|CreateAccessGroup|操作接口名，系统规定参数，取值：CreateAccessGroup

 |
|Description|String|否|classictestaccessgroup|权限组描述，默认和名称相同

 |
|FileSystemType|String|否|standard|文件系统类型，可选值：standard、extreme，默认值：standard

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AccessGroupName|String|classic-test|权限组名称

 |
|RequestId|String|55C5FFD6-BF99-41BD-9C66-FFF39189F4F8|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessGroup
&AccessGroupName=classic-test
&AccessGroupType=Classic
&Description=classic test access group
&<公共请求参数>…

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateAccessGroupResponse>
  <RequestId>55C5FFD6-BF99-41BD-9C66-FFF39189F4F8</RequestId>
  <AccessGroupName>classic-test</AccessGroupName>
</CreateAccessGroupResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"55C5FFD6-BF99-41BD-9C66-FFF39189F4F8",
	"AccessGroupName ":"classic-test"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

