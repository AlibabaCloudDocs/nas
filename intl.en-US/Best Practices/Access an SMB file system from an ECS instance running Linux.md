# Access an SMB file system from an ECS instance running Linux {#task_1580275 .task}

This topic describes how to mount an SMB file system on an ECS instance running Linux and perform read/write operations on the file system.

-   At least one ECS instance is available in the region where you need to create a file system.

    In this topic, unless otherwise specified, any Linux mentioned refers to one of the following Linux versions supported by an SMB file system:

    -   CentOS 7.6 64-bit \(3.10.0-957.5.1.el7.x86\_64\)
    -   Ubuntu 18.04 64-bit \(4.15.0-48-generic\)
    -   Debian 9.9 64-bit \(4.9.0-9-amd64\)
    -   Suse Enterprise Server 12 SP2 64-bit \(4.4.74-92.35-default\)
    -   OpenSUSE 42.3 64-bit \(4.4.90-28-default\)
    -   Aliyun Linux \(4.19.34-11.al7.x86\_64\)
    -   CoreOS \(4.19.43-coreos VersionID=2079.4.0\)
    **Note:** When you are using an earlier version of Linux, defects that exist in the SMB module of the Linux kernel will be exposed in specific scenarios. If you use an unsupported version of Linux, Alibaba Cloud cannot ensure the reliability of an SMB file system.

