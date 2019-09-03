# ModifyLDAPConfig {#doc_api_NAS_ModifyLDAPConfig .reference}

用于修改LDAP配置。

## 说明 {#description .section}

本接口只支持CPFS并行文件系统。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=ModifyLDAPConfig&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyLDAPConfig|系统规定参数。取值：ModifyLDAPConfig。

 |
|BindDN|String|是|cn=alibaba,dc=com|绑定LDAP的指定条目。

 |
|FileSystemId|String|是|109c042666|文件系统ID。

 |
|SearchBase|String|是|dc=example|LDAP搜索起始点。

 |
|URI|String|是|ldap://ldap.example.example|LDAP服务地址。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|5B4511A7-C99E-4071-AA8C-32E2529DA963|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyLDAPConfig
&FileSystemId=cpfs-xxx
&URI=[ldap://ldap.example.example](需做URLEncode)
&BindDN=[cn=alibaba,dc=com](需做URLEncode)
&SearchBase=[dc=example](需做URLEncode)
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyLDAPConfigResponse>
      <RequestId>5B4511A7-C99E-4071-AA8C-32E2529DA963</RequestId>
</ModifyLDAPConfigResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"5B4511A7-C99E-4071-AA8C-32E2529DA963"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/NAS)查看更多错误码。

