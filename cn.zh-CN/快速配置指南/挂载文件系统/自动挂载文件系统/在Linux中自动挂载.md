# 在Linux中自动挂载 {#concept_xmg_1kk_2fb .concept}

您可以修改 ECS 示例中的配置文件，使其重启时自动挂载 NAS 文件系统。

您可以通过配置/etc/fstab文件以及配置/etc/rc.local文件两种方式在 Linux 系统中设置自动挂载。

## 配置 /etc/fstab 文件（推荐） {#section_czd_wmk_2fb .section}

在首次连接至 ECS 实例后，在该实例的/etc/fstab配置文件中添加以下命令：

```
fid-xxxx.cn-hangzhou.nas.aliyuncs.com:/ /mnt  nfs4 vers=4.0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
```

命令中各参数说明如下：

|参数|说明|
|--|--|
|**\_netdev**|防止客户端在网络就绪之前开始挂载文件系统。|
|**0**（noresvport 后第一项）|非零值表示文件系统应由 dump 备份。对于 NAS，此值为 0。|
|**0**（noresvport 后第二项）|该值表示 fsck 在启动时检查文件系统的顺序。对于 NAS 文件系统，此值应为 0，表示 fsck 不应在启动时运行。|

## 配置 /etc/rc.local 文件 {#section_k4v_ynk_2fb .section}

在首次连接至 ECS 实例后，在该实例的/etc/rc.local配置文件中添加挂载命令。

以挂载 NFSv4 文件系统为例，添加的命令如下：

```
sudo mount -t nfs -o vers=4.0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport fid-xxxx.cn-hangzhou.nas.aliyuncs.com:/ /mnt
```

**说明：** 

-   命令中的fid-xxxx.cn-hangzhou.nas.aliyuncs.com为挂载点的域名。有关挂载命令，请参阅[在 Linux 系统中挂载 NFS 文件系统](cn.zh-CN/快速配置指南/挂载文件系统/挂载 NFS 文件系统/在 Linux 系统中挂载 NFS 文件系统.md#)。
-   在配置/etc/rc.local文件前，需要确保用户对/etc/rc.local和/etc/rc.d/rc.local文件有可执行权限。

## 极速型 NAS 的配置 {#section_gsl_kkp_hhb .section}

1.  编辑/etc/systemd/system/sockets.target.wants/rpcbind.socket文件，注释掉 IPv6 相关的rpcbind参数，否则 NFS 的 rpcbind 服务自动启动会失败。如图所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21506/155429651343322_zh-CN.png)

2.  在首次连接至 ECS 实例后，在该实例的/etc/fstab配置文件中添加以下命令：

    ```
    xxxx:/share /tmp/benchmark   nfs vers=3,proto=tcp,noresvport,_netdev 0 0
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21506/155429651343323_zh-CN.png)