-   Networks
    -   The target ECS instance running Linux on which you need to mount an SMB file system must reside in the same network as that of the SMB file system. For example, when an ECS instance and an SMB file system reside in the same VPC, you can mount the SMB file system on the ECS instance.
    -   Check the whitelist of a file system to ensure that the ECS instance is authorized to access the SMB file system.
    -   Ensure that port 445 is enabled. TCP port 445 is used for SMB to communicate with SMB clients.

        If port 445 is disabled, we recommend that you add rules regarding port 445 to the security group of the target ECS instance. For more information, see [Add security group rules](../../../../../reseller.en-US/Security/Security groups/Add security group rules.md#).

-   You have created an SMB file system. For more information, see [Create file systems](../reseller.en-US/Console User Guide/Manage file systems.md#section_5jo_0kj_jn5).
-   You have created a mount point. For more information, see [Create a mount point](../reseller.en-US/Console User Guide/Manage mount points.md#section_6xi_a3u_zkq).
-   Software requirements

    The SMB kernel module is pre-installed on each supported Linux distribution. However, you still need to install the cifs-utils package.

    -   If you are using Ubuntu or Debian, you can use the apt-get tool to install the cifs-utils package.

        ``` {#codeblock_c8u_ftu_es6}
        sudo apt-get update
        ```

        ``` {#codeblock_rup_brf_b4w}
        sudo apt-get install cifs-utils
        ```

    -   If you are using RHEL, CentOS, or Aliyun Linux, you can use the yum tool to install the cifs-utils package.

        ``` {#codeblock_gky_h2e_tru}
        sudo yum install nfs-utils
        ```

    -   If you are using OpenSUSE or SLES12-SP2, you can use the zypper or yast tool to install the cifs-utils package.

        ``` {#codeblock_hhe_4l0_iys}
        sudo zypper install cifs-utils
        ```

        ``` {#codeblock_nrd_vqh_i04}
        Run the sudo yast2 command, choose Software > Software Management, and then install the cifs-utils package.
        ```

    -   If you are using a supported CoreOS distribution, you can perform the following steps to install the cifs-utils package:
        1.  Configure SELinux settings

            ``` {#codeblock_jeh_t1b_bne}
            sed -i 's/SELINUXTYPE=mcs/SELINUXTYPE=targeted/' /etc/selinux/config
            ```

        2.  Compile and install the cifs-utils package on CoreOS

            You can use the following command to run a Fedora-based Docker container to compile and install the cifs-utils package. You can also download the cifs-utils package from the Alibaba Cloud official site and copy the package to the /tmp or /bin folder.

            ``` {#codeblock_c06_e3c_u73}
            $ docker run -t -i -v /tmp:/cifs fedora /bin/bash
            
            fedora # yum groupinstall -y "Development Tools" "Development Libraries"
            
            fedora # yum install -y bzip2
            
            fedora # curl https://download.samba.org/pub/linux-cifs/cifs-utils/cifs-utils-
            
            6.9.tar.bz2 --output cifs-utils-6.9.tar.bz2;
            
            fedora # bunzip cifs-utils-6.9.tar.bz2; && tar xvf cifs-utils-6.9.tar
            
            fedora # cd cifs-utils-6.9; ./configure && make
            
            fedora # cp mount.cifs /cifs/
            
            fedora # exit
            ```


## Mount a file system {#section_9sq_p2c_vtp .section}

1.  Log on to an ECS instance running Linux by using a root user account or a client administrator user account authorized by using the sudo command.
2.  Run the following command to mount a file system. 

    ``` {#codeblock_en5_7p9_l8v}
    mount -t cifs //xxx-crf23.eu-west-1.nas.aliyuncs.com/myshare /mnt -o vers=2.1,guest,uid=0,gid=0,dir_mode=0755,file_mode=0755,mfsymlinks,cache=strict,rsize=1048576,wsize=1048576
    ```

    The format of a mount command: mount -t cifs //<the domain name of a mount point\>/myshare <a mount directory\> -o <mount options\>

    |Parameter|Description|
    |---------|-----------|
    |File system type|For an SMB file system, you must specify -t cifs.|
    |Domain name of a mount point|When you create a mount point for a file system, the domain name of the mount point is generated. You must replace the domain name based on your requirements. For more information about mount points, see [Manage mount points](Manage mount points../DNnas1882233/EN-US_TP_18694.dita#task_27531_zh).|
    |myshare|The name of an SMB share. You cannot change the name.|
    |Mount directory|The target mount directory, such as /mnt/sharepath.|
    |Mount option|You can use the -o switch to specify mount options.     -   \(Required\) vers: specifies the version of the SMB protocol. You can specify 2.1 or 3.0 for the parameter.
    -   \(Required\) guest: specifies a user account that you use to mount a file system. You can only use a guest user account that can be authenticated by NT LAN Manager \(NTLM\) to mount a file system. You can specify one of the following statements for the parameter: username=guest, password=guest, or guest.

**Note:** The NTLM, NTLMv2, and NTLMSSP protocols are applicable. If you leave this parameter blank, an SMB client will negotiate with NAS to use an acceptable NTLM protocol to mount a file system. You can also specify the required value, such as ntlm, ntlmv2, or ntlmssp, for the sec parameter when mounting a file system.

    -   \(Optional\) uid: specifies the owner of the files stored on the file system after a successful mount. The default value of uid is 0.
    -   \(Optional\) gid: specifies the user group of the files stored on the file system after a successful mount. The default value of gid is 0.
    -   \(Optional\) dir\_mode: specifies the permissions for a directory that you grant to the directory owner. The permissions include read, write, and execute. The value must start with a 0, such as 0755 and 0644. The default value of dir\_mode is 0755.
    -   \(Optional\) file\_mode: specifies the permissions for a file that you can grant to the file owner. The permissions include read, write, and execute. The value must start with a 0, such as 0755 and 0644. The default value of file\_mode is 0755.
    -   \(Optional\) mfsymlinks: specifies whether symbol links are supported.
    -   \(Optional\) cache:
        -   If the cache parameter is set to strict, it indicates that a cache is enabled on an SMB client. The cache parameter is set to strict by default.
        -   If the cache parameter is set to none, it indicates that a cache is disabled on an SMB client.
    -   \(Optional\) rsize: specifies the maximum number of bytes of data that the NFS client can receive for each network read request. The default value is 1048576.
    -   \(Optional\) wsize: indicates the maximum number of bytes of data that the NFS client can send for each network write request. The default value is 1048576.
    -   \(Optional\) atime|relatime: If your businesses are not sensitive to access time for files, we do not recommend that you use the atime option. The default option is relatime.
 **Note:** 

    -   The authorized administrator of the Linux ECS instance has full access to the SMB file system.
    -   You can use the `mount | grep cifs` command to retrieve a list of available mount points and the details of each mount point.
    -   If you are using an unsupported Linux distribution, we recommend that the kernel version of the distribution must be later than 3.10.0-514. If the kernel version of the distribution is earlier than or equal to 3.7, you must specify the cache=strict statement in the mount command when mounting a file system. You can use the `uname -a` command to view the kernel version.
 |

3.  You can use the `mount -l` command to verify mount results. 

    The following figure shows an example of a successful mount.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253385/156654604154720_en-US.png)

4.  After you mount a file system, you can perform read/write operations on the NAS file system from the Linux ECS instance. 

    You can access the NAS file system in the same way you access a normal directory. The following figure shows a code example.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18690/156654604154347_en-US.png)


## Scenarios {#section_6xk_1hd_bzj .section}

You can apply different mount options to different scenarios. This section describes typical scenarios and corresponding mount options.

-   Shared access to a file system from multiple Linux ECS instances

    Multiple ECS instances running Linux share access to a file system but without access control requirements. You can use an authorized administrator account of each ECS instance to mount a file system on these ECS instances. An example mount command is as follows.

    ``` {#codeblock_bbm_mfx_4i6}
     mount -t cifs //smbfs.hangzhou-g.aliyun.com/myshare /mnt/sharepath -o vers=2.1,guest,mfsymlinks
    ```

-   Shared access to a file system from multiple Linux ECS instances with different access permissions

    Multiple ECS instances running Linux share access to a file system with access control requirements. You can configure the uid, gid, dir\_mode, and file\_mode parameters in the mount command to meet these requirements.

-   Shared access to a file system from multiple Linux ECS instances implemented as Web servers

    You can install Web server applications such as Apache on multiple Linux ECS instances and use an SMB file system as shared file storage.

    **Note:** 

    -   The benefits of an SMB file system are shared-access, scalability, and high availability. In several scenarios such as accessing a large number of small files on an SMB file system, the performance of the SMB file system may be slightly compromised. This occurs because the implementation scheme of physical disks is different from that of an SMB file system. For Web server scenarios, we recommend that you store shared files on an SMB file system and exclusive files on local disks to achieve high performance.
    -   Web server applications require high bandwidth for communication. A Web server acceleration feature is designed for these applications. You can contact Alibaba Cloud Technical Support to enable the feature.
-   Shared access to a file system from both Windows ECS instances and Linux ECS instances

    For example, you may require shared access to an SMB file system from both Windows ECS instances and Linux ECS instances at the same time. In this scenario, you must specify the cache=strict statement or use the default value of cache in the mount command when mounting a file system on a Linux ECS instance.


If any issue occurs when you mount a file system, see [Troubleshoot issues when you access an SMB file system from an ECS instance running Linux](../reseller.en-US/FAQ/SMB FAQ/Troubleshoot issues when you access an SMB file system from an ECS instance running Linux.md#).

