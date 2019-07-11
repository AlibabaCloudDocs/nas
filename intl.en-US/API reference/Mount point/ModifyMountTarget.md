# ModifyMountTarget {#concept_62628_zh .concept}

ModifyMountTarget is used to modify the mount point information.

## Debugging {#section_a46_alx_xtx .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_pon_du7_bru .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|Action|String|No|ModifyMountTarget|Operation interface name and system required parameter. Value: ModifyMountTarget.|
|FileSystemId|String|Yes|1ca404a666|File system ID.|
|MountTargetDomain|String|Yes|1ca404a666-wxa89.cn-hangzhou.nas.aliyuncs.com|Mount point domain name.|
|AccessGroupName|String|No|classic-test|Permission group name.|
|Status|String|No|Inactive|The status of the mount point. Valid values: Active and Inactive.|

## Response parameters {#section_cct_y2t_w2h .section}

|Parameter name|Type|Example|Description|
|--------------|----|-------|-----------|
|RequestId|String|FF387D95-34C4-4879-B65A-99D1FA1B65CD|The ID of the request.|

## Example {#section_hn1_v56_l1d .section}

-   Request example

    ``` {#codeblock_fg0_plt_c0g .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyMountTarget
    &FileSystemId=1ca404a666
    &MountTargetDomain=1ca404a666
    &Status=Inactive
    &<Public Request Parameter>
    …
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_unr_lp0_ptz .language-xml}
        <? xml version="1.0" encoding="UTF-8"? >
        <ModifyMountTargetResponse>
          <RequestId>FF387D95-34C4-4879-B65A-99D1FA1B65CD</RequestId>
        </ModifyMountTargetResponse>
        							
        ```

    -   JSON example

        ``` {#codeblock_v5m_5k5_5xq .language-json}
        {
          "RequestId": "FF387D95-34C4-4879-B65A-99D1FA1B65CD"
        }
        							
        ```


## Error codes {#section_hog_x9q_m42 .section}

For more information, see [Error codes](https://error-center.alibabacloud.com/status/product/NAS).

