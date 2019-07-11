# DeleteAccessRule {#concept_62638_zh .concept}

DeleteAccessRule is used to delete existing permission rules.

## Debugging {#section_bvk_9xp_xye .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_srd_4mz_bgh .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|AccessGroupName|String|Yes|classic-test|Permission group name.|
|AccessRuleId|String|Yes|1|Permission Rule ID.|
|Action|String|No|DeleteAccessRule| Operation interface name and system required parameter. Value: DeleteAccessRule.

 |
|FileSystemType|String|No|standard| The type of the file system. Valid values: standard and extreme. Default value: standard.

 |

## Response parameters {#section_6ve_2dz_e9j .section}

|Parameter name|Type|Example|Description|
|--------------|----|-------|-----------|
|RequestId|String|5B4511A7-C99E-4071-AA8C-32E2529DA963|The ID of the request.|

## Example {#section_vfw_cnb_11s .section}

-   Request example

    ``` {#codeblock_r34_jtf_hj0 .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreatAccessRule
    &AccessGroupName=classic-test
    &AccessRuleId=1
    &<Public Request Parameter>
    ...
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_mxx_16p_a7h .language-xml}
        <? xml version="1.0" encoding="UTF-8"? >
        <DeleteAccessRuleResponse>
          <RequestId>5B4511A7-C99E-4071-AA8C-32E2529DA963</RequestId>
        </DeleteAccessRuleResponse>
        							
        ```

    -   JSON example

        ``` {#codeblock_zfl_yz6_0up .language-json}
        {
          "RequestId": "5B4511A7-C99E-4071-AA8C-32E2529DA963",
        }
        							
        ```


## Error codes {#section_4v6_2ce_hde .section}

