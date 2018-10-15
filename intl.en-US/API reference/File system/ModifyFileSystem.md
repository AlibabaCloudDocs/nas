# ModifyFileSystem {#concept_62619_zh .concept}

ModifyFileSystemis used to modify the file system information.

## Request parameters { .section}

|Parameter name |Type|Required|Description|
|---------------|----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: ModifyFileSystem|
|FileSystemId|String|TRUE|File system ID|
|Description|String|FASLE|Description \(space characters are not allowed\).|

## Response parameters { .section}

None

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyFileSystem
    &FileSystemId=1ca404a666
    &<Public Request Parameter>
    ...
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <ModifyFileSystemResponse>
          <RequestId>5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8</RequestId>
        </ModifyFileSystemResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8"
        }
        
        ```


