# CreateMountTarget {#concept_62621_zh .concept}

CreateMountTarget is used to create a mount point.

## Debugging {#section_k5c_cer_co4 .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_eat_9u2_iew .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|Action|String|Yes|CreateMountTarget|Operation interface name and system required parameter. Value: CreateMountTarget.|
|FileSystemId|String|Yes|174494b666|File system ID.|
|AccessGroupName|String|Yes|classic-test|Permission group name.|
|NetworkType|String|Yes|vpc|Network type, including Vpc and Classic networks.|
|VpcId|String|No|vpc-2zesj9afh3y518k9oe86q|VPC network ID.|
|VSwitchId|String|No|vsw-2zevmwkwyztjuoffgdiwl|VSwitch ID.|

## Response parameters {#section_jt2_big_osz .section}

|Parameter name|Type|Example|Description|
|--------------|----|-------|-----------|
|MountTargetDomain|String|174494b666-xog95.cn-hangzhou.nas.aliyuncs.com|Mount point domain name.|
|RequestId|String|70EACC9C-D07A-4A34-ADA4-77506C42B023|The ID of the request.|

## Example {#section_ubw_3fj_cbh .section}

-   Request example

    ``` {#codeblock_czj_iqw_uwh .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateMountTarget
    &AccessGroupName=classic-test
    &FileSystemId=174494b666
    &<Public Request Parameter>
    …
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_o9w_7rs_kvo .language-xml}
        <? xml version="1.0" encoding="UTF-8"? >
        <CreateMountTargetResponse>
          <RequestId>70EACC9C-D07A-4A34-ADA4-77506C42B023</RequestId>
          <MountTargetDomain>174494b666-xog95.cn-hangzhou.nas.aliyuncs.com</MountTargetDomain>
        </CreateMountTargetResponse>
        							
        ```

    -   JSON example

        ``` {#codeblock_6dc_gp8_e30 .language-json}
        {
          "RequestId": "70EACC9C-D07A-4A34-ADA4-77506C42B023",
          "MountTargetDomain": "174494b666-xog95.cn-hangzhou.nas.aliyuncs.com"
        }
        							
        ```


## Error codes {#section_pcw_1tt_o6v .section}

For more information, see [Error codes](https://error-center.alibabacloud.com/status/product/NAS).

