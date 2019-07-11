# CreateFileSystem {#doc_api_NAS_CreateFileSystem .reference}

You can call this operation to create file systems.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=NAS&api=CreateFileSystem) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ProtocolType|String|Yes|NFS| The protocol type of the file system. Valid values: NFS and SMB.

 |
|StorageType|String|Yes|Performance| The type of the file system. Valid values: Performance and Capacity.

 |
|Action|String|No|CreateFileSystem| The operation that you want to perform. Set the value to CreateFileSystem.

 |
|Description|String|No|balabala| The description of the file system. The description must be 2 to 128 characters in length. The description must start with a letter, but cannot start with http:// or https://. The description can contain letters, numbers, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|FileSystemId|String|1ca404a666| The ID of the new file system.

 |
|RequestId|String|98696EF0-1607-4E9D-B01D-F20930B68845| The request ID.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

GET https://nas.cn-hangzhou.aliyuncs.com/?Action=CreateFileSystem
&StorageType=Performance
&ProtocolType=NFS
&Description=balabala
&<Common request parameters>

```

Sample success response

`XML` format

``` {#xml_return_success_demo}
<CreateFileSystemResponse>
  <FileSystemId>1ca404a666</FileSystemId>
  <RequestId>98696EF0-1607-4E9D-B01D-F20930B68845</RequestId>
</CreateFileSystemResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"FileSystemId":"1ca404a666",
	"RequestId":"98696EF0-1607-4E9D-B01D-F20930B68845"
}
```

## Error codes {#section_li6_9n8_w2l .section}

For more information, see [Error codes](https://error-center.alibabacloud.com/status/product/NAS).

