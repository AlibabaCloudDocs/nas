# DescribeAccessRules {#concept_62639_zh .concept}

DescribeAccessRules is used to return the permission group rule description.

## Request parameters { .section}

|Parameter name |Type |Required|Description|
|---------------|-----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: DescribeAccessRules|
|AccessGroupName|String|TRUE|Permission group name|
|AccessRuleId|String|FALSE|Rule serial number|
|PageSize |Integer  |FALSE|The number of permission rules contained on each page. The default value is 10.|
|PageNumber|Integer|FALSE|The page number of the list \(beginning from 1\).|

## Response parameters { .section}

|Parameter name |Type|Description|
|---------------|----|-----------|
|TotalCount|Integer|Total number of permission rules|
|PageSize|Integer  |The number of permission rules contained on each page|
|PageNumber|Integer|The page number of the list|
|AccessRules|AccessRules|Permission rule description|

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeAccessRules
    &AccessGroupName=classic-test
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <DescribeAccessRulesResponse>
          <AccessRules>
            <AccessRule>
              <SourceCidrIp>10.0.0.1/32</SourceCidrIp>
              <AccessRuleId>1</AccessRuleId>
              <RWAccess>RDWR</RWAccess>
              <UserAccess>no_squash</UserAccess>
              <Priority>1</Priority>
            </AccessRule>
          </AccessRules>
          <PageNumber>1</PageNumber>
          <TotalCount>1</TotalCount>
          <PageSize>1</PageSize>
          <RequestId>86D89E82-4297-4343-8E1E-A2495B35CC70</RequestId>
        </DescribeAccessRulesResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "TotalCount": 1,
          "PageSize": 1,
          "RequestId": "86D89E82-4297-4343-8E1E-A2495B35CC70",
          "PageNumber": 1,
          "AccessRules": {
            "AccessRule": [
              {
                "RWAccess": "RDWR",
                "UserAccess": "no_squash",
                "Priority": 1,
                "SourceCidrIp": "10.0.0.1/32",
                "AccessRuleId": "1"
              }
            ]
          }
        }
        
        ```


