# DescribeAccessGroups {#concept_62633_zh .concept}

DescribeAccessGroups is used to return the permission group description.

## Request parameters { .section}

|Parameter name|Type|Required|Description|
|--------------|----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: DescribeAccessGroups|
|AccessGroupName|String|FALSE|Permission group name|
|PageSize|Integer  |FALSE|The number of permission groups contained on each page. The default value is 10.|
|PageNumber|Integer|FALSE|The page number of the list \(beginning from 1\).|

## Response parameters { .section}

|Parameter name|Type|Description|
|--------------|----|-----------|
|TotalCount|Integer|Total number of permission groups|
|PageSize |Integer  |The number of permission groups contained on each page|
|PageNumber|Integer|The page number of the list|
|AccessGroups|String|Permission group description|

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeAccessGroups
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
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
          "PageNumber": 1,
        }
        
        ```


