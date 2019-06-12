# Causes and solutions of SMB mount failures {#concept_fpq_xwf_2hb .concept}

When you mount an SMB file system on an ECS instance that runs Windows, a mount failure may occur due to one of the following errors. This topic describes the causes and solutions of mount failures.

## System error 53 {#section_kkp_c4t_s32 .section}

**Description**

The network path was not found.

**Cause**

The network connection fails.

**Solution**

You can check the network connection as follows:

1.  Use the following ping command to check whether you can access the IP address of a mount point and ensure that the latency is within the expected range.

    ping <the IP address of a mount point\>

    -   If you can ping the IP address, go to [Step 2](#li_c2c_vh8_ugj).
    -   If you fail to ping the IP address, perform the following steps:
        -   Check whether the mount command is valid. For example, no redundant or missing forward slash `/`, backslash `\`, space, and myshare exists.

            The following provides the valid format of a mount command.

            ``` {#codeblock_at9_yzk_jn6}
            net use <the target drive> \\<the IP address of a mount point>\myshare
            ```

            Example:

            ``` {#codeblock_asi_1za_86c}
            net use z: \\xxxx.cn-hangzhou.nas.aliyuncs.com\myshare 
            ```

        -   Ensure that the protocol type of a file system is SMB.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/149028/156032096041401_en-US.png)

        -   Ensure that the IP address of the mount point is valid.
        -   Ensure that the ECS instance and the mount point are located in the same VPC.
        -   Ensure the network configuration is valid. We recommend that you check the network configuration if the ECS instance and the mount point are located in different VPCs. We also recommend that you check the network configuration if the ECS instance is connect to the VPC by using a VPN.
2.  Use the following telnet command to check whether the SMB file system is available.

    telnet <the IP address of a mount point\> 445


## System error 58 {#section_hc3_y35_loh .section}

**Description**

The specified server cannot perform the requested operation.

**Cause**

The SMB protocol version used on the ECS instance is not compatible with the version used by the file system.

**Solution**

Ensure that the ECS instance runs Windows Server 2008 R2 or later, excluding Windows Server 2008.

## System error 64 {#section_3fa_9qy_l9f .section}

**Description**

The specified network name is no longer available.

**Cause**

-   The IP address of the target ECS instance is not specified in any NAS permission group that is bound to the file system.
-   The NAS service is overdue.
-   The ECS instance and the NAS file system are located in classic networks, but they are created by different Alibaba Cloud accounts.
-   The protocol type of a file system is not SMB.

**Solution**

This issue occurs when you do not have permission to access NAS file system resources. You can troubleshoot the issue as follows:

1.  Ensure that the private IP address or the VPC IP address of the ECS instance is specified in a permission group that is bound to the file system.
2.  Confirm that the balance of the Alibaba Cloud account is positive.
3.  Ensure that the ECS instance and the NAS file system are created by the same Alibaba Cloud account if they are located in classic networks.
4.  Ensure that the protocol type of a file system is SMB.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/149028/156032096041401_en-US.png)


## System error 67 {#section_2xt_2ks_so0 .section}

**Description**

The network name cannot be found.

**Cause**

Several important network services are not started.

**Solution**

Start the following services. For more information, see [Mount an SMB file system](../../../../intl.en-US/Quick Start/Mount a file system/Mount an SMB file system.md#section_zlq_3j1_dfb).

1.  Workstation
2.  TCP/IP NetBIOS Helper

## System error 85 {#section_dsx_7nn_yn0 .section}

**Description**

The local device name is already in use.

**Cause**

The target drive letter is already in use.

**Solution**

You must change the target drive letter and re-mount the file system.

## System error 1272 {#section_pwi_i6q_rqy .section}

**Description**

Error message: You can't access this shared folder because your organization's security policies block unauthenticated guest access. These policies can help protect your computer from threats from insecure or malicious devices on the network.

**Cause**

Due to security policies, Windows denies access to an SMB file system from Guest users.

**Solution**

If the ECS instance runs a version later than Windows Server 2016 \(excluding Windows Server 2016\), modify the following registry key to allow access from Guest users.

``` {#codeblock_ju0_36o_rzr}
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters]
"AllowInsecureGuestAuth"=dword:1
```

For more information, see [Guest access in SMB2 disabled by default in Windows](https://support.microsoft.com/en-us/help/4046019/guest-access-in-smb2-disabled-by-default-in-windows-10-and-windows-ser).

