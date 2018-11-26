# Configure automatic mounting in Linux {#concept_xmg_1kk_2fb .concept}

You can modify the configuration file of an ECS instance to automatically mount a NAS file system to the ECS instance when the instance is restarted.

You can configure automatic mounting in Linux by using the following two methods:

## Configure the /etc/fstab file \(recommended\) {#section_czd_wmk_2fb .section}

After connecting to an ECS instance for the first time, add the following command to the /etc/fstab configuration file of the instance:

```
fid-xxxx.cn-hangzhou.nas.aliyuncs.com:/ /mnt  nfs4 vers=4.0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
```

The following table describes the parameters in the command.

|Parameter|Description|
|---------|-----------|
|**\_netdev**|Prevents the client from mounting a file system before the network is ready.|
|**0**\(the first value after noresvport\)|If the value is not 0, it indicates that the file system is backed up by dump. This value is 0 for NAS file systems.|
|**0** \(the second value after noresvport\)|Indicates the order in which fsck checks the file system when the ECS instance is started. This value should be 0 for NAS file systems, meaning that fsck does not check the file system when the ECS instance is started.|

## Configure the /etc/rc.local file {#section_k4v_ynk_2fb .section}

After connecting to an ECS instance for the first time, add a mounting command to the /etc/rc.local configuration file of the instance.

For example, if you want to automatically mount an NFSv4 file system, add the following command:

```
sudo mount -t nfs -o vers=4.0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport fid-xxxx.cn-hangzhou.nas.aliyuncs.com:/ /mnt
```

**Note:** 

-   In the command, fid-xxxx.cn-hangzhou.nas.aliyuncs.com is the domain name of the mount point. For more information about mounting commands, see [Mount an NFS file system in Linux](reseller.en-US/Quick Start/Mount a file system/Mount a NFS file system/Mount an NFS file system in Linux.md#).
-   Before configuring the /etc/rc.local file, ensure that you have execution access to the /etc/rc.local file and the /etc/rc.d/rc.local file.

