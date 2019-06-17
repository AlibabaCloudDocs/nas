# DescribeRegions {#concept_62608_zh .concept}

DescribeRegions用于返回所有 RegionId。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：DescribeRegions|
|AcceptLanguage|String|FALSE|默认值：无；中文：zh-CN；英文：en-US；日文：ja|
|PageSize|Integer|FALSE|每个分页包含的区域个数（默认 10）|
|PageNumber|Integer|FALSE|列表的分页页码（从 1 开始计数）|

## 返回参数 { .section}

|参数名称|类型|描述|
|----|--|--|
|RequestId|String|请求ID|
|TotalCount|Integer|返回区域信息的总个数|
|PageSize|Integer|每个分页包含的区域个数|
|PageNumber|Integer|列表的分页页码|
|Regions|RegionType|区域的描述信息|

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeRegions
    &PageSize=2
    &PageNumber=1
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <DescribeRegionsResponse>
          <PageNumber>1</PageNumber>
          <TotalCount>4</TotalCount>
          <PageSize>2</PageSize>
          <RequestId>A70BEE5D-76D3-49FB-B58F-1F398211A5C3</RequestId>
          <Regions>
            <Region>
              <RegionId>cn-hangzhou</RegionId>
              <RegionEndpoint>nas.cn-hangzhou.aliyuncs.com</RegionEndpoint>
        	  <LocalName>华东1</LocalName>
            </Region>
            <Region>
              <RegionId>cn-shanghai</RegionId>
        	  <RegionEndpoint>nas.cn-shanghai.aliyuncs.com</RegionEndpoint>
              <LocalName>华东2</LocalName>
            </Region>
          </Regions>
        </DescribeRegionsResponse>
        
        ```

    -   JSON示例

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
                "LocalName": "华东1"
              },
              {
                "RegionId": "cn-shanghai",
                "RegionEndpoint": "nas.cn-shanghai.aliyuncs.com",
        		"LocalName": "华东2"
              }
            ]
          }
        }
        
        ```


