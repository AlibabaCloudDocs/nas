# CreateAccessGroup {#doc_api_NAS_CreateAccessGroup .reference}

CreateAccessGroup用于创建权限组。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=CreateAccessGroup&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|是|classic-test|权限组名称，长度为3-64个字符，必须以大小字母开头，可以包含英文字母、数字、下划线（\_）或者连字符（-）。

 系统预置两个内建权限组："DEFAULT\_VPC\_GROUP\_NAME"和 "DEFAULT\_CLASSIC\_GROUP\_NAME"，命名不能与两个内建权限组冲突。

 |
|AccessGroupType|String|是|Classic|权限组类型，包括 Vpc和 Classic

 |
|Action|String|否|CreateAccessGroup|操作接口名，系统规定参数，取值：CreateAccessGroup

 |
|Description|String|否|classictestaccessgroup|权限组描述，默认和名称相同，长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）

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

