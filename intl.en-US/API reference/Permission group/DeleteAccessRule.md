# DeleteAccessRule {#concept_62638_zh .concept}

DeleteAccessRule is used to delete existing permission rules.

## Request parameters { .section}

|Parameter name|Type|Required|Description|
|--------------|----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: DeleteAccessRule|
|AccessGroupName|String|TRUE|Permission group name|
|AccessRuleId|String|TRUE|Rule serial number|

## Response parameters { .section}

None

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessRule
    &AccessGroupName=classic-test
    &AccessRuleId=1
    &<Public Request Parameter>
    ...
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <DeleteAccessRuleResponse>
          <RequestId>5B4511A7-C99E-4071-AA8C-32E2529DA963</RequestId>
        </DeleteAccessRuleResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "5B4511A7-C99E-4071-AA8C-32E2529DA963",
        }
        
        ```


