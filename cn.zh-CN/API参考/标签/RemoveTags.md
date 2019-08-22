# RemoveTags {#doc_api_NAS_RemoveTags .reference}

从一个文件系统实例上解绑一个或多个标签。

## 说明 {#description .section}

删除的对象不存在时，也会返回成功。比如文件系统不存在，或标签键（TagKey）和标签值（TagValue）不存在时，都可以返回成功。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=RemoveTags&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RemoveTags|系统规定参数。取值：RemoveTags。

 |
|FileSystemId|String|是|0addcw13cd|文件系统ID。

 |
|Tag.N.Key|String|否|keyN|当前第N组标签键（TagKey）。需要解绑的标签，包括标签键（TagKey）和标签值（TagValue），单次最少传入1组值，最多传入10组值。标签键（TagKey）不能为空，标签值（TagValue）可以为空。

 |
|Tag.N.Value|String|否|valueN|当前第N组标签值（TagValue）。需要解绑的标签，包括标签键（TagKey）和标签值（TagValue），单次最多支持传入5组值。标签键（TagKey）不能为空，标签值（TagValue）可以为空。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|98696EF0-1607-4E9D-B01D-F20930B68845|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=RemoveTags
&FileSystemId=109c042666
&Tag.1.Key=test_key
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RemoveTagsResponse>
    <RequestId>98696EF0-1607-4E9D-B01D-F20930B68845</RequestId>
</RemoveTagsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"98696EF0-1607-4E9D-B01D-F20930B68845"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/NAS)查看更多错误码。

