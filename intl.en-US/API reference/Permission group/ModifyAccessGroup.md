# ModifyAccessGroup {#concept_62634_zh .concept}

ModifyAccessGroup is used to modify the permission group.

## Debugging {#section_3d5_xqm_ghz .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_io3_yz1_8eq .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|Action|String|No|ModifyAccessGroup|Operation interface name and system required parameter. Value: ModifyAccessGroup.|
|AccessGroupName|String|Yes|classic-test|Permission group name.|
|Description|String|No|classic-test| The description of the permission group. By default, the description of the permission group is the same as the name of the permission group. The description must be 2 to 128 characters in length. The description must start with a letter and cannot start with http:// or https://. The description can contain letters, numbers, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |
|FileSystemType|String|No|standard|The type of the file system. Valid values: standard and extreme. Default value: standard.|

## Response parameters {#section_xbh_8iw_r9q .section}

|Parameter name|Type|Example|Description|
|--------------|----|-------|-----------|
|RequestId|String|ED2AE737-9D50-4CA4-B0DA-31BD610C2363|The ID of the request.|

## Example {#section_b7t_vgb_r8a .section}

-   Request example

    ``` {#codeblock_n7q_1or_mq5 .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAccessGroup
    &AccessGroupName=classic-test
    &Description=classic-test
    &<Public Request Parameter>
    …
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_7k1_l2i_l66 .language-xml}
        <? xml version="1.0" encoding="UTF-8"? >
        <ModifyAccessGroupResponse>
          <RequestId>ED2AE737-9D50-4CA4-B0DA-31BD610C2363</RequestId>
        </ModifyAccessGroupResponse>
        							
        ```

    -   JSON example

        ``` {#codeblock_ydp_8qi_0fl .language-json}
        {
          "RequestId": "ED2AE737-9D50-4CA4-B0DA-31BD610C2363"
        }
        							
        ```


## Error codes {#section_elg_a4c_bhp .section}

