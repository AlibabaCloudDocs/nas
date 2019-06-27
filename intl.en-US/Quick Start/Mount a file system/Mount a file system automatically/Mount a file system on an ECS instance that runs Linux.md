# Mount a file system on an ECS instance that runs Linux {#concept_xmg_1kk_2fb .concept}

You can modify either one of the following configuration files on an ECS instance to automatically mount a NAS file system when the instance is restarted.

To enable a file system to be mounted automatically on an ECS instance that runs Linux, you can modify either the /etc/fstab file or the /etc/rc.local file.

## Modify the /etc/fstab file \(recommended\) {#section_czd_wmk_2fb .section}

After you connect to an ECS instance for the first time, add the following command to the /etc/fstab file.

``` {#codeblock_9pv_ygq_wop}
fid-xxxx.cn-hangzhou.nas.aliyuncs.com:/ /mnt  nfs vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
```

The parameters used in the command are described as follows:

|Parameter|Description|
|---------|-----------|
|**\_netdev**|Prevents a file system from mounting on an ECS instance before a network connection is established.|
|**0**\(the first zero after noresvport\)|Non-zero values indicate that a file system must be backed up by dump. For a NAS file system, the value of the parameter is 0.|
|**0** \(the second zero after noresvport\)|This value indicates the order in which fsck checks available file systems when an ECS instance is started. For a NAS file system, the value of the parameter is 0. It indicates that fsck is not allowed to run when an instance is started.|

## Modify the /etc/rc.local file {#section_k4v_ynk_2fb .section}

After you connect to an ECS instance for the first time, add the following command to the /etc/rc.local file.

Take an NFSv4 file system as an example. Add the following command.

``` {#codeblock_d35_uua_ubu}
sudo mount -t nfs -o vers=4.0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport fid-xxxx.cn-hangzhou.nas.aliyuncs.com:/ /mnt
```

**Note:** 

-   In this command, fid-xxxx.cn-hangzhou.nas.aliyuncs.com is the domain name of the mount point. For more information about the mount command, see [Mount an NFS file system in Linux](reseller.en-US/Quick Start/Mount a file system/Mount a NFS file system/Mount an NFS file system in Linux.md#).
-   Before you modify the /etc/rc.local file, ensure that you have the execute permission to run the/etc/rc.local file and the /etc/rc.d/rc.local file.

## Mount a NAS Extreme file system on an ECS instance {#section_gsl_kkp_hhb .section}

1.  Modify the /etc/systemd/system/sockets.target.wants/rpcbind.socket file, move IPv6-related rpcbind parameters to comments. Otherwise, the rpcbind service fails to automatically start up. The details are shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21506/156162900943322_en-US.png)

2.  After you connect to an ECS instance for the first time, add the following command to the /etc/fstab file.

    ``` {#codeblock_ef7_a18_a0a}
    xxxx:/share /tmp/benchmark   nfs vers=3,proto=tcp,noresvport,_netdev 0 0
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21506/156162900943323_en-US.png)


