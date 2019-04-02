# DescribeRegions {#concept_62608_zh .concept}

DescribeRegions is used to return all region IDs.

## Request parameters { .section}

|Parameter name|Type|Required|Description|
|--------------|----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: DescribeRegions|
|AcceptLanguage|String|FALSE|Default value: none. Chinese: zh-CN, English: en-US, Japanese: ja|
|PageSize|Integer|FALSE|The number of regions contained on each page. The default value is 10.|
|PageNumber|Integer|FALSE|The page number of the list \(beginning from 1\).|

## Response parameters { .section}

|Parameter name |Type|Description|
|---------------|----|-----------|
|RequestId|String|Request ID|
|TotalCount|Integer|The total number of returned region information items|
|PageSize |Integer  |The number of regions contained on each page|
|PageNumber|Integer|The page number of the list|
|Regions|RegionType|Region description|

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeRegions
    &PageSize=2
    &PageNumber=1
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <DescribeRegionsResponse>
          <PageNumber>1</PageNumber>
          <TotalCount>4</TotalCount>
          <PageSize>2</PageSize>
          <RequestId>A70BEE5D-76D3-49FB-B58F-1F398211A5C3</RequestId>
          <Regions>
            <Region>
              <RegionId>cn-hangzhou</RegionId>
              <RegionEndpoint>nas.cn-hangzhou.aliyuncs.com</RegionEndpoint>
        	  <LocalName>China East 1</LocalName>
            </Region>
            <Region>
              <RegionId>cn-shanghai</RegionId>
        	  <RegionEndpoint>nas.cn-shanghai.aliyuncs.com</RegionEndpoint>
              <LocalName>China East 2</LocalName>
            </Region>
          </Regions>
        </DescribeRegionsResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "TotalCount": 4,
          "PageSize": 2,
          "RequestId": "A70BEE5D-76D3-49FB-B58F-1F398211A5C3",
          "PageNumber": 1,
          "Regions": {
            "Region": [
              {
                "RegionId": "cn-hangzhou",
        		"RegionEndpoint": "nas.cn-hangzhou.aliyuncs.com",
                "LocalName": "China East 1"
              },
              {
                "RegionId": "cn-shanghai",
                "RegionEndpoint": "nas.cn-shanghai.aliyuncs.com",
        		"LocalName": "China East 2"
              }
            ]
          }
        }
        
        ```


