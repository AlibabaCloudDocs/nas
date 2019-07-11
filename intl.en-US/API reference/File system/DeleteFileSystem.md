# DeleteFileSystem {#concept_62615_zh .concept}

DeleteFileSystem is used to delete existing file systems.

## Debugging {#section_gun_vul_wbx .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_vnn_f4v_cth .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|FileSystemId|String|Yes|1ca404a348|The file system ID to be deleted.|
|Action|String|No|DeleteFileSystem| Operation interface name and system required parameter. Value: DeleteFileSystem.

 |

## Response parameters {#section_57p_tk2_ffu .section}

|Parameter name|Type|Example|Description|
|--------------|----|-------|-----------|
|RequestId|String|9E15E394-38A6-457A-A62A-D9797C9A0262|The ID of the request.|

## Example {#section_3q5_h5l_py8 .section}

-   Request example

    ``` {#codeblock_8s4_yrn_eaa .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DeleteFileSystem
    &FileSystemId=1ca404a348
    &<Public Request Parameter>
    …
    
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_n45_3f7_0fq .language-xml}
        <? xml version="1.0" encoding="UTF-8"? >
        <DeleteFileSystemResponse>
          <RequestId>9E15E394-38A6-457A-A62A-D9797C9A0262</RequestId>
        </DeleteFileSystemResponse>
        							
        ```

    -   JSON example

        ``` {#codeblock_xr4_d92_vvs .language-json}
        {
          "RequestId": "9E15E394-38A6-457A-A62A-D9797C9A0262"
        }
        							
        ```


## Error codes {#section_ayv_9vp_ben .section}

For more information, see [Error codes](https://error-center.alibabacloud.com/status/product/NAS).

