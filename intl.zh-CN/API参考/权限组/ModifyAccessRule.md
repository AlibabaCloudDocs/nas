# ModifyAccessRule {#concept_62641_zh .concept}

ModifyAccessRule用于修改权限规则。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：ModifyAccessRule|
|AccessGroupName|String|TRUE|权限组名称|
|AccessRuleId|String|TRUE|规则序号|
|SourceCidrIp|String|FALSE|地址或地址段|
|RWAccessType|String|FALSE|读写权限类型|
|UserAccessType|String|FALSE|用户权限类型|
|Priority|Integer|FALSE|优先级，范围 1-100，默认值为 1|

## 返回参数 { .section}

无

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAccessRule
    &AccessGroupName=classic-test
    &AccessRuleId=1
    &SourceCidrIp=192.168.0.1
    &RWAccessType=RDWR
    &UserAccessType=all_squash
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <ModifyAccessRuleResponse>
          <RequestId>6299428C-3861-435D-AE54-9B330A0007C8</RequestId>
        </ModifyAccessRuleResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "6299428C-3861-435D-AE54-9B330A0007C8",
        }
        
        ```


