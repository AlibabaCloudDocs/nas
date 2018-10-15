# DeleteMountTarget {#concept_62624_zh .concept}

DeleteMountTarget is used to delete existing mount points.

## Request parameters { .section}

|Parameter name|Type|Required| Description|
|--------------|----|--------|------------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: DeleteMountTarget|
|FileSystemId|String|TRUE|File system ID|
|MountTargetDomain|String|TRUE|Mount point domain name|

## Response parameters { .section}

None

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteMountTarget
    &FileSystemId=174494b666
    &MountTargetDomain=174494b666-xog95.cn-hangzhou.nas.aliyuncs.com
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <DeleteMountTargetResponse>
          <RequestId>5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8</RequestId>
        </DeleteMountTargetResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8"
        }
        
        ```


