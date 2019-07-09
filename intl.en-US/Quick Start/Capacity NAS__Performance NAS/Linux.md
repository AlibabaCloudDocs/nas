# Linux {#concept_27526_zh .task}

## Step 1: Create a file system {#section_4pf_qbn_yze .section}

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
    |Protocol Type| You can select **NFS \(including NFSv3 and NFSv4\)**.

 NFS is recommended in Linux and SMB is recommended in Windows.

 |
    |Zone| Zones are physical areas with independent power grids and networks within one region.

 Click the drop-down box to select the zone. we recommend that you select the zone of the ECS instance where you want to mount your file system.

**Note:** A file system or computing node in a zone can communicate with a file system or computing node in a different zone but of the same region.

 |

4.  Click **OK**.

## Step 2: Add a mount point {#section_trw_n4i_5na .section}

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
        -   For a classic network mount point, no default permission group is provided. When using this for the first time, you must go to the Permission Group page to create a permission group in a classic network, and add rules for the permission group. For more information, see [Manage the data access permissions of a file system](../../../../intl.en-US/User Guide/Manage the data access permissions of a file system.md#).
        -   When adding a mount point in a classic network for the first time, you are requested to authorize NAS through RAM to access the query interface of your ECS instance. Follow the instructions to complete the authorization, then try creating the mount point in the classic network again. For more information, see [Why do I need RAM permissions to create a mount point in a classic network](../../../../intl.en-US/FAQ/FAQs/Why do I need RAM permissions to create a mount point in a classic network.md#).
 |

5.  Click **OK**.

## Step 3: Install an NFS client in Linux {#section_xox_mq9_8jn .section}

To mount a NAS NFS file system to an ECS instance in Linux, you must install an NFS client.

1.  Log on to [ECS console](https://ecs.console.aliyun.com/)。
2.  Run either of the following commands to install an NFS client.
    -   If you use the CentOS , Redhat or Aliyun Linux run the following command:

        ``` {#codeblock_t2k_hd7_fs8}
        sudo yum install nfs-utils
        ```

    -   If you use the Ubuntu or Debian system, run the following commands:

        ``` {#codeblock_9t8_ixc_izu}
        sudo apt-get update
        ```

        ``` {#codeblock_yqd_rns_k56}
        sudo apt-get install nfs-common
        ```

3.  Run the following command to view the number of NFS requests that are initiated simultaneously.

    ``` {#codeblock_w2s_itt_xbs}
    cat /proc/sys/sunrpc/tcp_slot_table_entries
    ```

    **Note:** 

    The number of NFS requests that are initiated simultaneously is controlled by the NFS client in Linux. If the parameter is set to a small value, the I/O performance of the system reduces. The maximum value of the parameter is 256 in the default kernel. For better I/O performance, you can run the following commands as the root user to set the parameter to a larger value. After modifying the parameter, restart the system.

    ``` {#codeblock_8dw_dq0_ssr}
    echo "options sunrpc tcp_slot_table_entries=128" >> /etc/modprobe.d/sunrpc.conf
    echo "options sunrpc tcp_max_slot_table_entries=128" >>  /etc/modprobe.d/sunrpc.conf
    sysctl -w sunrpc.tcp_slot_table_entries=128
    ```


## Step 4: Mount an NFS file system in Linux {#section_7h6_39t_tbm .section}

When you mount a NAS NFS file system to an ECS instance, you can use the DNS name of the file system or the target to which you want to mount the file system. The DNS name of the file system is automatically resolved to the IP address of the mount target in the available zone of the mounted ECS instance.

1.  Log on to [ECS console](https://ecs.console.aliyun.com/)。
2.  You can run either of the following commands to mount an NFS file system.

    -   To mount an NFSv4 file system, run the following command:

        ``` {#codeblock_plg_qd1_rdw}
        sudo mount -t nfs -o vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
        							
        ```

        If you fail to mount the file system, run the following command:

        ``` {#codeblock_1ey_py0_z2t}
        sudo mount -t nfs4 -o rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
        							
        ```

    -   To mount an NFSv3 file system, run the following command:

        ``` {#codeblock_vw4_7ux_pb8}
        sudo mount -t nfs -o vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
        ```

    The following table describes the parameters used in the mounting command.

    |Parameter|Description|
    |:--------|:----------|
    |mount point| The mount point includes the mount point domain name and the mount point path.

    -   Mount point domain name: this parameter is automatically generated when you create a file system and does not need to be set manually.
    -   Mount point path: which can be the root directory "/" or any sub-directory in the NAS file system.
 |
    |vers|Indicates the file system version. Only NFSv3 and NFSv4 are supported.|
    |option| You can specify multiple options when mounting a NAS file system. For more information, see [Mount option description table](intl.en-US/Quick Start/Mount a file system/Mount an NFS file system in Linux.md#table_2uc_odz_vk9) on the [Mount an NFS file system in Linux](intl.en-US/Quick Start/Mount a file system/Mount an NFS file system in Linux.md#).

 |

3.  Run `mount -l` command to view the mounted file system.

    If the command output contains the following information, the mount is successful.

    ![](images/49539_en-US.png)

    After the mounting succeeds, you can also run `df -h` command to view the capacity information about the mounted file system.


