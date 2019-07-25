# ModifyAccessRule {#doc_api_NAS_ModifyAccessRule .reference}

ModifyAccessRule用于修改权限规则。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=ModifyAccessRule&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AccessGroupName|String|是|classic-test|权限组名称

 |
|AccessRuleId|String|是|1|规则 ID

 |
|Action|String|否|ModifyAccessRule|操作接口名，系统规定参数，取值：ModifyAccessRule

 |
|FileSystemType|String|否|standard|文件系统类型，可选值：standard、extreme，默认值：standard

 |
|Priority|Integer|否|1|优先级，范围 1-100，默认值为 1

 |
|RWAccessType|String|否|RDWR|读写权限类型

 |
|SourceCidrIp|String|否|192.168.0.1|地址或地址段（格式必须为单一IP地址或者CIDR网段格式，如：12.1.1.1 或 13.1.1.1/25）

 |
|UserAccessType|String|否|all\_squash|用户权限类型

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|6299428C-3861-435D-AE54-9B330A0007C8|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAccessRule
&AccessGroupName=classic-test
&AccessRuleId=1
&SourceCidrIp=192.168.0.1
&RWAccessType=RDWR
&UserAccessType=all_squash
&<公共请求参数>…

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyAccessRuleResponse>
    <RequestId>6299428C-3861-435D-AE54-9B330A0007C8</RequestId>
</ModifyAccessRuleResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"6299428C-3861-435D-AE54-9B330A0007C8"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

