# Manage the data access permissions of a file system {#concept_27534_zh .concept}

You can use permission groups to manage data access permissions of a file system in Network Attached Storage \(NAS\).

## Introduction {#section_znp_brm_hfb .section}

A permission group can be a whitelist or a blacklist of a mount point. You can add IP addresses and IP segments to a permission group by adding rules. You can also grant different levels of permissions to the IP addresses and IP segments in the rules.

When NAS is activated, a permission group named VPC default permission group \(allow all\) is generated. The default permission group allows read/write access to a mount point from all IP addresses in a VPC and no limit is specified for root users.

**Note:** 

-   For a mount point that is located in a classic network, no default permission group is provided. You need to bind a custom permission group to the mount point. In the custom permission group, you can only specify one IP address in each rule, and IP segments are not supported.
-   We recommend that you only specify required IP addresses or IP segments when adding rules to a permission group to ensure data security.

## Create a permission group {#section_ot2_xrm_hfb .section}

Proceed as follows to create a permission group

1.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).
2.  In the left-side navigation pane, select **Permission Group**, and then click **Create Permission Group** in the upper-right corner.
3.  Enter a name to create a new permission group.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18697/155972816332272_en-US.png)


**Note:** With an Alibaba Cloud account, you can create up to 10 permission groups.

## Manage permission group rules {#section_efy_3sm_hfb .section}

You can add, modify, and delete permission group rules.

1.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).
2.  In the left-side navigation pane, select **Permission Group**, and then click **Manage** next to a permission group.
3.  On the **Permission Group Rules** page,
    -   you can click **Add Rule** in the upper-right corner to add a rule.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18697/155972816332287_en-US.png)

        For a rule, you can configure the following options.

        |Option|Value|Description|
        |------|-----|-----------|
        |**Authorization Address**|An IP address or IP segment. When you add a rule to a permission group whose network type is classic network, you must specify an IP address.|The authorized object to which this rule applies.|
        |**Read/Write Permissions**|**Read-only** and **Read/Write**|Indicates whether to allow read-only or read/write access to a file system from the authorized object.|
        |**User Permission**|**Do not limit root users \(no\_squash\)**, **Limit root users \(root\_squash\)**, and **Limit all users \(all\_squash\)**|Indicates whether to limit a Linux user's access to a file system. When a Linux user attempts to access the files or directories of a file system, the specified user permission is checked.

        -   **Do not limit root users \(no\_squash\)**: allows access to a file system from root users.
        -   **Limit root users \(root\_squash\)**: denies access to a file system from root users. All root users are treated as nobody users.
        -   **Limit all users \(all\_squash\)**: denies access to a file system from all users including root users. All users are treated as nobody users.
 |
        |**Priority**|1 to 100, in which 1 is the highest priority|When an authorized object matches multiple rules, the rule with the highest priority takes effect.|

    -   After you create a permission group rule, you can click **Edit** or **Delete** next to the rule to modify or delete this rule.

        ![](images/32289_en-US.png)


