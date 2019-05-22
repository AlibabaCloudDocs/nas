# Mount an SMB file system {#concept_zb5_1rh_cfb .concept}

You can mount an SMB file system on an ECS instance that runs Windows.

## Prerequisites {#section_zlq_3j1_dfb .section}

Before mounting an SMB file system on an ECS instance that runs Windows, ensure that the following services are started in Windows:

-   Workstation

    Choose **All Programs** \> **Accessories** \> **Run**, or press`Win+R` and enter `services.msc` to open the Services console. Locate the Workstation service and check the status. The Workstation service is started by default.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/155850442942055_en-US.png)

-   TCP/IP NetBIOS Helper

    Use the following steps to start the TCP/IP NetBIOS Helper service:

    1.  Open **Network and Sharing Center** and click the active network connection.
    2.  Click **Properties** to open the Local Area Network Properties dialog box. Double-click **Internet Protocol Version 4 \(TCP/IPv4\)** to open the Internet Protocol Version 4 \(TCP/IPv4\) Properties dialog box, and then click **Advanced**.
    3.  In the Advanced TCP/IP Settings dialog box, choose **WINS** \> **Enable NetBIOS over TCP/IP**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/155850442942056_en-US.png)


## Mount a file system using a command {#section_pgk_srh_cfb .section}

You can run the following command to mount an SMB file system.

```
net use <the target mount drive> \\<the mount address of a mount point>\myshare
```

-   The target mount drive indicates the mount drive of the target Windows instance. In this command, you must add a space before \\\\ and another space before <the target mount drive\>.

    **Note:** Ensure that the name of the target mount drive is unique on the target instance.

-   When you create a mount point for a file system, a mount address is generated. You must enter the mount address to mount the file system.

    For more information, see [Add a mount point](reseller.en-US/Quick Start/Add a mount point.md#).

-   myshare: indicates the name of an SMB share. However, this name cannot be changed.

**Note:** When a network connection is established between NAS and the Windows instance, you can mount an SMB file system on the instance. For more information, see [Precautions before mounting a file system](reseller.en-US/Quick Start/Mount a file system/Considerations before mounting a file system.md#).

## Examples {#section_dyj_bsh_cfb .section}

For example, to mount an SMB file system on drive Z, you can run the following command.

```
 net use z: \\file-system-id-xxxx.region.nas.aliyuncs.com\myshare
				
```

## View mount information {#section_ypf_4sh_cfb .section}

After mounting an SMB file system, you can run the following command in Windows command prompt to view the mounted file system.

```
net use
```

