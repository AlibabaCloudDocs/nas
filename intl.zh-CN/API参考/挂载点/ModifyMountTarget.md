# ModifyMountTarget {#concept_62628_zh .concept}

ModifyMountTarget用于修改挂载点信息。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：ModifyMountTarget|
|FileSystemId|String|TRUE|文件系统 ID|
|MountTargetDomain|String|TRUE|挂载点域名|
|AccessGroupName|String|FALSE|权限组名称|
|Status|String|FALSE|状态，包括 Active 和 Inactive|

## 返回参数 { .section}

无

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyMountTarget
    &FileSystemId=1ca404a666
    &MountTargetDomain=1ca404a666
    &Status=Inactive
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <ModifyMountTargetResponse>
          <RequestId>FF387D95-34C4-4879-B65A-99D1FA1B65CD</RequestId>
        </ModifyMountTargetResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "FF387D95-34C4-4879-B65A-99D1FA1B65CD"
        }
        
        ```


