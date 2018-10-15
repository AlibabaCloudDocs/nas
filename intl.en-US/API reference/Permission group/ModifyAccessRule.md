# ModifyAccessRule {#concept_62641_zh .concept}

ModifyAccessRule is used to modify permission rules.

## Request parameters { .section}

|Parameter name |Type |Required|Description|
|---------------|-----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: ModifyAccessRule|
|AccessGroupName|String|TRUE|Permission group name|
|AccessRuleId|String|TRUE|Rule serial number|
|SourceCidrIp|String|FALSE|Address or address segment|
|RWAccessType|String|FALSE|Read-write permission type|
|UserAccessType|String|FALSE|User permission type|
|Priority|Integer|FALSE|Priority level. Range: 1-100. Default value: 1|

## Response parameters { .section}

None

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAccessRule
    &AccessGroupName=classic-test
    &AccessRuleId=1
    &SourceCidrIp=192.168.0.1
    &RWAccessType=RDWR
    &UserAccessType=all_squash
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <ModifyAccessRuleResponse>
          <RequestId>6299428C-3861-435D-AE54-9B330A0007C8</RequestId>
        </ModifyAccessRuleResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "6299428C-3861-435D-AE54-9B330A0007C8",
        }
        
        ```


