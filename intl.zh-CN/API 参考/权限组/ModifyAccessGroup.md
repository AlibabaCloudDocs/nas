# ModifyAccessGroup {#concept_62634_zh .concept}

ModifyAccessGroup用于修改权限组。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：ModifyAccessGroup|
|AccessGroupName|String|TRUE|权限组名称|
|Description|String|FALSE|权限组描述|

## 返回参数 { .section}

无

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAccessGroup
    &AccessGroupName=classic-test
    &Description=classic-test
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <ModifyAccessGroupResponse>
          <RequestId>ED2AE737-9D50-4CA4-B0DA-31BD610C2363</RequestId>
        </ModifyAccessGroupResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "ED2AE737-9D50-4CA4-B0DA-31BD610C2363"
        }
        
        ```


