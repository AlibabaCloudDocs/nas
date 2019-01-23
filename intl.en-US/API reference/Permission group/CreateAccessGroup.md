# CreateAccessGroup {#concept_62630_zh .concept}

CreateAccessGroup is used to create a permission group.

## Request parameters { .section}

|Parameter name|Type |Required|Description|
|--------------|-----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: CreateAccessGroup|
|AccessGroupName|String|TRUE|Permission group name|
|AccessGroupType|String|TRUE|Permission group type, including the Vpc and Classic types|
|Description|String|FALSE|Permission group description. It is the same as the permission group name by default.|

## Response parameters { .section}

|Parameter name |Type|Description|
|---------------|----|-----------|
|AccessGroupName|String|Permission group name|

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessGroup
    &AccessGroupName=classic-test
    &AccessGroupType=Classic
    &Description=classic test access group
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <CreateAccessGroupResponse>
          <RequestId>55C5FFD6-BF99-41BD-9C66-FFF39189F4F8</RequestId>
          <AccessGroupName>classic-test</AccessGroupName>
        </CreateAccessGroupResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "55C5FFD6-BF99-41BD-9C66-FFF39189F4F8",
          "AccessGroupName ": "classic-test"
        }
        
        ```


