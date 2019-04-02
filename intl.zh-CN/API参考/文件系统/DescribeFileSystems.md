# DescribeFileSystems {#concept_62617_zh .concept}

DescribeFileSystems用于返回文件系统的描述信息。

## 请求参数 { .section}

|参数名称|类型|必选|描述|
|----|--|--|--|
|Action|String|TRUE|操作接口名，系统规定参数，取值：DescribeFileSystems|
|FileSystemId|String|FALSE|文件系统 ID|
|PageSize|Integer|FALSE|每个分页包含的文件系统个数（默认为 10）|
|PageNumber|Integer|FALSE|列表的分页页码（从 1 开始计数）|

## 返回参数 { .section}

|参数名称|类型|描述|
|----|--|--|
|TotalCount|Integer|文件系统的总个数|
|PageSize|Integer|每个分页包含的文件系统个数|
|PageNumber|Integer|列表的分页页码|
|FileSystems|FileSystemType|文件系统描述信息|

## 示例 { .section}

-   请求示例

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeFileSystems
    &FileSystemId=109c042666
    &<公共请求参数>
    …
    
    ```

-   返回示例
    -   XML示例

        ```language-xml
        <?xml version="1.0" encoding="UTF-8"?>
        <DescribeFileSystemsResponse>
          <PageNumber>1</PageNumber>
          <TotalCount>1</TotalCount>
          <PageSize>1</PageSize>
          <RequestId>035B3A3A-E514-4B41-B906-5D906CFBD65F</RequestId>
          <FileSystems>
            <FileSystem>
              <FileSystemId>109c042666</FileSystemId>
              <ProtocolType>NFS</ProtocolType>
              <RegionId>cn-hangzhou</RegionId>
              <CreateTime>2017-05-27T15:43:06CST</CreateTime>
              <Destription/>
              <MountTargets>
                <MountTarget>
                  <MountTargetDomain>109c042666-wjb85.cn-hangzhou.nas.aliyuncs.com</MountTargetDomain>
                </MountTarget>
              </MountTargets>
              <StorageType>Performance</StorageType>
              <MeteredSize>1611661312</MeteredSize>
            </FileSystem>
          </FileSystems>
        </DescribeFileSystemsResponse>
        
        ```

    -   JSON示例

        ```language-json
        {
          "FileSystems": {
            "FileSystem": [
              {
                "StorageType": "Performance",
                "ProtocolType": "NFS",
                "CreateTime": "2017-05-27T15:43:06CST",
                "Destription": "",
                "MountTargets": {
                  "MountTarget": [
                    {
                      "MountTargetDomain": "109c042666-wjb85.cn-hangzhou.nas.aliyuncs.com"
                    }
                  ]
                },
                "FileSystemId": "109c042666",
                "RegionId": "cn-hangzhou",
                "MeteredSize": 1611661312
              }
            ]
          },
          "TotalCount": 1,
          "PageSize": 1,
          "RequestId": "035B3A3A-E514-4B41-B906-5D906CFBD65F",
          "PageNumber": 1
        }
        
        
        ```


