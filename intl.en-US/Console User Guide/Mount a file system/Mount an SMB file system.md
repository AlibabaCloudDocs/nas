# Mount an SMB file system {#concept_zb5_1rh_cfb .task}

This topic describes how to mount an SMB file system in Windows.

## Prerequisites {#section_zlq_3j1_dfb .section}

1.  You have created a file system. For more information, see [Create file systems](reseller.en-US/Console User Guide/Manage file systems.md#section_5jo_0kj_jn5).
2.  You have created a mount point. For more information, see [Create a mount point](reseller.en-US/Console User Guide/Manage mount points.md#section_6xi_a3u_zkq).
3.  Ensure that the following Windows services are started:
    -   Workstation
        1.  Choose **All Programs** \> **Accessories** \> **Run**, or press `Win+R` and enter `services.msc` to open the Services console.
        2.  Locate the Workstation service and ensure that the status of the service is **Started**.

            The Workstation service is started by default.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156507788842055_en-US.png)

    -   TCP/IP NetBIOS Helper

        Perform the following steps to start the TCP/IP NetBIOS Helper service:

        1.  Open **Network and Sharing Center** and click the active network connection.
        2.  Click **Properties** to open the Local Area Network Properties dialog box. Double-click **Internet Protocol Version 4 \(TCP/IPv4\)** to open the Internet Protocol Version 4 \(TCP/IPv4\) Properties dialog box, and then click **Advanced**.
        3.  In the Advanced TCP/IP Settings dialog box, choose **WINS** \> **Enable NetBIOS over TCP/IP**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156507788842056_en-US.png)

        4.  Choose **All Programs** \> **Accessories** \> **Run**, or press `Win+R` and enter `services.msc` to open the Services console.
        5.  Locate the TCP/IP NetBIOS Helper service and ensure that the status of the service is **Started**.

            The TCP/IP NetBIOS Helper service is started by default.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156507788954417_en-US.png)


## Procedure {#section_pgk_srh_cfb .section}

Perform the following steps to mount an SMB file system.

1.  Log on to the [ECS console](partners-intl.console.aliyun.com/#/ecs).
2.  Open the command prompt and run the following command to mount the file system.

    ``` {#codeblock_qt9_gik_x61}
    net use D: \\file-system-id.region.nas.aliyuncs.com\myshare
    ```

    The format of the command used to mount the file system is `net use <the drive of the mount target> \\<the domain name of a mount point>\myshare`.

    -   The drive of the mount target: the target drive on which you need to mount a file system.
    -   The domain name of a mount point: the domain name generated when you create the mount point for a file system. For more information, see [Create a mount point](reseller.en-US/Quick Start/NAS Capacity and NAS Performance/Mount a file system on an ECS instance running Windows.md#).
    -   myshare: indicates the name of an SMB share. You cannot change the name.
    **Note:** 

    Ensure that the name of the target mount drive is unique on the target ECS instance.

    For more information about how to troubleshoot the errors that occur while the mount command is running, see [Causes and solutions of SMB mount failures](../reseller.en-US/FAQ/SMB FAQ/Causes and solutions of SMB mount failures.md#).

3.  Use the `net use` command to view the results.

    An example of a successful mount is shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156507788949545_en-US.png)


