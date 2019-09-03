# RemoveClientFromBlackList {#doc_api_NAS_RemoveClientFromBlackList .reference}

从CPFS服务中，将客户端移出黑名单，恢复其写入请求。

## 说明 {#description .section}

本接口只支持CPFS并行文件系统。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=RemoveClientFromBlackList&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RemoveClientFromBlackList|系统规定参数。取值：RemoveClientFromBlackList。

 |
|ClientIP|String|是|192.168.0.0|待移出黑名单的客户端IP地址。

 |
|ClientToken|String|是|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。ClientToken只支持ASCII字符，且不能超过64个字符。

 更多详情，请参见[如何保证幂等性](https://help.aliyun.com/document_detail/25693.html)。

 |
|FileSystemId|String|是|1ca404a348|文件系统ID。

 |
|RegionId|String|是|cn-hangzhou|文件系统所属的地域ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|A70BEE5D-76D3-49FB-B58F-1F398211A5C3|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=RemoveClientFromBlackList
&FileSystemId=cpfs-xxx
&ClientIP=192.168.0.1
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<EvictClientResponse>
    <RequestId>A70BEE5D-76D3-49FB-B58F-1F398211A5C3</RequestId>
</EvictClientResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"A70BEE5D-76D3-49FB-B58F-1F398211A5C3"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/NAS)查看更多错误码。

