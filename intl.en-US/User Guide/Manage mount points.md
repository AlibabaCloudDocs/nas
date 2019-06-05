# Manage mount points {#concept_27531_zh .concept}

In the NAS console, you can perform multiple operations on mount points. These operations include viewing a list of mount points, deleting a mount point, modifying the permission group of a mount point, disabling a mount point, and enabling a mount point.

## Prerequisites {#section_ekf_pjm_hfb .section}

Before operating a mount point, you must perform the following actions:

1.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).
2.  [Create a file system](../../../../reseller.en-US/Quick Start/Create a file system.md#)Create at least one file system.
3.  [Add a mount point](../../../../reseller.en-US/Quick Start/Add a mount point.md#)Add at least one mount point to a file system.

## View a list of mount points {#section_sq4_zlm_hfb .section}

On the **File System List** page, click the name of a file system to open the **File System Details** page. On the File System Details page, you can manage mount points in the Mount Point section. You can perform multiple actions, such as **adding a mount point**, **modifying the permission group of a mount point**, **enabling** or **disabling** a mount point, and **deleting** a mount point.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18694/155972787732271_en-US.png)

## Add a mount point {#section_dvy_xmm_hfb .section}

You can add one or more mount points to a file system. For more information, see [Add a mount point](../../../../reseller.en-US/Quick Start/Add a mount point.md#).

## Enable or disable a mount point {#section_w12_cnm_hfb .section}

You can click **Disable** next to a mount point to prevent a client from accessing the mount point, or click **Activate** to enable access.

## Delete a mount point {#section_bqs_vnm_hfb .section}

You can click **Delete** next to a mount point to delete the mount point. You cannot restore a deleted mount point.

**Note:** Before deleting a VPC, you must remove all mount points located in the VPC.

## Modify the permission group of a mount point {#section_zwh_d4m_hfb .section}

You must bind a permission group to each mount point. ECS instances whose IP addresses are added to the permission group of a mount point are allowed to access the mount point. You can click **Modify Permission Group** next to a mount point to modify the permission group of the mount point.

**Note:** The process of modifying the permission group requires up to one minute.

