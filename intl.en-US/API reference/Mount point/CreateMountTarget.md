# CreateMountTarget {#concept_62621_zh .concept}

CreateMountTarget is used to create a mount point.

## Request parameters { .section}

|Parameter name|Type|Required|Description|
|--------------|----|--------|-----------|
|Action|String|TRUE|Operation interface name and system required parameter. Value: CreateMountTarget|
|FileSystemId|String|TRUE|File system ID|
|AccessGroupName|String|TRUE|Permission group name|
|NetworkType|String|TRUE|Network type, including Vpc and Classic networks.|
|VpcId|String|FALSE|VPC network ID|
|VSwitchId|String|FALSE|VSwitch ID.|

## Response parameters { .section}

|Parameter name|Type|Description|
|--------------|----|-----------|
|MountTargetDomain|String|Mount point domain name|

## Example { .section}

-   Request example

    ```language-shell
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateMountTarget
    &FileSystemId=174494b666
    &AccessGroupName=classic-test
    &<Public Request Parameter>
    …
    
    ```

-   Response example
    -   XML example

        ```language-xml
        <? xml version="1.0" encoding="UTF-8"? >
        <CreateMountTargetResponse>
          <RequestId>70EACC9C-D07A-4A34-ADA4-77506C42B023</RequestId>
          <MountTargetDomain>174494b666-xog95.cn-hangzhou.nas.aliyuncs.com</MountTargetDomain>
        </CreateMountTargetResponse>
        
        ```

    -   JSON example

        ```language-json
        {
          "RequestId": "70EACC9C-D07A-4A34-ADA4-77506C42B023",
          "MountTargetDomain": "174494b666-xog95.cn-hangzhou.nas.aliyuncs.com"
        }
        
        ```


