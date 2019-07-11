# DescribeAccessGroups {#concept_62633_zh .concept}

DescribeAccessGroups is used to return the permission group description.

## Debugging {#section_w6s_rz7_ha8 .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_5fo_ekw_6t9 .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|Action|String|No|DescribeAccessGroups|Operation interface name and system required parameter. Value: DescribeAccessGroups.|
|AccessGroupName|String|No|classic-test|Permission group name.|
|FileSystemType|String|No|standard|The type of the file system. Valid values: standard and extreme. Default value: standard.|
|PageSize|Integer|No|2|The number of permission groups contained on each page. The default value is 10.|
|PageNumber|Integer|No|1|The page number of the list \(beginning from 1\).|

## Response parameters {#section_8oo_6qo_f5a .section}

|Parameter name|Type|example|Description|
|--------------|----|-------|-----------|
|AccessGroups| | |Permission group description.|
|AccessGroupName|String|classic-test|Permission group name.|
|AccessGroupType|String|Classic| The type of the Permission group. Valid values: Vpc and Classic.

 |
|Description|String|This is a classic test access group~|Permission group description.|
|MountTargetCount|Integer|0| The number of mount points to which this permission group applies.

 |
|RuleCount|Integer|0|The number of permission rules contained in this permission group.|
|PageNumber|Integer|1|The page number of the list.|
|PageSize|Integer|2|The number of permission groups contained on each page.|
|RequestId|String|2514F97E-FFF0-4A1F-BF04-729CEAC64B6F|The ID of the request.|
|TotalCount|Integer|2|Total number of permission groups.|

## Example {#section_5w0_r73_o86 .section}

-   Request example

    ``` {#codeblock_8k4_ztt_0yo .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeAccessGroups
    &<Public Request Parameter>
    …
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_v2s_tsb_i08 .language-xml}
        <? xml version="1.0" encoding="UTF-8"? >
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

    -   JSON example

        ``` {#codeblock_f9a_3r1_nx5 .language-json}
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
          "PageNumber": 1,
        }
        							
        ```


## Error codes {#section_ru8_1w0_6z0 .section}

For more information, see [Error codes](https://error-center.alibabacloud.com/status/product/NAS).

