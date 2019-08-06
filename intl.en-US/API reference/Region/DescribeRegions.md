# DescribeRegions {#concept_62608_zh .concept}

DescribeRegions is used to return all region IDs.

## Debugging {#section_u0g_u38_mtr .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_43c_d8l_7ew .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRegions|Operation interface name and system required parameter. Value: DescribeRegions.|
|FileSystemType|String|No|standard|The type of the file system. Valid values: standard and extreme. Default value: standard.|
|PageSize|Integer|No|2|The number of regions contained on each page. The default value is 10.|
|PageNumber|Integer|No|1|The page number of the list \(beginning from 1\).|

## Response parameters {#section_66b_qnt_nm0 .section}

|Parameter name|Type|Example|Description|
|--------------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the list.|
|PageSize|Integer|2|The number of regions contained on each page.|
|Regions| | |Region description.|
|LocalName|String|China East 1| Region name.

 |
|RegionEndpoint|String|nas.cn-hangzhou.aliyuncs.com|The endpoint of the region.|
|RegionId|String|cn-hangzhou| Region ID.

 |
|RequestId|String|A70BEE5D-76D3-49FB-B58F-1F398211A5C3|The ID of the request.|
|TotalCount|Integer|4|The total number of returned region information items.|

## Example {#section_ggd_upv_ubh .section}

-   Request example

    ``` {#codeblock_60m_az4_sti .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeRegions
    &PageSize=2
    &PageNumber=1
    &<Public Request Parameter>
    …
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_cap_zqt_fzf .language-xml}
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

        ``` {#codeblock_cqv_etl_hky .language-json}
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


## Error codes {#section_t1m_ywf_r6y .section}

For more information, see [Error codes](https://error-center.alibabacloud.com/status/product/NAS).

