# DescribeAccessRules {#concept_62639_zh .concept}

DescribeAccessRules is used to return the permission group rule description.

## Debugging {#section_pt2_j04_hwf .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_j9a_1nx_v3b .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|AccessGroupName|String|Yes|classic-test|Permission group name.|
|AccessRuleId|String|No|1|Permission rule ID.|
|Action|String|No|DescribeAccessRules|Operation interface name and system required parameter. Value: DescribeAccessRules.|
|FileSystemType|String|No|standard| The type of the file system. Valid values: standard and extreme. Default value: standard.

 |
|PageNumber|Integer|No|1|The page number of the list \(beginning from 1\).|
|PageSize|Integer|No|1|The number of permission rules contained on each page. The default value is 10.|

## Response parameters {#section_fzv_e58_aum .section}

|Parameter name|Type|Example|Description|
|--------------|----|-------|-----------|
|AccessRules| | |Permission rule description.|
|AccessRuleId|String|1| Permission rule ID.

 |
|Priority|Integer|1|Priority level. Range: 1-100. Default value: 1.|
|RWAccess|String|RDWR| Read-write permission type: RDWR \(default value\) and RDONLY.

 |
|SourceCidrIp|String|10.0.0.1/32|Address or address segment.|
|UserAccess|String|no\_squash| User permission type: no\_squash \(default value\), root\_squash and all\_squash.

 |
|PageNumber|Integer|1|The page number of the list.|
|PageSize|Integer|1|The number of permission rules contained on each page.|
|RequestId|String|86D89E82-4297-4343-8E1E-A2495B35CC70|The ID of the request.|
|TotalCount|Integer|1|Total number of permission rules.|

## Example {#section_ii9_xrt_681 .section}

-   Request example

    ``` {#codeblock_2fl_ksi_jc8 .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeAccessRules
    &AccessGroupName=classic-test
    &<Public Request Parameter>
    …
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_swt_4y9_39o .language-xml}
        <? xml version="1.0" encoding="UTF-8"? >
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

    -   JSON example

        ``` {#codeblock_u15_ec0_ass .language-json}
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


## Error codes {#section_xxv_xax_k3y .section}

