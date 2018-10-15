# ModifyAccessGroup {#concept_62634_zh .concept}

ModifyAccessGroup is used to modify the permission group.

## Request parameters { .section}

|Parameter name |Type |Required|Description|
|---------------|-----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: ModifyAccessGroup|
|AccessGroupName|String|TRUE|Permission group name|
|Description|String|FALSE|Permission group description|

## Response parameters { .section}

None

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAccessGroup
    &AccessGroupName=classic-test
    &Description=classic-test
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <ModifyAccessGroupResponse>
          <RequestId>ED2AE737-9D50-4CA4-B0DA-31BD610C2363</RequestId>
        </ModifyAccessGroupResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "ED2AE737-9D50-4CA4-B0DA-31BD610C2363"
        }
        
        ```


