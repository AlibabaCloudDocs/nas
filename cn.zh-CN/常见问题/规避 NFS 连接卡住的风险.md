# 规避 NFS 连接卡住的风险 {#task_508507 .task}

在网络抖动或者服务端升级时，可能发生 TCP 连接异常，在某些情况下会造成 NFS 文件系统卡住，需要在卡住之后，手动重新挂载才能恢复。

## 规避方法 {#section_gw8_cy2_741 .section}

为了避免以上风险，让异常的 TCP 连接自动恢复，请确保挂载 NFS 文件系统的 ECS 实例同时满足以下两个条件：

1.  拥有 2.6.32-696.16.1 及以上版本的 Linux 内核。
2.  使用 noresvport 参数挂载 NFS 文件系统并且确认生效。

## 确认内核版本 {#section_f9j_z33_yhx .section}

您可以在 ECS 实例上执行`uname -a`命令查看当前内核版本。

请务必确保内核版本高于 2.6.32-696.16.1，否则必须尽快升级内核。继续使用低版本内核会对您的业务带来巨大的风险，在升级过程中可能会造成 NFS 文件系统卡住，在卡住之后，必须手动重新挂载才能恢复业务。如果在卡住之后没有及时手动重新挂载，会造成无限长时间的业务停滞。

要让异常的 TCP 连接自动恢复，规避 NFS 文件系统卡住的风险，请在谨慎评估应用与内核的兼容性之后，逐台升级内核。假如评估发现无法升级内核，请尽快通过钉钉用户群[联系我们](../../../../cn.zh-CN/联系我们/联系我们.md#)。

**说明：** 

NFS 客户端是 Linux 内核的一部分，请避免使用有缺陷的内核版本，详细信息请参考 [NFS 客户端已知问题](cn.zh-CN/常见问题/NFS 客户端已知问题.md#)。

内核升级后，请重启 ECS 实例使新内核生效。

## 使用 noresvport 参数 {#section_7s6_x8n_97v .section}

确认 ECS 实例内核版本符合要求后，请执行`ss -nt | grep 2049 | awk '{print $4}' | awk -F ':' '{print $2}'`命令检查挂载 NFS 的端口号是否大于 1024，确认 noresvport 参数是否已经生效。

-   如果没有输出结果，或者所有输出结果都大于 1024，则说明升级过程不会对 TCP 连接造成影响。
-   如果有任何结果小于1024，请按照下面推荐的方法，将NFS文件系统全部卸载，再重新挂载。

    此处挂载点地址以 foo.aliyuncs.com 为例，挂载的本地目录路径以/mnt为例。

    1.  执行以下命令记录已经挂载的所有 NFS 文件系统，找到一个挂载的本地目录（例如/mnt）。

        ``` {#codeblock_8r2_yoj_qll}
        mount | grep aliyun > /tmp/mount_aliyun && cat /tmp/mount_aliyun
        ```

    2.  停止对/mnt中的任何文件进行操作的所有应用。
    3.  卸载文件系统。

        ``` {#codeblock_6e1_fnf_zlv}
        sudo umount /mnt
        ```

        如果卸载失败，请确认所有相关应用已停止后，执行`sudo umount -lf /mnt`。

    4.  检查是否所有的 NFS 文件系统卸载完成。

        ``` {#codeblock_4oz_5z8_uvb}
        mount | grep aliyun
        ```

        -   如果返回为空，则表示所有的 NFS 文件系统卸载完成。
        -   如果返回不为空，请重复[步骤 ii](#li_92w_5og_153) 和[步骤 iii](#li_b13_ueh_pbw)，直到所有的 NFS 文件系统卸载完成。
    5.  挂载文件系统。
        -   如果希望使用 NFSv4 挂载，请执行以下命令。

            ``` {#codeblock_o8h_6ve_cg0}
            sudo mount -t nfs -o vers=4.0,noresvport foo.aliyuncs.com:/ /mnt || sudo mount -t nfs4 -o noresvport foo.aliyuncs.com:/ /mnt
            ```

        -   如果希望使用 NFSv3 挂载，请执行以下命令。

            ``` {#codeblock_f1u_8rb_bpu}
            sudo mount -t nfs -o vers=3,nolock,proto=tcp,noresvport foo.aliyuncs.com:/ /mnt
            ```

    6.  执行以下命令查找其他需要挂载的文件系统，并执行步骤[步骤 v](#li_so1_j9j_dvw) 完成挂载。

        ``` {#codeblock_txv_oz4_2ri}
        cat /tmp/mount_aliyun
        ```

    7.  当所有 NFS 文件系统重新挂载成功后，请再次执行检查端口号的命令，确保所有端口号大于 1024。

        ``` {#codeblock_i8u_z5u_hgt}
        ss -nt | grep 2049 | awk '{print $4}' | awk -F ':' '{print $2}'
        ```

        如果端口号仍然有小于 1024 的情况，请执行`uname -a`确认内核版本高于 2.6.32-696.16.1。如果按照上述步骤升级内核后，显示的内核版本仍然低于要求，请确认内核升级后是否已重启 ECS 实例。


## 升级注意事项 {#section_62j_u1a_lba .section}

完成所有上述操作后，升级过程中的 TCP 连接异常可以全部自动恢复。虽然无须人工干预，但仍然建议您在升级期间关注业务运行状况。

升级期间我们的研发团队会密切关注 TCP 连接恢复情况，如果需要您手动重新挂载恢复业务，我们会在第一时间联系您，请保持阿里云账号的手机号码畅通。

