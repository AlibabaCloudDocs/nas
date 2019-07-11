# DeleteAccessGroup {#concept_62631_zh .concept}

DeleteAccessGroup is used to delete existing permission groups.

## Debugging {#section_lj7_ia5_jot .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_usl_pgz_vpb .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|Action|String|No|DeleteAccessGroup|Operation interface name and system required parameter. Value: DeleteAccessGroup.|
|AccessGroupName|String|Yes|classic-test|Permission group name.|
|FileSystemType|String|No|standard|The type of the file system. Valid values: standard and extreme. Default value: standard.|

## Response parameters {#section_75x_034_oke .section}

|Parameter name|Type|Example|Description|
|--------------|----|-------|-----------|
|RequestId|String|9E15E394-38A6-457A-A62A-D9797C9A0262|The ID of the request.|

## Example {#section_zxj_75q_j5e .section}

-   Request example

    ``` {#codeblock_az4_46z_j5s .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteAccessGroup
    &AccessGroupName=classic-test
    &<Public Request Parameter>
    ...
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_9l6_jjx_blz .language-xml}
        <? xml version="1.0" encoding="UTF-8"? >
        <DeleteAccessGroupResponse>
          <RequestId>5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8</RequestId>
        </DeleteAccessGroupResponse>
        							
        ```

    -   JSON example

        ``` {#codeblock_an3_5xl_xiq .language-json}
        {
          "RequestId": "9E15E394-38A6-457A-A62A-D9797C9A0262"
        }
        							
        ```


## Error codes {#section_32t_r61_0up .section}

