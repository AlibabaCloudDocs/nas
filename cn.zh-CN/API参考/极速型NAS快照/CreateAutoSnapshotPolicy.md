# CreateAutoSnapshotPolicy {#doc_api_NAS_CreateAutoSnapshotPolicy .reference}

CreateAutoSnapshotPolicy 用于创建一条自动快照策略。创建的自动快照策略可以应用到任一文件系统（ApplyAutoSnapshotPolicy），成功创建的自动快照策略可以后续修改策略内容（ModifyAutoSnapshotPolicies）。

## 接口说明 {#description .section}

-   一个阿里云账户在一个地域最多能创建 100 条自动快照策略。
-   如果文件系统数据较多，单次创建自动快照的时长超过两个时间点间隔，则自动跳过下一时间点。示例：您设置了09:00、10:00、11:00 和12:00 为自动快照时间点。由于文件系统数据较多，09:00 开始创建快照，10:20 完成创建快照，实际耗时 80 分钟。系统会跳过 10:00 时间点，等到 11:00 继续为您创建自动快照。
-   快照数量总额度 64 个，达到快照额度上限后，系统会自动删除最早创建的自动快照，手动快照不受影响。
-   修改自动快照策略的保留时间时，仅对新增快照生效，历史快照沿用历史保留时间。
-   正在对某一个文件系统执行自动快照时，您需要等待自动快照完成后，才能手动创建快照。
-   非正常状态的文件系统无法执行自动快照策略。
-   创建的自动快照具有统一命名格式 auto\_yyyyMMdd\_X，其中auto：表示自动快照，与手动快照区分；yyyyMMdd：创建快照的日期，y 表示年、M 表示月、d 表示天；X：当日创建的第几份自动快照。例如：auto\_20140418\_1 表示 2014 年 4 月 18 日创建的第一份自动快照。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=CreateAutoSnapshotPolicy&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|FileSystemType|String|是|extreme|文件系统类型，可选值：extreme。

 |
|RepeatWeekdays|String|是|1,2,3|自动快照的重复日期，单位为天，周期为星期。取值范围：1~7，如 1 表示周一。当一星期内需要创建多次自动快照时，可以传入多个时间点：

 -   最多传入7个时间点。
-   多个时间点用半角逗号（,）隔开。

 |
|TimePoints|String|是|0,1,…23|自动快照的创建时间点，单位为小时。取值范围：0~23，代表 00:00 至 23:00 共 24 个时间点，如 1 表示 01:00。当一天内需要创建多次自动快照时，可以传入多个时间点，最多传入 24 个时间点。

 |
|Action|String|否|CreateAutoSnapshotPolicy|系统规定参数。取值：CreateAutoSnapshotPolicy。

 |
|AutoSnapshotPolicyName|String|否|FinanceJoshua|自动快照策略的名称。长度为 2~128 个英文或中文字符，必须以大小字母或中文开头，可包含数字、半角冒号（:）、下划线（\_）或连字符（-），不能以 http:// 和 https:// 开头。默认值：空

 |
|RetentionDays|Integer|否|30|自动快照的保留时间，单位为天。默认值：-1。取值范围：

 -   -1：永久保存。
-   1~65536：指定保存天数。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoSnapshotPolicyId|String|sp-extreme-233e6ylv0|自动快照策略ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateAutoSnapshotPolicy
&FileSystemType=extreme
&RepeatWeekdays=1,2,3
&TimePoints=0,1,2,3,4
&<公共请求参数>
…

```

正常返回示例

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"12FA778B-C8D3-4D2B-88AD-C10ED0326C57",
	"AutoSnapshotPolicyId":"sp-extreme-6i0brwewjt0gfylh0"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/NAS)查看更多错误码。

