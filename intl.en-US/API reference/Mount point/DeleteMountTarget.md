# DeleteMountTarget {#concept_62624_zh .concept}

DeleteMountTarget is used to delete existing mount points.

## Debugging {#section_gil_vhf_754 .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_yi1_9xx_mzu .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|FileSystemId|String|Yes|174494b666| File system ID.

 |
|MountTargetDomain|String|Yes|174494b666-xog95.cn-hangzhou.nas.aliyuncs.com|Mount point domain name.|
|Action|String|No|DeleteMountTarget| Operation interface name and system required parameter. Value: DeleteMountTarget.

 |

## Response parameters {#section_lt8_sdj_82c .section}

|Parameter name|Type|Example|Description|
|--------------|----|-------|-----------|
|RequestId|String|5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8|The ID of the request.|

## Example {#section_iex_dth_hew .section}

-   Request example

    ``` {#codeblock_vbb_z0y_1ji .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteMountTarget
    &FileSystemId=174494b666
    &MountTargetDomain=174494b666-xog95.cn-hangzhou.nas.aliyuncs.com
    &<Public Request Parameter>
    …
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_irm_mll_3nd .language-xml}
        <? xml version="1.0" encoding="UTF-8"? >
        <DeleteMountTargetResponse>
          <RequestId>5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8</RequestId>
        </DeleteMountTargetResponse>
        							
        ```

    -   JSON example

        ``` {#codeblock_h84_936_kss .language-json}
        {
          "RequestId": "5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8"
        }
        							
        ```


## Error codes {#section_oxv_anu_tu0 .section}

