# Mount an NFS file system {#concept_hpp_dkh_cfb .concept}

This topic describes how to install an NFS client in Linux and use the mount command to mount an NFS file system.

## Prerequisites {#section_b22_6c8_4of .section}

1.  You have created a file system. For more information, see [Create file systems](intl.en-US/Console User Guide/Manage file systems.md#section_5jo_0kj_jn5).
2.  You have created a mount point. For more information, see [Create a mount point](intl.en-US/Console User Guide/Manage mount points.md#section_6xi_a3u_zkq).

## Step 1: Install an NFS client {#section_kvj_d02_szj .section}

In Linux, you must install an NFS client before mounting an NFS file system on an ECS instance.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
2.  Use the following command to install an NFS client.
    -   If CentOS, RHEL, or Aliyun Linux is running on the ECS instance, run the following command.

        ``` {#codeblock_hvf_5xm_593}
        sudo yum install nfs-utils
        ```

    -   If Ubuntu or Debian is running on the ECS instance, run the following commands.

        ``` {#codeblock_znv_ibv_dd4}
        sudo apt-get update
        ```

        ``` {#codeblock_pcb_rj6_uao}
        sudo apt-get install nfs-common
        ```

3.  Modify the maximum number of concurrent NFS requests. For more information, see [How can I modify the maximum number of concurrent NFS requests?](../intl.en-US/FAQ/FAQs/How can I modify the maximum number of concurrent NFS requests?.md#).

    The maximum number of concurrent requests from an NFS client is limited to 2, which reduces NFS performance.


## Step 2: Mount an NFS file system {#section_spc_nlh_cfb .section}

You can use the domain name of the file system or the domain name of the mount target to mount the NFS file system on an ECS instance. The domain name of the file system is resolved to the IP address of the mount target in a zone where the ECS instance is located.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
2.  Mount the NFS file system.

    -   If you need to mount an NFSv4-compliant file system, use the following command.

        ``` {#codeblock_4bv_6vg_5y0}
        sudo mount -t nfs -o vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
        							
        ```

        If you fail to mount the file system, run the following command.

        ``` {#codeblock_6i1_370_3ch}
        sudo mount -t nfs4 -o rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
        							
        ```

    -   If you need to mount an NFSv3-compliant system, run the following command.

        ``` {#codeblock_kxf_3pr_1c5}
        sudo mount -t nfs -o vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
        ```

    The parameters used in the command are described in the following table.

    |Parameter|Description|
    |:--------|:----------|
    |**Mount point**| A mount point consists of a domain name and path.

    -   The domain name of a mount point is generated when you create the mount point. You do not need to manually configure the name of a mount point.
    -   The path of a mount point indicates the target mount address. The path can be the root directory \(/\) or a subfolder such as /mnt in Linux.
 |
    |**vers**|The version of the file system. Only NFSv3 and NFSv4 are applicable.|

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
3.  Use the `mount -l` command to view the mount results.

    An example of a successful mount is shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21207/156438399649539_en-US.png)

    After a file system is mounted, you can use the `df -h` command to view the capacity of the file system.


