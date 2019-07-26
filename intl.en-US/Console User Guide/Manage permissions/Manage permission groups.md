# Manage permission groups {#task_27534_zh .task}

This topic describes how to manage permission groups in the Network Attached Storage \(NAS\) console. The management includes creating and deleting permission groups and rules, viewing a list of permission groups, and viewing a list of rules.

A permission group is a whitelist of a mount point. You can add IP addresses and IP segments to a permission group by adding rules. You can also grant different levels of permissions to the IP addresses and IP segments in the rules.

When NAS is activated, a permission group named VPC default permission group \(allow all\) is generated. The default permission group allows read/write access to a mount point from all IP addresses in a VPC, and no limit is specified for root users.

**Note:** 

-   For a mount point that is located in a classic network, no default permission group is provided. You need to bind a custom permission group to the mount point. In the custom permission group, you can only specify one IP address in each rule, and IP segments are not supported.
-   We recommend that you only add rules for required IP addresses and IP segments to ensure data security.
-   You cannot delete or modify the default permission group and its rules.
-   You can create a maximum of 10 permission groups by using an Alibaba Cloud account.

## Create a permission group and add rules {#section_0la_i30_27g .section}

1.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).
2.  Create a permission group.
    1.  Choose **NAS** \> **Permission Group** and click **Create Permission Group**.
    2.  In the Create Permission Group dialog box, configure the required settings.

        ![manage permission](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18697/156410760752619_en-US.png)

        |Name|Description|
        |----|-----------|
        |Region|Select a region that hosts the permission group.|
        |Name|The name of the permission group.|
        |Network Type|Valid values: VPC and classic network.|

3.  Add a rule
    1.  Locate the target permission group and click **Manage**.
    2.  On the Permission Group Rules page, click **Add Rule**.
    3.  Configure the required settings.

        ![permission rule](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18697/156410760752620_en-US.png)

        |Name|Description|
        |----|-----------|
        |**Authorization Address**| The authorized object to which this rule applies.

 |
        |**Read/Write Permissions**|Indicates whether to allow read-only or read/write access to the file system from the authorized object. Valid values: **Read-only** and **Read/Write**.|
        |**User Permission**|Indicates whether to limit a Linux user's access to a file system. When a Linux user attempts to access the files or directories of a file system, the specified user permission is checked.

        -   **Do not limit root users \(no\_squash\)**: allows access to a file system from root users.
        -   **Limit root users \(root\_squash\)**: denies access to a file system from root users. All root users are treated as nobody users.
        -   **Limit all users \(all\_squash\)**: denies access to a file system from all users including root users. All users are treated as nobody users.
 |
        |**Priority**|When an authorized object matches multiple rules, the rule with the highest priority takes effect. 1 to 100, in which 1 is the highest priority.

 |

    4.  Click **OK**.

## More actions {#section_23a_bcs_9ix .section}

On the Permission Group page, you can perform the following actions.

|Action|Description|
|------|-----------|
|View the list of permission groups or the details of a permission group.|View the list of permission groups in a region or view the details of a permission group. The details include the type, number of rules, and number of linked file systems.|
|Modify a permission group|Locate the target permission group and click **Edit** to modify the description of the permission group.|
|Delete a permission|Locate the target permission group and click **Delete** to delete the permission group.|
|View the list of rules|Locate the target permission group and click **Manage** to view the list of rules in the permission group.|
|Modify a rule|Click **Manage**, locate the target rule, and click **Edit** to modify fields including the Authorization Address, Read/Write Permissions, User Permission, and Priority.|
|Delete a rule|Click **Manage**, locate the target rule, and click **Delete** to delete the rule.|

