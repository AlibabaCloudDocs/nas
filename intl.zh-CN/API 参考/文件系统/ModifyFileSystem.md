# ModifyFileSystem {#concept_62619_zh .concept}

ModifyFileSystem用于修改文件系统的信息。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：ModifyFileSystem|
|FileSystemId|String|TRUE|文件系统 ID|
|Description|String|FASLE|描述信息（不可用空格符）|

## 返回参数 { .section}

无

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyFileSystem
    &FileSystemId=1ca404a666
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <ModifyFileSystemResponse>
          <RequestId>5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8</RequestId>
        </ModifyFileSystemResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8"
        }
        
        ```


