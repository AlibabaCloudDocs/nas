# ModifyMountTarget {#concept_62628_zh .concept}

ModifyMountTarget is used to modify the mount point information.

## Request parameters { .section}

|Parameter name|Type|Required|Description|
|--------------|----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: ModifyMountTarget|
|FileSystemId|String|TRUE|File system ID|
|MountTargetDomain|String|TRUE|Mount point domain name|
|AccessGroupName|String|FALSE|Permission group name|
|Status|String|FALSE|Status, including Active and Inactive|

## Response parameters { .section}

None

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyMountTarget
    &FileSystemId=1ca404a666
    &MountTargetDomain=1ca404a666
    &Status=Inactive
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <ModifyMountTargetResponse>
          <RequestId>FF387D95-34C4-4879-B65A-99D1FA1B65CD</RequestId>
        </ModifyMountTargetResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "FF387D95-34C4-4879-B65A-99D1FA1B65CD"
        }
        
        ```


