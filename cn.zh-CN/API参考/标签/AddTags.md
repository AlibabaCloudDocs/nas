# AddTags {#doc_api_NAS_AddTags .reference}

添加或者覆盖一个或者多个标签到一个文件系统实例。

## 限制 {#description .section}

-   每个标签（Tag）由标签键（TagKey）和标签值（TagValue）组成。
-   标签键（TagKey）和标签值（TagValue）会自动去除头尾的占位符，如空格、\\t、\\n、\\r。
-   标签键（TagKey）不允许为空，标签值（TagValue）可为空。
-   标签键（TagKey）和标签值（TagValue）不区分大小写。
-   标签键（TagKey）最长为64个字符，标签值（TagValue）最长为128个字符。
-   每个实例最多绑定10个标签，对于相同标签键（TagKey）进行重复绑定的标签，则后绑定的标签将覆盖之前的标签。
-   如果一个标签所绑定的实例全都解绑，则该标签自动删除。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=AddTags&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AddTags|系统规定参数。取值：AddTags。

 |
|FileSystemId|String|是|0addcw13cd|文件系统ID。

 |
|Tag.N.Key|String|否|keyN|当前第N组标签键（TagKey）。需要绑定的标签，包括标签键（TagKey）和标签值（TagValue），单次最多支持传入10组值。标签键（TagKey）不能为空，标签值（TagValue）可以为空。

 |
|Tag.N.Value|String|否|valueN|当前第N组标签值（TagValue）。需要绑定的标签，包括标签键（TagKey）和标签值（TagValue），单次最多支持传入10组值。标签键（TagKey）不能为空，标签值（TagValue）可以为空。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|98696EF0-1607-4E9D-B01D-F20930B68845|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=AddTags
&FileSystemId=109c042666
&Tag.1.Key=test_key
&Tag.1.Value=test_value
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AddTagsResponse>
    <RequestId>98696EF0-1607-4E9D-B01D-F20930B68845</RequestId>
</AddTagsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"98696EF0-1607-4E9D-B01D-F20930B68845"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/NAS)查看更多错误码。

