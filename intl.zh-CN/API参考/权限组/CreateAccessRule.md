# CreateAccessRule {#concept_62636_zh .concept}

CreateAccessRule用于创建权限规则。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：CreateAccessRule|
|AccessGroupName|String|TRUE|权限组名称|
|SourceCidrIp|String|TRUE|地址或地址段|
|RWAccessType|String|FALSE|读写权限类型：RDWR（默认）和 RDONLY|
|UserAccessType|String|FALSE|用户权限类型：no\_squash（默认）、root\_squash和all\_squash|
|Priority|Integer|FALSE|优先级，范围 1-100，默认值为1|

## 返回参数 { .section}

|参数名称|类型|描述|
|----|--|--|
|AccessRuleId|String|规则序号|

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessRule
    &AccessGroupName=classic-test
    &SourceCidrIp=10.0.0.1/32
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <CreateAccessRuleResponse>
          <AccessRuleId>1</AccessRuleId>
          <RequestId>A323836B-5BC6-45A6-8048-60675C23EE2A</RequestId>
        </CreateAccessRuleResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "A323836B-5BC6-45A6-8048-60675C23EE2A",
          "AccessRuleId": "1"
        }
        
        ```


