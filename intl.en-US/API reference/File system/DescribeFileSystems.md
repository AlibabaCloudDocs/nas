# DescribeFileSystems {#doc_api_NAS_DescribeFileSystems .reference}

You can call this operation to retrieve a list of file systems and the details of each file system.

## Debugging {#section_vg6_amh_y9q .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=DescribeMountTargets) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|DescribeFileSystems| The operation that you want to perform. Set the value to DescribeFileSystems.

 |
|FileSystemId|String|No|109c042666| The ID of the file system.

 |
|FileSystemType|String|No|standard| The type of file system. Valid values: standard and extreme. Default value: standard.

 |
|PageNumber|Integer|No|1| The number of a page. The number starts at 1.

 |
|PageSize|Integer|No|1| The number of file systems that are displayed on each page. Default value: 10.

 |
|VpcId|String|No|vpc-bp1sevsgtqvk5gxblhhod| The VPC ID.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1| The number of a page.

 |
|PageSize|Integer|1| The number of file systems that are displayed on each page.

 |
|RequestId|String|035B3A3A-E514-4B41-B906-5D906CFBD65F| The request ID.

 |
|TotalCount|Integer|1| The total number of file systems.

 |
|FileSystems| | | A list of file systems and the details of each file system.

 |
|Bandwidth|Long|150| The maximum throughput of the file system. Unit: Mbit/s. This parameter is only applicable to standard file systems.

 |
|Capacity|Long|1| The capacity of the file system. Unit: GB.

 |
|CreateTime|String|2017-05-27T15:43:06CST| The time when the file system is created.

 |
|Description|String|Null| The description of the file system.

 |
|Description|String|Null| The description of the file system.

 |
|FileSystemId|String|109c042666| The file system ID.

 |
|MeteredSize|Long|1611661312| The used space of the file system. The value indicates the maximum amount of used space over the last one hour rather than the current used space. Unit: Byte.

 |
|MountTargets| | | A list of mount points and the details of each mount point.

 |
|AccessGroupName|String|test-001| The name of the permission group that applies to the mount point.

 |
|MountTargetDomain|String|109c042666-wjb85.cn-hangzhou.nas.aliyuncs.com| The name of the mount point.

 |
|NetworkType|String|vpc| The network type. Valid values: vpc and classic.

 |
|Status|String|active| The status of the mount point. This parameter is only applicable to standard file systems. Valid values: active and inactive.

 |
|VpcId|String|vpc-bp1sevsgtqvk5gxblhhod| vpcid

 |
|VswId|String|vsw-bp1omfzsszekkvaxnz66e| vswid

 |
|Packages| | | The storage package that is bound to the file system.

 |
|PackageId|String|naspackage-xxxxxxxxxxx-xxxxxx| The ID of the storage package.

 |
|ProtocolType|String|NFS| The protocol type.

 |
|RegionId|String|cn-hangzhou| The region ID.

 |
|Status|String|Pending| The status of the file system. This parameter is only applicable to NAS Extreme. Valid values: Pending, Running, and Stopped. You can perform subsequent operations such as creating a mount point only when the status is Running.

 |
|StorageType|String|Performance| The storage type. Valid values for NAS Standard: Capacity and Performance. Valid values for NAS Extreme: standard and advance.

 |
|ZoneId|String|cn-hangzhou-b| The zone where the file system is located.

 |

## Example {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=DescribeFileSystems
&FileSystemId=109c042666
&<Common request parameters>

```

Sample success response

`XML` format

``` {#xml_return_success_demo}
<DescribeFileSystemsResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>1</TotalCount>
  <PageSize>1</PageSize>
  <RequestId>035B3A3A-E514-4B41-B906-5D906CFBD65F</RequestId>
  <FileSystems>
    <FileSystem>
      <FileSystemId>109c042666</FileSystemId>
      <ProtocolType>NFS</ProtocolType>
      <RegionId>cn-hangzhou</RegionId>
      <CreateTime>2017-05-27T15:43:06CST</CreateTime>
      <Destription/>
      <MountTargets>
        <MountTarget>
          <MountTargetDomain>109c042666-wjb85.cn-hangzhou.nas.aliyuncs.com</MountTargetDomain>
        </MountTarget>
      </MountTargets>
      <StorageType>Performance</StorageType>
      <MeteredSize>1611661312</MeteredSize>
    </FileSystem>
  </FileSystems>
</DescribeFileSystemsResponse>

```

`JSON` format

``` {#codeblock_dbu_d7m_rzs}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":1,
	"RequestId":"BC7C825C-5F65-4B56-BEF6-98C56C7C546E",
	"FileSystems":{
		"FileSystem":[
			{
				"FileSystemId":"31a8e48eda",
				"Description":"31a8e48eda",
				"Packages":{
					"Package":[
						{
							"PackageId":""
						}
					]
				},
				"ProtocolType":"NFS",
				"CreateTime":"2017-04-18T00:22:56CST",
				"RegionId":"cn-shanghai",
				"Destription":"31a8e48eda",
				"ZoneId":"cn-shanghai-b",
				"StorageType":"Performance",
				"MountTargets":{
					"MountTarget":[
						{
							"NetworkType":"vpc",
							"Status":"active",
							"VswId":"vsw-uf64zi0nn71ntvkbzdti4",
							"AccessGroupName":"DEFAULT_VPC_GROUP_NAME",
							"MountTargetDomain":"31a8e48eda-ykf64.cn-shanghai.nas.aliyuncs.com",
							"VpcId":"vpc-uf65wx2khu08h4dlw2qfv"
						}
					]
				},
				"MeteredSize":4295639040
			}
		]
	}
}
```

## Error codes {#section_cgz_wcz_x0t .section}

