# How to prevent NFS 4.0 from being mistaken for a Trojan attack {#concept_65281_zh .concept}

## Symptom {#section_x2t_3bh_hfb .section}

After NFS 4.0 is mounted to a NAS, NFS 4.0 listens to a random 0.0.0.0 port. Netstat is unable to identify the process that listens to this port.

The changing listened port and the unidentified listening program make NFS 4.0 may be mistaken for a Trojan attack.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18748/153959009513103_en-US.jpg)

## Cause { .section}

NFS 4.0 listens to this random port to support callback. NFS 4.0 listens to this random port to support callback. Because the default value of the fs.nfs.nfs\_callback\_tcpport kernel parameter is 0, the NFS 4.0 client randomly chooses a port to listen. This random port does not constitute a security risk.

To facilitate port management, see Solution to fix the callback port.

## Solution { .section}

Before mounting the file system, set the parameter fs.nfs.nfs\_callback\_tcpport to a non-zero value.

```
sudo sysctl fs.nfs.nfs_callback_tcpport=<port>

```

In the following example, the fs.nfs.nfs\_callback\_tcpport parameter is manually set to port 45450, and then NFS 4.0 is mounted. Netstat shows that the listened port is 45450.

Note that the following commands are run as user root, so running the `sysctl` command in `sudo` is unnecessary.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18748/153959009513104_en-US.jpg)

