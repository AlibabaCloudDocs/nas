# DeleteAccessGroup {#concept_62631_zh .concept}

DeleteAccessGroup用于删除已有权限组。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：DeleteAccessGroup|
|AccessGroupName|String|TRUE|权限组名称|

## 返回参数 { .section}

无

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteAccessGroup
    &AccessGroupName=classic-test
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <DeleteAccessGroupResponse>
          <RequestId>5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8</RequestId>
        </DeleteAccessGroupResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "9E15E394-38A6-457A-A62A-D9797C9A0262"
        }
        
        ```


