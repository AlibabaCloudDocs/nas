# CreateAccessGroup {#concept_62630_zh .concept}

CreateAccessGroup用于创建权限组。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：CreateAccessGroup|
|AccessGroupName|String|TRUE|权限组名称|
|AccessGroupType|String|TRUE|权限组类型，包括 VPC和 Classic|
|Description|String|FALSE|权限组描述，默认和名称相同|

## 返回参数 { .section}

|参数名称|类型|描述|
|----|--|--|
|AccessGroupName|String|权限组名称|

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessGroup
    &AccessGroupName=classic-test
    &AccessGroupType=Classic
    &Description=classic test access group
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <CreateAccessGroupResponse>
          <RequestId>55C5FFD6-BF99-41BD-9C66-FFF39189F4F8</RequestId>
          <AccessGroupName>classic-test</AccessGroupName>
        </CreateAccessGroupResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "RequestId": "55C5FFD6-BF99-41BD-9C66-FFF39189F4F8",
          "AccessGroupName ": "classic-test"
        }
        
        ```


