# Enable an automatic mount at startup for an NFS file system {#task_xmg_1kk_2fb .task}

This topic describes how to modify Linux configuration files to allow an NFS file system to be automatically mounted at startup.

1.  You have created a file system. For more information, see [Create file systems](reseller.en-US/Console User Guide/Manage file systems.md#section_5jo_0kj_jn5).
2.  You have created a mount point. For more information, see [Create a mount point](reseller.en-US/Console User Guide/Manage mount points.md#section_6xi_a3u_zkq).
3.  You have installed an NFS client. For more information, see [Install an NFS client](reseller.en-US/Console User Guide/Mount a file system/Mount an NFS file system.md#section_kvj_d02_szj).

## Prerequisites {#section_s5p_3m3_0zz .section}

We recommend that you configure the /etc/fstab file to enable an NFS file system to be automatically mounted at startup. You can also configure the /etc/rc.local file to set an automatic mount.

1.  Log on to the [ECS console](partners-intl.console.aliyun.com/#/ecs).
2.  Configure an automatic mount.
    -   \(Recommended\) Open the /etc/fstab file and add the following command.

        **Note:** If you configure an automatic mount on CentOS 6.x, use the `chkconfg netfs on` command to enable the netfs service to run at startup.

        -   If you need to mount an NFSv4-compliant file system, add the following command.

            ``` {#codeblock_h4f_oyv_rqa}
            file-system-id.region.nas.aliyuncs.com:/ /mnt nfs vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
            ```

        -   If you need to mount an NFSv3-compliant file system, add the following command.

            ``` {#codeblock_8c4_lp7_3qy}
            file-system-id.region.nas.aliyuncs.com:/ /mnt nfs vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
            ```

    -   Open the /etc/rc.local configuration file and add the mount command.

        **Note:** 

        Before configuring the /etc/rc.local file, ensure that you have execute permissions on the /etc/rc.local and /etc/rc.d/rc.local files. For example, on CentOS 7.x, no execute permission is granted to a user by default. You must assign the execute permission to a user before configuring the /etc/rc.local file.

        -   If you need to mount an NFSv4-compliant file system, add the following command.

            ``` {#codeblock_3n0_a3u_f6q}
            sudo mount -t nfs -o vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
            ```

        -   If you need to mount an NFSv3-compliant file system, add the following command.

            ``` {#codeblock_ycw_chq_glo}
            sudo mount -t nfs -o vers=3,nolock,proto=tcp, rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport file-system-id-xxxx.region.nas.aliyuncs.com:/ /mount-point
            ```

        The parameters used in the command are described in the following table.

        |Parameter|Description|
        |---------|-----------|
        |Mount Point| A mount point consists of a domain name and path.

        -   The domain name of a mount point is generated when you create the mount point. You do not need to manually configure the name of a mount point.
        -   The path of a mount point indicates the target mount address. The path can be the root directory \(/\) or a subfolder such as /mnt in Linux.
 |
        |\_netdev|Prevents a file system from mounting on an ECS instance before a network connection is established.|
        |0 \(the first zero after noresvport\)|Non-zero values indicate that a file system must be backed up by using dump. For a NAS file system, the value of the parameter is 0.|
        |0 \(the second zero after noresvport\)|This value indicates the order in which fsck checks available file systems at startup. For a NAS file system, the value of the parameter is 0. It indicates that fsck is not allowed to run at startup.|

        When you mount a file system, multiple parameters are available. Separate these parameters with commas \(,\). We recommend the following values for mount parameters.

        |Parameter|Description|
        |:--------|:----------|
        |**rsize**|You can set the maximum number of bytes of data that the NFS client can receive for each network read request. Recommended value: 1048576|
        |**wsize**|You can set the maximum number of bytes of data that the NFS client can send for each network write request. Recommended value: 1048576|
        |**hard**|Indicates that applications stop access to a file system when the file system is unavailable, and wait until the file system is available. We recommended that you use the hard parameter.|
        |**timeo**|You can set the timeout value that the NFS client uses to wait for a response before it retries an NFS request. Unit: deciseconds. Recommended value: 600.|
        |**retrans**|You can set the number of times the NFS client retries a request. Recommended value: 2|
        |**noresvport**|Indicates that the NFS client uses a new TCP source port when a network connection is re-established to ensure data integrity. We recommend that you use the noresvport parameter.|

        **Note:** If you do not use the preceding values, you must consider the following issues:

        -   We recommend that you specify a maximum value of 1048576 for both the rsize parameter and the wsize parameter to avoid diminished performance.
        -   If you must modify the timeo parameter, we recommend that you specify a minimum of 150 for the parameter. The unit of the timeo parameter is decisecond, which is 0.1 second. For example, a value of 150 indicates 15 seconds.
        -   We recommend that you do not use the soft parameter to avoid data inconsistencies. You must use the soft parameter with careful consideration.
        -   We recommend that you use the default setting for other mount parameters. For example, changing read or write buffer sizes or disabling attribute caching can result in reduced performance.
3.  Run the `reboot` command to restart the ECS instance.
4.  Use the `mount -l` command to view the mount results.

    An example of a successful mount is shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21207/156473953149539_en-US.png)

    After a file system is mounted, you can use the `df -h` command to view the capacity of the file system.


