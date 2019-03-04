# ModifyAccessGroup {#doc_api_1038895 .reference}

ModifyAccessGroup用于修改权限组。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=NAS&api=ModifyAccessGroup)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|是|classic-test|权限组名称

 |
|Action|String|是|ModifyAccessGroup|操作接口名，系统规定参数，取值：ModifyAccessGroup

 |
|Description|String|否|classic-test|权限组描述

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|ED2AE737-9D50-4CA4-B0DA-31BD610C2363|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GEThttps://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAccessGroup
&AccessGroupName=classic-test
&Description=classic-test
&<公共请求参数>…

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyAccessGroupResponse>
  <RequestId>ED2AE737-9D50-4CA4-B0DA-31BD610C2363</RequestId>
</ModifyAccessGroupResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"ED2AE737-9D50-4CA4-B0DA-31BD610C2363"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/NAS)

