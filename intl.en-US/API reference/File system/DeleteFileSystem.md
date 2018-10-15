# DeleteFileSystem {#concept_62615_zh .concept}

DeleteFileSystem is used to delete existing file systems.

## Request parameters { .section}

|Parameter name|Type|Required|Description|
|--------------|----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: DeleteFileSystem|
|FileSystemId|String|TRUE|ID of the file system to be deleted|

## Response parameters { .section}

None

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteFileSystem
    &FileSystemId=1ca404a348
    &<Public Request Parameter>
    …
    
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <DeleteFileSystemResponse>
          <RequestId>9E15E394-38A6-457A-A62A-D9797C9A0262</RequestId>
        </DeleteFileSystemResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "9E15E394-38A6-457A-A62A-D9797C9A0262"
        }
        
        ```


