# CreateFileSystem {#concept_62611_zh .concept}

CreateFileSystem is used to create a new file system.

## Request parameters { .section}

|Parameter name |Type|Required|Description|
|---------------|----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: CreateFileSystem|
|StorageType|String|TRUE|The file system type. Currently includes the Performance type and the Capacity type|
|ProtocolType|String|TRUE|Type of protocol used. Currently includes the NFS type and the SMB type|
|Description|String|FALSE|File system description \(space characters are not allowed\)|

## Response parameters { .section}

|Parameter name |Type|Description|
|---------------|----|-----------|
|FileSystemId|String|ID of the file system created|

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateFileSystem
    &StorageType=Performance
    &ProtocolType=NFS
    &Description=balabala
    &<Public Request Parameter>
    …
    
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <CreateFileSystemResponse>
          <FileSystemId>1ca404a666</FileSystemId>
          <RequestId>98696EF0-1607-4E9D-B01D-F20930B68845</RequestId>
        </CreateFileSystemResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "98696EF0-1607-4E9D-B01D-F20930B68845",
          "FileSystemId": "1ca404a666"
        }
        
        ```


