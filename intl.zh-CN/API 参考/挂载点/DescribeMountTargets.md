# DescribeMountTargets {#concept_62626_zh .concept}

DescribeMountTargets用于返回挂载点描述信息。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：DescribeMountTargets|
|FileSystemId|String|TRUE|文件系统 ID|
|MountTargetDomain|String|FALSE|挂载点域名|
|PageSize|Integer|FALSE|每个分页包含的挂载点个数（默认 10）|
|PageNumber|Integer|FALSE|列表的分页页码（从1开始计数）|

## 返回参数 { .section}

|参数名称|类型|描述|
|----|--|--|
|TotalCount|Integer|挂载点的总个数|
|PageSize|Integer|每个分页包含的挂载点个数|
|PageNumber|Integer|列表的分页页码|
|MountTargets|MountTargetType|挂载点描述信息|

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeMountTargets
    &FileSystemId=1ca404a666
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <?xml version="1.0" encoding="UTF-8"?>
        <DescribeMountTargetsResponse>
          <PageNumber>1</PageNumber>
          <TotalCount>1</TotalCount>
          <PageSize>1</PageSize>
          <RequestId>3BAB90FD-B4A0-48DA-9F09-2B963510A0EF</RequestId>
          <MountTargets>
            <MountTarget>
              <Status>Active</Status>
              <NetworkType>Vpc</NetworkType>
              <VswId>vsw-2zevmwkwyztjuoffgdiwl</VswId>
              <VpcId>vpc-2zesj9afh3y518k9oe86q</VpcId>
              <MountTargetDomain>1ca404a666-wxa89.cn-hangzhou.nas.aliyuncs.com</MountTargetDomain>
              <AccessGroup>DEFAULT_VPC_GROUP_NAME</AccessGroup>
            </MountTarget>
          </MountTargets>
        </DescribeMountTargetsResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "TotalCount": 1,
          "PageSize": 1,
          "RequestId": "3BAB90FD-B4A0-48DA-9F09-2B963510A0EF",
          "PageNumber": 1,
          "MountTargets": {
            "MountTarget": [
              {
                "Status": "Active",
                "VswId": "vsw-2zevmwkwyztjuoffgdiwl",
                "VpcId": "vpc-2zesj9afh3y518k9oe86q",
                "MountTargetDomain": "1ca404a666-wxa89.cn-hangzhou.nas.aliyuncs.com",
                "NetworkType": "Vpc",
                "AccessGroup": "DEFAULT_VPC_GROUP_NAME"
              }
            ]
          }
        }
        
        ```


