# DeleteMountTarget {#concept_62624_zh .concept}

DeleteMountTarget用于删除已有挂载点。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：DeleteMountTarget|
|FileSystemId|String|TRUE|文件系统 ID|
|MountTargetDomain|String|TRUE|挂载点域名|

## 返回参数 { .section}

无

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteMountTarget
    &FileSystemId=174494b666
    &MountTargetDomain=174494b666-xog95.cn-hangzhou.nas.aliyuncs.com
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <DeleteMountTargetResponse>
          <RequestId>5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8</RequestId>
        </DeleteMountTargetResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8"
        }
        
        ```


