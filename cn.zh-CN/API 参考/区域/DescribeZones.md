# DescribeZones {#reference_ddf_xmw_mfb .reference}

DescribeZones用于查询某个 Region 下的所有可用区及可用区所支持的 NAS 类型。

## 请求参数 {#section_vgm_jnw_mfb .section}

|参数名称|类型|是否必需|描述|
|:---|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：DescribeZones|

## 返回参数 {#section_k5y_44w_mfb .section}

|参数名称|类型|描述|
|:---|:-|:-|
|RequestId|String|请求ID|
|Zones|数组|每个元素是一个Zone|

## 示例 {#section_yjp_1pw_mfb .section}

-   请求示例

    ```
    https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeZones
    &<公共请求参数>
    ```

-   返回示例
    -   XML示例

        ```
        <?xml version="1.0" encoding="UTF-8"?>
        <DescribeZones>
            <RequestId>A70BEE5D-76D3-49FB-B58F-1F398211A5C3</RequestId>
            <Zones>
                <Zone>
                    <Performance>
                    </Performance>
                    <Capacity>
                        <Protocol>nfs</Protocol>
                        <Protocol>smb</Protocol>
                        <Protocol>nasplus</Protocol>
                    </Capacity>
                    <ZoneId>cn-hangzhou-b</ZoneId>
                </Zone>
                <Zone>
                    <Performance>
                        <Protocol>nfs</Protocol>
                        <Protocol>smb</Protocol>
                    </Performance>
                    <Capacity>
                        <Protocol>nfs</Protocol>
                        <Protocol>smb</Protocol>
                        <Protocol>nasplus</Protocol>
                    </Capacity>
                    <ZoneId>cn-hangzhou-g</ZoneId>
                </Zone>
                <Zone>
                    <Performance>
                        <Protocol>nfs</Protocol>
                        <Protocol>smb</Protocol>
                        <Protocol>newnfs</Protocol>
                    </Performance>
                    <Capacity>
                    </Capacity>
                    <ZoneId>cn-hangzhou-f</ZoneId>
                </Zone>
            </Zones>
        </DescribeZones>
        ```

    -   JSON示例

        ```
        {
         "RequestId": “A70BEE5D-76D3-49FB-B58F-1F398211A5C3”,
          "Zones": {
            "Zone": [
              {
                "Performance": {
                  "Protocol": []
                },
                "Capacity": {
                  "Protocol": [
                    "nfs",
                    "smb",
                    "nasplus"
                  ]
                },
                "ZoneId": "cn-hangzhou-b"
              },
              {
                "Performance": {
                  "Protocol": [
                    "nfs",
                    "smb"
                  ]
                },
                "Capacity": {
                  "Protocol": [
                    "nfs",
                    "smb",
                    "nasplus"
                  ]
                },
                "ZoneId": "cn-hangzhou-g"
              },
              {
                "Performance": {
                  "Protocol": [
                    "nfs",
                    "smb",
                    "newnfs"
                  ]
                },
                "Capacity": {
                  "Protocol": []
                },
                "ZoneId": "cn-hangzhou-f"
              }
            ]
          }
        }
        ```


