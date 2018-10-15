# CreateAccessRule {#concept_62636_zh .concept}

CreateAccessRule is used to create a permission rule.

## Request parameters { .section}

|Parameter name|Type |Required|Description|
|--------------|-----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: CreateAccessRule|
|AccessGroupName|String|TRUE|Permission group name|
|SourceCidrIp|String|TRUE|Address or address segment|
|RWAccessType|String|FALSE|Read-write permission type: RDWR \(default\), RDONLY|
|UserAccessType|String|FALSE|User permission type: no\_squash \(default\), root\_squash, all\_squash|
|Priority|Integer|FALSE|Priority level. Range: 1-100. Default value: 1|

## Response parameters { .section}

|Parameter name |Type|Description|
|---------------|----|-----------|
|AccessRuleId|String|Rule serial number|

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessRule
    &AccessGroupName=classic-test
    &SourceCidrIp=10.0.0.1/32
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <CreateAccessRuleResponse>
          <AccessRuleId>1</AccessRuleId>
          <RequestId>A323836B-5BC6-45A6-8048-60675C23EE2A</RequestId>
        </CreateAccessRuleResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "A323836B-5BC6-45A6-8048-60675C23EE2A",
          "AccessRuleId": "1"
        }
        
        ```


