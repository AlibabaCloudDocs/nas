# DescribeSnapshots {#doc_api_NAS_DescribeSnapshots .reference}

DescribeSnapshots 用于查询一个文件系统所有的快照列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=NAS&api=DescribeSnapshots&type=RPC&version=2017-06-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|FileSystemType|String|是|extreme|文件系统类型，可选值：extreme。

 |
|Action|String|否|DescribeSnapshots|系统规定参数。取值：DescribeSnapshots。

 |
|FileSystemId|String|否|extreme-22fd123|指定的文件系统 ID。

 |
|PageNumber|Integer|否|1|快照列表的页码。起始值：1，默认值：1。

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：100，默认值：10。

 |
|SnapshotIds|String|否|s-extreme-xxxxxxxxx,s-extreme-yyyyyyyyy,s-extreme-zzzzzzzzz|快照标识编码。取值可以由多个快照 ID 组成，多个ID用半角逗号（,）隔开，最多支持 100 个ID。

 |
|SnapshotName|String|否|FinanceJoshua|快照名称。

 |
|SnapshotType|String|否|all|快照类型。取值范围：

 -   auto：自动快照
-   user：手动创建的快照
-   all（默认）：所有快照类型

 |
|Status|String|否|all|快照状态。取值范围：

 -   progressing：正在创建的快照
-   accomplished：创建成功的快照
-   failed：创建失败的快照
-   all（默认）：所有快照状态

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|快照列表的页码。

 |
|PageSize|Integer|10|输入时设置的每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|Snapshots| | |快照详情集合。

 |
|CreateTime|String|2014-07-24T13:00:52Z|创建时间。按照 [ISO8601](https://help.aliyun.com/document_detail/25696.html) 标准表示，并需要使用UTC时间。格式为：yyyy-MM-ddThh:mmZ。

 |
|Description|String|FinanceDept|接口说明信息。

 |
|Progress|String|100|快照创建进度，单位为百分比。

 |
|RemainTime|Integer|38|正在创建的快照剩余完成时间，单位为秒。

 |
|RetentionDays|Integer|30|自动快照保留天数。

 |
|SnapshotId|String|s-extreme-snapshotid1|快照 ID。

 |
|SnapshotName|String|FinanceJoshua|快照显示名称。如果创建时指定了快照显示名称，则返回。

 |
|SourceFileSystemId|String|extreme-012321d|源文件系统 ID，如果快照的源文件系统已经被删除，该字段仍旧保留。

 |
|SourceFileSystemSize|Long|2000|源文件系统容量，单位：GB。

 |
|Status|String|accomplished|快照状态。取值范围：progressing、accomplished、failed

 |
|TotalCount|Integer|36|快照总个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeSnapshots
&FileSystemType=extreme
&<公共请求参数>
…

```

正常返回示例

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"DBECAD38-CFA8-4799-A746-BAEF6ABA0C4F",
	"Snapshots":{
		"Snapshot":[
			{
				"Status":"progressing",
				"Description":"",
				"SnapshotName":"xoxo",
				"CreateTime":"1563791255",
				"RemainTime":0,
				"SnapshotId":"s-extreme-67pxwk9aevrkrwwj8",
				"SourceFileSystemSize":1,
				"RetentionDays":-1,
				"SourceFileSystemId":"extreme-06d8cac6",
				"Progress":"0"
			}
		]
	}
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.alibabacloud.com/status/product/NAS)查看更多错误码。

