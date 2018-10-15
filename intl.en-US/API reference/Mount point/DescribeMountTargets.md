# DescribeMountTargets {#concept_62626_zh .concept}

DescribeMountTargets is used to return the mount point description.

## Request parameters { .section}

|Parameter name |Type |Required|Description|
|---------------|-----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: DescribeMountTargets|
|FileSystemId|String|TRUE|File system ID|
|MountTargetDomain|String|FALSE|Mount point domain name|
|PageSize |Integer  |FALSE|The number of mount points contained on each page. The default value is 10.|
|PageNumber|Integer|FALSE|The page number of the list \(beginning from 1\)|

## Response parameters { .section}

|Parameter name |Type|Description|
|---------------|----|-----------|
|TotalCount|Integer|Total number of mount points|
|PageSize |Integer  |The number of mount points contained on each page|
|PageNumber|Integer|The page number of the list|
|MountTargets|MountTargetType|Mount point description|

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeMountTargets
    &FileSystemId=1ca404a666
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <? xml version="1.0" encoding="UTF-8"? >
        <DescribeMountTargetsResponse>
          <PageNumber>1</PageNumber>
          <TotalCount>1</TotalCount>
          <PageSize>1</PageSize>
          <RequestId>3BAB90FD-B4A0-48DA-9F09-2B963510A0EF</RequestId>
          <MountTargets>
            <MountTarget>
              <Status>Active</Status>
              <NetworkType>Vpc</NetworkType>
              <VswId>vsw-2zevmwkwyztjuoffgdiwl</VswId>
              <VpcId>vpc-2zesj9afh3y518k9oe86q</VpcId>
              <MountTargetDomain>1ca404a666-wxa89.cn-hangzhou.nas.aliyuncs.com</MountTargetDomain>
              <AccessGroup>DEFAULT_VPC_GROUP_NAME</AccessGroup>
            </MountTarget>
          </MountTargets>
        </DescribeMountTargetsResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "TotalCount": 1,
          "PageSize": 1,
          "RequestId": "3BAB90FD-B4A0-48DA-9F09-2B963510A0EF",
          "PageNumber": 1,
          "MountTargets": {
            "MountTarget": [
              {
                "Status": "Active",
                "VswId": "vsw-2zevmwkwyztjuoffgdiwl",
                "VpcId": "vpc-2zesj9afh3y518k9oe86q",
                "MountTargetDomain": "1ca404a666-wxa89.cn-hangzhou.nas.aliyuncs.com",
                "NetworkType": "Vpc",
                "AccessGroup": "DEFAULT_VPC_GROUP_NAME"
              }
            ]
          }
        }
        
        ```


