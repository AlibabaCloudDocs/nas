# DeleteAccessRule {#concept_62638_zh .concept}

DeleteAccessRule用于删除已有权限规则。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：DeleteAccessRule|
|AccessGroupName|String|TRUE|权限组名称|
|AccessRuleId|String|TRUE|规则序号|

## 返回参数 { .section}

无

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessRule
    &AccessGroupName=classic-test
    &AccessRuleId=1
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <DeleteAccessRuleResponse>
          <RequestId>5B4511A7-C99E-4071-AA8C-32E2529DA963</RequestId>
        </DeleteAccessRuleResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "5B4511A7-C99E-4071-AA8C-32E2529DA963",
        }
        
        ```


