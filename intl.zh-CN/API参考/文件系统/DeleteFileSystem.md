# DeleteFileSystem {#concept_62615_zh .concept}

DeleteFileSystem用于删除已有的文件系统。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：DeleteFileSystem|
|FileSystemId|String|TRUE|要删除的文件系统 ID|

## 返回参数 { .section}

无

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteFileSystem
    &FileSystemId=1ca404a348
    &<公共请求参数>
    …
    
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <DeleteFileSystemResponse>
          <RequestId>9E15E394-38A6-457A-A62A-D9797C9A0262</RequestId>
        </DeleteFileSystemResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "9E15E394-38A6-457A-A62A-D9797C9A0262"
        }
        
        ```


