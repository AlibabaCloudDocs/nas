# DescribeFileSystems {#concept_62617_zh .concept}

DescribeFileSystems is used to return the description of a file system.

## Request parameters { .section}

|Parameter name |Type|Required|Description|
|---------------|----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: DescribeFileSystems|
|FileSystemId|String|FALSE|File system ID|
|PageSize |Integer  |FALSE|The number of file systems contained on each page. The default value is 10.|
|PageNumber|Integer|FALSE|The page number of the list \(beginning from 1\)|

## Response parameters { .section}

|Parameter name |Type|Description|
|---------------|----|-----------|
|TotalCount|Integer|Total number of file systems|
|PageSize |Integer  |The number of file systems contained on each page|
|PageNumber|Integer|The page number of the list|
|FileSystems|FileSystemType|File system description|

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeFileSystems
    &FileSystemId=109c042666
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
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

    -   JSON example

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


