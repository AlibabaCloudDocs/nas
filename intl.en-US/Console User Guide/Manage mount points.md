# Manage mount points {#task_27531_zh .task}

This topic describes how to manage mount points in the Network Attached Storage \(NAS\) console. The management includes creating, deleting, enabling, and disabling mount points. It also includes viewing a list of mount points, and modifying the permission group of a mount point.

## Create a mount point {#section_6xi_a3u_zkq .section}

You must use a mount point to mount a file system on an ECS instance. You can perform the following steps to create a mount point in the NAS console.

**Note:** You can create a NAS Capacity file system or NAS Performance file system in a classic network or VPC. You can create a maximum of two mount points for each file system.

1.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).
2.  Choose **NAS** \> **File System List**.
3.  Locate the target file system and click **Add Mount Point**.
4.  In the **Add Mount Point** dialog box, configure the required settings.

    ![Create a mount point](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18694/156410769050629_en-US.png)

    **Mount Point Type**: includes VPC and classic network.

    -   If you need to create a mount point with the VPC type, configure the settings as described in the following table.

        |Name|Description|
        |----|-----------|
        |VPC| Select a VPC. If no VPC is available, create a VPC in the [Virtual Private Cloud console](https://vpc.console.aliyun.com/).

**Note:** The VPC and VSwitch you select must be the same as those of the ECS instance on which you mount a file system.

 |
        |VSwitch| Select a VSwitch that is created in the VPC.

 |
        |Permission Group| Select **VPC default permission group \(allow all\)** or an existing permission group.

**Note:** This VPC default permission group is generated for each Alibaba Cloud account, which allows access to the file system through the mount point from all IP addresses of the VPC. For more information about how to create a permission group, see [Manage permission groups](../reseller.en-US/Console User Guide/Manage permissions/Manage permission groups.md#).

 |

    -   If you need to create a mount point in a classic network, configure the settings as described in the following table.

        |Name|Description|
        |----|-----------|
        |Permission group| Select a permission group. If no available permission group exists, create a permission group in the [NAS console](https://nas.console.aliyun.com/#/accessGroup/list).

**Note:** 

        -   You can only create a mount point with the classic network type in a region that is located in China.
        -   You can only attach a mount point with the classic network type to an ECS instance.
        -   For data security, NAS dos not provide a permission group for a mount point with the classic network type. Therefore, you need to create a permission group with the network type set as classic network before specifying the permission group for a mount point with the classic network type. Then, you need to add the required rules to the permission group. For more information about how to manage permission groups, see [Manage permission groups](../reseller.en-US/Console User Guide/Manage permissions/Manage permission groups.md#).
        -   When creating a mount point in a classic network for the first time, you are required to use RAM to authorize NAS to access ECS instances hosted by the logon Alibaba Cloud account. We recommend that you follow the instructions to complete the authorization and create a mount point in a classic network. For more information, see [Why do I need RAM permissions to create a mount point in a classic network](../reseller.en-US/FAQ/FAQs/Why do I need RAM permissions to create a mount point in a classic network.md#).
 |

5.  After you complete the configuration, click **OK**.

## View a list of mount points {#section_sq4_zlm_hfb .section}

On the **File System List** page, locate the target file system, and click **Manage** to open the **File System Details** page. In the Mount Point section, view the list of mount points.

![View a list of mount points](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18694/156410769032271_en-US.png)

## Enable or disable a mount point {#section_w12_cnm_hfb .section}

You can perform the following actions to control access to the mount point from clients.

-   Click **Disable** to disable access to the mount point from clients.
-   Click **Activate** to allow access to the mount point from clients.

## Delete a mount point {#section_bqs_vnm_hfb .section}

Click **Delete** to delete a mount point.

**Note:** Use caution while deleting a mount point. After you delete a mount point, the mount point cannot be restored.

## Modify the permission group of a mount point {#section_zwh_d4m_hfb .section}

Click **Modify Permission Group** to modify the permission group of a mount point. For more information about permission groups, see [Manage permission groups](reseller.en-US/Console User Guide/Manage permissions/Manage permission groups.md#).

**Note:** After you modify the permission group, the modification process requires about one minute to complete.

