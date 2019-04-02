# DescribeAccessGroups {#concept_62633_zh .concept}

DescribeAccessGroups用于返回权限组描述信息。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：DescribeAccessGroups|
|AccessGroupName|String|FALSE|权限组名称|
|PageSize|Integer|FALSE|每个分页包含的权限组个数（默认10）|
|PageNumber|Integer|FALSE|列表的分页页码（从1开始计数）|

## 返回参数 { .section}

|参数名称|类型|描述|
|----|--|--|
|TotalCount|Integer|权限组的总个数|
|PageSize|Integer|每个分页包含的权限组个数|
|PageNumber|Integer|列表的分页页码|
|AccessGroups|String|权限组描述信息|

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeAccessGroups
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <DescribeAccessGroupsResponse>
          <PageNumber>1</PageNumber>
          <TotalCount>2</TotalCount>
          <PageSize>2</PageSize>
          <RequestId>3E569F4A-F743-490B-AC01-A8088F5C17A1</RequestId>
          <AccessGroups>
            <AccessGroup>
              <Description>DEFAULT ACCESS GROUP NAME</Description>
              <RuleCount>1</RuleCount>
              <AccessGroupType>Vpc</AccessGroupType>
              <AccessGroupName>DEFAULT_VPC_GROUP_NAME</AccessGroupName>
              <MountTargetCount>8</MountTargetCount>
            </AccessGroup>
            <AccessGroup>
              <Description>This is a classic test access group~</Description>
              <RuleCount>0</RuleCount>
              <AccessGroupType>Classic</AccessGroupType>
              <AccessGroupName>classic-test</AccessGroupName>
              <MountTargetCount>0</MountTargetCount>
            </AccessGroup>
          </AccessGroups>
        </DescribeAccessGroupsResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "AccessGroups": {
            "AccessGroup": [
              {
                "RuleCount": 1,
                "AccessGroupType": "Vpc",
                "Description": "DEFAULT ACCESS GROUP NAME",
                "AccessGroupName": "DEFAULT_VPC_GROUP_NAME",
                "MountTargetCount": 8
              },
              {
                "RuleCount": 0,
                "AccessGroupType": "Classic",
                "Description": "This is a classic test access group~",
                "AccessGroupName": "classic-test",
                "MountTargetCount": 0
              }
            ]
          },
          "TotalCount": 2,
          "PageSize": 2,
          "RequestId": "2514F97E-FFF0-4A1F-BF04-729CEAC64B6F",
          "PageNumber": 1
        }
        
        ```


