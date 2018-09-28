# DescribeAccessRules {#concept_62639_zh .concept}

DescribeAccessRules用于返回权限规则描述。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：DescribeAccessRules|
|AccessGroupName|String|TRUE|权限组名称|
|AccessRuleId|String|FALSE|规则序号|
|PageSize|Integer|FALSE|每个分页包含的权限规则个数（默认 10）|
|PageNumber|Integer|FALSE|列表的分页页码（从 1 开始计数）|

## 返回参数 { .section}

|参数名称|类型|描述|
|----|--|--|
|TotalCount|Integer|权限规则的总个数|
|PageSize|Integer|每个分页包含的权限规则个数|
|PageNumber|Integer|列表的分页页码|
|AccessRules|AccessRules|权限规则描述信息|

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeAccessRules
    &AccessGroupName=classic-test
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <DescribeAccessRulesResponse>
          <AccessRules>
            <AccessRule>
              <SourceCidrIp>10.0.0.1/32</SourceCidrIp>
              <AccessRuleId>1</AccessRuleId>
              <RWAccess>RDWR</RWAccess>
              <UserAccess>no_squash</UserAccess>
              <Priority>1</Priority>
            </AccessRule>
          </AccessRules>
          <PageNumber>1</PageNumber>
          <TotalCount>1</TotalCount>
          <PageSize>1</PageSize>
          <RequestId>86D89E82-4297-4343-8E1E-A2495B35CC70</RequestId>
        </DescribeAccessRulesResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "TotalCount": 1,
          "PageSize": 1,
          "RequestId": "86D89E82-4297-4343-8E1E-A2495B35CC70",
          "PageNumber": 1,
          "AccessRules": {
            "AccessRule": [
              {
                "RWAccess": "RDWR",
                "UserAccess": "no_squash",
                "Priority": 1,
                "SourceCidrIp": "10.0.0.1/32",
                "AccessRuleId": "1"
              }
            ]
          }
        }
        
        ```


