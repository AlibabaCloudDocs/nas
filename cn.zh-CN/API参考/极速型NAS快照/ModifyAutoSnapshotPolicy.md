# ModifyAutoSnapshotPolicy {#doc_api_NAS_ModifyAutoSnapshotPolicy .reference}

ModifyAutoSnapshotPolicy 用于修改一条自动快照策略。修改自动快照策略后，之前已应用该策略的文件系统随即执行修改后的自动快照策略。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=ModifyAutoSnapshotPolicy&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AutoSnapshotPolicyId|String|是|sp-extreme-233e6ylv0|目标自动快照策略 ID。您可以调用 DescribeAutoSnapshotPolicies 查看您可用的自动快照策略。

 |
|Action|String|否|ModifyAutoSnapshotPolicy|系统规定参数。取值：ModifyAutoSnapshotPolicy。

 |
|AutoSnapshotPolicyName|String|否|FinanceJoshua|自动快照策略的名称。如果参数为空则代表不修改。

 |
|RepeatWeekdays|String|否|1,7|自动快照的重复日期，单位为天，周期为星期。取值范围：1~7，如1表示周一。当一星期内需要创建多次自动快照时，可以传入多个时间点：

 -   最多传入 7 个时间点。
-   多个时间点用半角逗号（,）隔开。

 |
|RetentionDays|Integer|否|30|自动快照的保留时间，单位为天。取值范围：

 -   -1（默认）：永久保存。
-   1~65536：指定保存天数。

 |
|TimePoints|String|否|0,1|自动快照的创建时间点，单位为小时。取值范围：0~23，代表00:00至23:00共24个时间点，如1表示01:00。当一天内需要创建多次自动快照时，可以传入多个时间点：

 -   最多传入 24 个时间点。
-   多个时间点半角逗号（,）隔开。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=ModifyAutoSnapshotPolicy
&AutoSnapshotPolicyId=sp-extreme-6i0brwewjt0gfylh0
&AutoSnapshotPolicyName=xoxo
&<公共请求参数>
…

```

正常返回示例

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"12FA778B-C8D3-4D2B-88AD-C10ED0326C57"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/NAS)查看更多错误码。

