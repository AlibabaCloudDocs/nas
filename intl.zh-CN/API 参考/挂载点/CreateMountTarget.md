# CreateMountTarget {#concept_62621_zh .concept}

CreateMountTarget用于创建挂载点。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：CreateMountTarget|
|FileSystemId|String|TRUE|文件系统 ID|
|AccessGroupName|String|TRUE|权限组名称|
|NetworkType|String|TRUE|网络类型，包括Vpc和Classic|
|VpcId|String|FALSE|VPC 网络 ID|
|VSwitchId|String|FALSE|交换机 ID|

## 返回参数 { .section}

|参数名称|类型|描述|
|----|--|--|
|MountTargetDomain|String|挂载点域名|

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateMountTarget
    &FileSystemId=174494b666
    &AccessGroupName=classic-test
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <CreateMountTargetResponse>
          <RequestId>70EACC9C-D07A-4A34-ADA4-77506C42B023</RequestId>
          <MountTargetDomain>174494b666-xog95.cn-hangzhou.nas.aliyuncs.com</MountTargetDomain>
        </CreateMountTargetResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "70EACC9C-D07A-4A34-ADA4-77506C42B023",
          "MountTargetDomain": "174494b666-xog95.cn-hangzhou.nas.aliyuncs.com"
        }
        
        ```


