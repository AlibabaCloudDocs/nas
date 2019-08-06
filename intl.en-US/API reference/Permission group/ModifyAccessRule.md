# ModifyAccessRule {#concept_62641_zh .concept}

ModifyAccessRule is used to modify permission rules.

## Debugging {#section_5bh_8uk_ncs .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#section_n4b_7of_ywe .section}

|Parameter name|Type|Required|Example|Description|
|--------------|----|--------|-------|-----------|
|Action|String|Yes|ModifyAccessRule|Operation interface name and system required parameter. Value: ModifyAccessRule.|
|AccessGroupName|String|Yes|classic-test|Permission group name.|
|AccessRuleId|String|Yes|1|Permission rule ID.|
|FileSystemType|String|No|standard|The type of the file system. Valid values: standard and extreme. Default value: standard.|
|SourceCidrIp|String|No|192.168.0.1| An IP address or a CIDR notation. For example, 12.1.1.1 or 13.1.1.1/25.

 |
|RWAccessType|String|No|RDWR|Read-write permission type.|
|UserAccessType|String|No|all\_squash|User permission type.|
|Priority|Integer|No|1|Priority level. Range: 1-100. Default value: 1.|

## Response parameters {#section_kkp_ezd_us4 .section}

|Parameter name|Type|Example|Description|
|--------------|----|-------|-----------|
|RequestId|String|6299428C-3861-435D-AE54-9B330A0007C8|The ID of the request.|

## Example {#section_4jw_l5s_ag7 .section}

-   Request example

    ``` {#codeblock_4m0_qwr_uqe .language-shell}
    GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAccessRule
    &AccessGroupName=classic-test
    &AccessRuleId=1
    &SourceCidrIp=192.168.0.1
    &RWAccessType=RDWR
    &UserAccessType=all_squash
    &<Public Request Parameter>
    …
    					
    ```

-   Response example
    -   XML example

        ``` {#codeblock_4ah_4df_o57 .language-xml}
        <? xml version="1.0" encoding="UTF-8"? >
        <ModifyAccessRuleResponse>
          <RequestId>6299428C-3861-435D-AE54-9B330A0007C8</RequestId>
        </ModifyAccessRuleResponse>
        							
        ```

    -   JSON example

        ``` {#codeblock_21w_6gi_916 .language-json}
        {
          "RequestId": "6299428C-3861-435D-AE54-9B330A0007C8",
        }
        							
        ```


## Error codes {#section_17b_zw0_lun .section}

For more information, see [Error codes](https://error-center.alibabacloud.com/status/product/NAS).

