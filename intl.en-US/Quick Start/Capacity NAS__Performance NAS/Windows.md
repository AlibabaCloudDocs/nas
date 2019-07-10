# Windows {#concept_60431_zh .task}

## Step 1: Create a file system {#section_hhw_ph5_jip .section}

1.  Log on to the [NAS console](https://nas.console.aliyun.com/).
2.  Choose **NAS** \> **File System List**, and Click **Create File System**.
3.  On the Create File System page, set the parameters.

    |Parameter|Description|
    |---------|-----------|
    |Region| Select the region where you want to create the file system.

**Note:** 

    -   A file system ornode in a region cannot communicate with a file system or computing node in another region.
    -   Each account can create up to 20 file systems.
 |
    |Storage Type| You can select **SSD performance-type** or **Capacity-type**.

**Note:** The maximum storage capacity of a file system is 1 PB for the SSD performance type and 10 PB for the capacity type. Fees are charged based on the actual usage.

 |
    |Protocol Type|You can select **SMB \(2.1and later\)**。 NFS is recommended in Linux and SMB is recommended in Windows.

 |
    |Zone| Zones are physical areas with independent power grids and networks within one region.

 Click the drop-down box to select the zone. we recommend that you select the zone of the ECS instance where you want to mount your file system.

**Note:** A file system or computing node in a zone can communicate with a file system or computing node in a different zone but of the same region.

 |

4.  Click **OK**.

## Step 2: Add a mount point {#section_ggg_2xd_pb7 .section}

After creating a file system, you must add a mount point for the file system before you can mount the file system on ECS. NAS supports two types of mount points: VPC and Classic Network.

1.  Log on to the [NAS console](https://nas.console.aliyun.com/).
2.  Choose **NAS** \> **File System List**.
3.  Click **Add Mount Point** on the right of the file system to which you want to add a mount point.
4.  On the Add Mount Point page, set the parameters.

    **Mount Point Type**: VPC and Classic Network.

    -   If you add a mount point in a VPC, configure the following parameters.

        |Parameter|Description|
        |---------|-----------|
        |VPC| select the permission group in the **Permission Group** drop-down box.

 |
        |VSwitch| Select the Select the switch created under the VPC network.switch created under the VPC network.

 |
        |Permission Group| Select **VPC default permission group \(allow all\)** or the permission group that has been created.

**Note:** You can select **VPC default permission group \(allow all\)** to allow all IP addresses in the same VPC to access the file system through the mount point.

 |

    -   If you add a mount point in a classic network, configure the following parameters.

        |Parameter|Description|
        |---------|-----------|
        |Permission Group| select the permission group in the **Permission Group** drop-down box.

**Note:** 

        -   Currently, only ECS instances can use mount points in classic networks.
        -   For a classic network mount point, no default permission group is provided. When using this for the first time, you must go to the Permission Group page to create a permission group in a classic network, and add rules for the permission group. For more information, see [Manage the data access permissions of a file system](../../../../intl.en-US/Console User Guide/Manage permission/Manage the data access permissions of a file system.md#).
        -   When adding a mount point in a classic network for the first time, you are requested to authorize NAS through RAM to access the query interface of your ECS instance. Follow the instructions to complete the authorization, then try creating the mount point in the classic network again. For more information, see [Why do I need RAM permissions to create a mount point in a classic network](../../../../intl.en-US/FAQ/FAQs/Why do I need RAM permissions to create a mount point in a classic network.md#).
 |

5.  Click **OK**.

## Step 3: Mount an SMB file system {#section_ixc_o25_gpf .section}

You can mount an SMB file system on an ECS instance that runs Windows.

1.  Log on to [ECS console](https://ecs.console.aliyun.com/)。
2.  You can run the following command to mount an SMB file system.

    ``` {#codeblock_xom_3j4_tdj}
    net use D: \\file-system-id.region.nas.aliyuncs.com\myshare
    ```

    Mount command format: `net use <target mount drive> \\<domain name of the mount point>\myshare`。

    -   Target mount drive: the mount drive of the target Windows instance.
    -   domain name of the mount point: when you create a mount point for a file system, a mount address is generated. You must enter the mount address to mount the file system. For more information, see [Manage mount points](../../../../intl.en-US/Console User Guide/Manage mount points.md#).
    -   myshare: indicates the name of an SMB share. However, this name cannot be changed.
    **Note:** 

    Ensure that the name of the target mount drive is unique on the target instance.

3.  Run `net use` command to view the mounted file system.

    If the command output contains the following information, the mount is successful.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18691/156272428951150_en-US.png)


