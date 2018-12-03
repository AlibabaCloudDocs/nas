# 在Linux中卸载文件系统 {#task_f5r_3kk_2fb .task}

本文介绍如何从基于 Linux 系统的 ECS 实例中卸载文件系统。

1.  在 ECS 实例中运行以下命令： 

    ```
    umount <挂载目标目录>
    ```

    **说明：** 

    建议您不要指定任何其他 umount 选项，并避免修改任何其他 umount 选项的默认值。

2.  在 ECS 实例中运行 df 命令，验证 NAS 文件系统是否成功卸载。 

    df 命令能够显示挂载在当前 ECS 实例上的文件系统的磁盘使用情况及统计信息。如果该命令的输出结果中没有您想要卸载的 NAS 文件系统，表示该文件系统已经成功卸载。


-   查看 NAS 文件系统的挂载状态。

    ```
    $ df -T
    Filesystem Type 1K-blocks Used Available Use% Mounted on
    /dev/vda1 ext4 41151808 5658860 33379516 15% /
    devtmpfs devtmpfs 8122760 0 8122760 0% /dev
    tmpfs tmpfs 8133492 0 8133492 0% /dev/shm
    tmpfs tmpfs 8133492 552 8132940 1% /run
    tmpfs tmpfs 8133492 0 8133492 0% /sys/fs/cgroup
    fid-xxxx.cn-hangzhou.nas.aliyuncs.com:/ nfs4 1099511627776 2498679808 1097012947968 1% /mnt
    
    ```

-   卸载文件系统。

    ```
    $ umount /mnt 
    ```


