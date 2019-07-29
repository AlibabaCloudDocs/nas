# Create a custom policy {#task_845375 .task}

This topic describes how to create a custom policy and grant the policy to a RAM user account. Custom policies provide you with fine-grained permissions to meet your actual business requirements. These policies make it easier and more flexible to adapt and manage permissions.

## Procedure {#section_lif_gr0_yuz .section}

1.  Log on to the [RAM console](https://ram.console.aliyun.com/overview) by using an Alibaba Cloud account.
2.  In the left-side navigation pane, select **Policies**, click **Create Policy**, and follow the instructions to create a policy. The following takes the NASReadOnlyAccess policy as an example. This policy allows read-only access to all NAS resources. For more information, see [../../SP\_65/DNRAM11885314/EN-US\_TP\_23770.dita\#concept\_srq\_fbk\_xdb](../../SP_65/DNRAM11885314/EN-US_TP_23770.dita#concept_srq_fbk_xdb).

    ``` {#codeblock_axc_8u8_8d3}
    {
        "Statement": [
            {
                "Effect": "Allow",
                "Action": "nas:Describe*",
                "Resource": "*"
            }
        ],
        "Version": "1"
    }
    					
    ```

    API operations that you can call to manage NAS file systems are listed in the following table.

    |Action|Description|
    |------|-----------|
    |DescribeFileSystems|List all file systems|
    |DescribeMountTargets|List all mount points|
    |DescribeAccessGroup|List all permission groups|
    |DescribeAccessRule|List all permission group rules|
    |CreateMountTarget|Add a mount point for a file system|
    |CreateAccessGroup|Create permission groups|
    |CreateAccessRule|Create permission group rules|
    |DeleteFileSystem|Delete file systems|
    |DeleteMountTarget|Delete mount points|
    |DeleteAccessGroup|Delete permission groups|
    |DeleteAccessRule|Delete permission group rules|
    |ModifyMountTargetStatus|Enable or disable mount points|
    |ModifyMountTargetAccessGroup|Modify the permission group of a mount point|
    |ModifyAccessGroup|Modify permission groups|
    |ModifyAccessRule|Modify permission group rules|

    The NAS resources that are accessible by clients are listed in the following table.

    |Resource|Description|
    |--------|-----------|
    |\*|Indicates all NAS resources.|

3.  After the policy is created, go to the Users page.
4.  Select a RAM user account to be authorized, click **Add Permissions**, select the required NAS permission, and grant the permission to the RAM user account.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18696/156436747252616_en-US.png)


