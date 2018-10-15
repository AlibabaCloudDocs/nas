# DeleteAccessGroup {#concept_62631_zh .concept}

DeleteAccessGroup is used to delete existing permission groups.

## Request parameters { .section}

|Parameter name |Type |Required|Description|
|---------------|-----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: DeleteAccessGroup|
|AccessGroupName|String|TRUE|Permission group name|

## Response parameters { .section}

None

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteAccessGroup
    &AccessGroupName=classic-test
    &<Public Request Parameter>
    ...
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <DeleteAccessGroupResponse>
          <RequestId>5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8</RequestId>
        </DeleteAccessGroupResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "9E15E394-38A6-457A-A62A-D9797C9A0262"
        }
        
        ```


