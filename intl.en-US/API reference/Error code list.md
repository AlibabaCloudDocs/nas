# Error code list {#concept_62603_zh .concept}

Various error code messages are returned when API exceptions occur.

## Error code {#section_yr5_jjg_hfb .section}

An error code is composed of four parts.

|Component|Definition|
|---------|----------|
|HttpCode|HTTP response code that complies with HTTP syntax|
|Code|Error code|
|Message|Error message|
|Resolution|Recommended solution|

## Error code list {#section_qvj_njg_hfb .section}

|HttpCode|Code|Message|Resolution|
|--------|----|-------|----------|
|500|InternalError|The request processing has failed due to some unknown error.|Please try again later.|
|503|ServiceUnavailable|The request has failed due to a temporary failure of the server.|Please try again later.|
|504|ServiceTimeout|The request processing has failed due to timeout.|Please try again later.|
|503|SecurityToken.CheckFailed|The security token check has failed due to some internal error.|Please try again later.|
|503|SecurityToken.DecodeFailed|The security token decode has failed due to some internal error.|Please try again later.|
|503|SubRam.CheckFailed|The sub user Ram check has failed due to some internal error.|Please try again later.|
|503|VpcRam.CheckFailed|The Vpc ram check has failed due to some internal error.|Please try again later.|
|503|VpcSubRam.CheckFailed|The Vpc sub user ram check has failed due to some internal error.|Please try again later.|
|400|Missingparameter. calleruid|Parameter \`callerUid\` is mandatory for this action.|Add the callerUid request parameter.|
|400|MissingParameter.RegionId|Parameter \`RegionId\` in endpoint is mandatory for this action.|Add the RegionId field to the domain name.|
|400|MissingParameter.VSwitchId|Parameter \`VSwitchId\` is mandatory for this action.|Add the VSwitchId request parameter.|
|400|MissingParameter.VpcId|Parameter \`VpcId\` is mandatory for this action.|Add the VpcId request parameter.|
|400|InvalidParameter.StorageType|Parameter \`StorageType\` is mandatory for this action.|A valid StorageType request parameter must contain Performance and Capacity.|
|400|InvalidParameter.ProtocalType|Parameter ProtocalType is mandatory for this action.|A valid ProtocalType request parameter must contain NFS and SMB.|
|400|InvalidParameter.Description|Parameter Description is mandatory for this action.|A valid Description string must contain Chinese and English characters in addition to @, \#, $, \_, +, and -.|
|404|InvalidFileSystem.NotFound|The specified FileSystem does not exist.|The specified file system does not exist or has been deleted.|
|403|InvalidFileSystem.AlreadyExisted|The specified FileSystem has been already existed.|The specified file system already exists. You can call DescribeFileSystems and specify the file system ID to view its information.|
|404|InvalidMountTarget.NotFound|The specified MountTarget does not exist.|The specified mount point does not exist or has been deleted.|
|404|InvalidAccessGroup.NotFound|The specified Account does not exist.|The specified permission group does not exist or has been deleted.|
|403|InvalidAccessGroup.AlreadyExisted|The specified AccessGroup has been already existed.|The specified permission group already exists. You can call DescribeMountTargets and specify the permission group to view its information.|
|403|InvalidAccessGroup.AlreadyAttached|The specified AccessGroup is still attached by some MountTarget\(s\).|The specified permission group is bound with one or more mount points. Unbind the mount points first before deleting the permission group.|
|404|InvalidAccessRule.NotFound|The specified AccessRule does not exist.|The specified permission rule does not exist or has been deleted.|
|404|InvalidLocatin.NotFound|The specified Location is not found or is not supported.|The requested Location does not exist or is not currently providing services.|
|404|InvalidRegionId.NotFound|The specified Region is not found.|The requested Region does not exist or is not currently providing services.|
|404|InvalidAZone.NotFound|The specified AZone is not found.|The requested AZone does not exist or is not currently providing services.|
|404|InvalidVpc.NotFound|The specified EcsId is not found.|The specified VPC does not exist. Create a VPC first.|
|404|InvalidVip.NotFound|The specified Vip is not found.|The specified VPC is not found. Make sure you use correct and valid VPC information.|
|404|InvalidLBid.NotFound|The specified LBid is not found.|The system failed to create LBid. Please try again later.|
|404|InvalidVpcTunnelId.NotFound|The specified vpc tunnelId is not found.|The specified VPC tunnelId does not exist. Check the VPC information first.|
|404|InvalidVpc.CreationFailed|The specified vpc instance creation failed.|Failed to create the specified VPC instance. Make sure you use correct and valid VPC information and there is available IP space for the instance, and then try again.|
|403|OperationDenied.DefaultAccessGroupCannotDelete|The default AccessGroup can not be deleted.|You can edit the operation-customized permission group.|
|403|OperationDenied.DefaultAccessGroupCannotModify|The default AccessGroup can not be modified.|You can edit the operation-customized permission group.|
|403|OperationDenied.NetworkTypeNotMatched|The NetworkType of MountTarget is not matched with AccessGroup.|Make sure the NetworkType of the mount point and the AccessGroupType of the permission group are consistent.|
|403|OperationDenied.MountTargetNotEmpty|There are still MountTarget\(s\) on the specified FileSystem.|The specified file system has one or more mount points. Delete the existing mount points first.|
|403|OperationDenied.FileSystemCountsExceeded|The amount of FileSystem has reached its limits\(maximum 10\).| To increase the limit, open a ticket.

 |
|403|OperationDenied.MountTargetCountsExceeded|The amount of MountTarget has reached its limits\(maximum 2 per FileSystem\).| To increase the limit, open a ticket.

 |
|403|OperationDenied.AccessGroupCountsExceeded|The amount of AccessGroup has reached its limits.| To increase the limit, open a ticket.

 |
|403|OperationDenied.AccessRuleCountsExceeded|The amount of AccessRule has reached its limits.| To increase the limit, open a ticket.

 |
|403|User. Disabled|Your account does not open Nas Service yet or balance is insufficient.| If you have not activated the NAS service, activate the service first.

 |
|403|Forbidden.InvalidUserType|The operation is not permitted due to type of account.|Sorry, but NAS-Open API does not currently support your account type.|
|403|Forbbiden.Ram|User not authorized to operate on the specified resource, or this API doesn't support RAM.|Your account RAM permission verification failed. Go to RAM to authorize required NAS permissions.|
|403|Forbidden.EcsTokenNotAuthorized|User not authorized to check ecs on creating MountTarget of classic network type.|Go to RAM to authorize NAS permissions to visit the ECS verification interface.|
|403|NotQualified|User has not been approved for the trail application.| Please initiate an application to try the related features. If your application fails to be approved, open a ticket.

 |

## Response example of error codes { .section}

-   XML format

    ```language-xml
    <? xml version="1.0" encoding="UTF-8"? >
    <Error>
      <RequestId>B71B4C68-6C6B-4D4B-AD70-8951BD7D188E</RequestId>
      <HostId>nas.cn-hangzhou.aliyuncs.com</HostId>
      <Code>InvalidFileSystem.NotFound</Code>
      <Message>The specified file system does not exist</Message>
    </Error>
    
    
    ```

-   JSON format

    ```language-json
    {
      "RequestId": "B71B4C68-6C6B-4D4B-AD70-8951BD7D188E",
      "HostId": " nas.cn-hangzhou.aliyuncs.com ",
      "Code": "InvalidFileSystem.NotFound",
      "Message": "The specified file system does not exist"
    }
    
    
    ```


