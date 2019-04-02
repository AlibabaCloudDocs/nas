# CreateFileSystem {#concept_62611_zh .concept}

CreateFileSystem用于创建新的文件系统。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：CreateFileSystem|
|StorageType|String|TRUE|文件系统类别，目前包含 Performance（性能型）和Capacity（容量型）|
|ProtocolType|String|TRUE|使用的协议类型，目前包含 NFS和SMB|
|Description|String|FALSE|文件系统描述（不可用空格符）|

## 返回参数 { .section}

|参数名称|类型|描述|
|----|--|--|
|FileSystemId|String|创建成的文件系统 ID|

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateFileSystem
    &StorageType=Performance
    &ProtocolType=NFS
    &Description=balabala
    &<公共请求参数>
    …
    
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <CreateFileSystemResponse>
          <FileSystemId>1ca404a666</FileSystemId>
          <RequestId>98696EF0-1607-4E9D-B01D-F20930B68845</RequestId>
        </CreateFileSystemResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "98696EF0-1607-4E9D-B01D-F20930B68845",
          "FileSystemId": "1ca404a666"
        }
        
        ```


