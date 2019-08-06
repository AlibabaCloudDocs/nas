# ModifyFileSystem {#concept_62619_zh .concept}

ModifyFileSystemis used to modify the file system information.

## Debugging {#section_o9s_no6_t98 .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_y47_fh3_29s .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|Action|String|Yes|ModifyFileSystem|Operation interface name and system required parameter. Value: ModifyFileSystem.|
|FileSystemId|String|Yes|1ca404a666|File system ID.|
|Description|String|No|None| The description of the file system. The description must be 2 to 128 characters in length. The description must start with a letter, but cannot start with http:// or https://. The description can contain letters, numbers, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |

## Response parameters {#section_c9j_lfu_tfs .section}

|Parameter name|Type|Example|Description|
|--------------|----|-------|-----------|
|RequestId|String|5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8|The ID of the request.|

## Example {#section_yk3_d0h_e7l .section}

-   Request example

    ``` {#codeblock_8bg_wq0_17q .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyFileSystem
    &FileSystemId=1ca404a666
    &<Public Request Parameter>
    ...
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_feb_snx_7gu .language-xml}
        <? xml version="1.0" encoding="UTF-8"? >
        <ModifyFileSystemResponse>
          <RequestId>5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8</RequestId>
        </ModifyFileSystemResponse>
        							
        ```

    -   JSON example

        ``` {#codeblock_79h_ift_5tn .language-json}
        {
          "RequestId": "5BC5CB97-9F28-42FE-84A4-0CD0DF4211C8"
        }
        							
        ```


## Error codes {#section_ng1_5nn_bs9 .section}

For more information, see [Error codes](https://error-center.alibabacloud.com/status/product/NAS).

