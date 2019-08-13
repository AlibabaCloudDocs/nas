# 自动挂载NFS文件系统 {#task_xmg_1kk_2fb .task}

本文档介绍如何修改Linux系统中的配置文件，使其重启时自动挂载NFS文件系统。

1.  已创建文件系统，详情请参见[创建文件系统](cn.zh-CN/控制台用户指南/管理文件系统.md#section_5jo_0kj_jn5)。
2.  已添加挂载点，详情请参见[添加挂载点](cn.zh-CN/控制台用户指南/管理挂载点.md#section_6xi_a3u_zkq)。
3.  已安装NFS客户端，详情请参见[安装NFS客户端](cn.zh-CN/控制台用户指南/挂载文件系统/手动挂载NFS文件系统.md#section_kvj_d02_szj)。

## 容量型/性能型NAS {#section_s5p_3m3_0zz .section}

您可以在Linux系统中配置 /etc/fstab 文件（推荐使用）或 /etc/rc.local 文件实现NFS文件系统自动挂载。

1.  登录[云服务器ECS](https://ecs.console.aliyun.com/)。
2.  配置自动挂载。 
    -   （推荐使用） 打开 /etc/fstab 配置文件，添加挂载命令。

        **说明：** 如果您是在CentOS6.x系统中配置自动挂载，您需先执行`chkconfg netfs on`命令，保证netfs开机自启动。

        -   如果您要挂载NFSv4文件系统，添加以下命令：

            ``` {#codeblock_xa1_fs1_x6w}
            file-system-id.region.nas.aliyuncs.com:/ /mnt nfs vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
            ```

        -   如果您要挂载NFSv3文件系统，添加以下命令：

            ``` {#codeblock_35n_dl7_76g}
            file-system-id.region.nas.aliyuncs.com:/ /mnt nfs vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
            ```

    -   打开/etc/rc.local配置文件，添加挂载命令。

        **说明：** 

        在配置/etc/rc.local文件前，请确保用户对/etc/rc.local和/etc/rc.d/rc.local文件有可执行权限。例如CentOS7.x系统，用户默认无可执行权限，需添加权限后才能配置/etc/rc.local文件。

        -   如果您要挂载NFSv4文件系统，添加以下命令：

            ``` {#codeblock_rwc_8h8_n9h}
            sudo mount -t nfs -o vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
            ```

        -   如果您要挂载 NFSv3 文件系统，添加以下命令：

            ``` {#codeblock_ghm_wat_r6b}
            sudo mount -t nfs -o vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
            ```

        命令中各参数说明如下表所示。

        |参数|说明|
        |--|--|
        |挂载点| 挂载点包括挂载点域名和挂载点路径，请根据实际值替换。

        -   挂载点域名：添加挂载点时自动生成，无需手工配置。
        -   挂载点路径：挂载的目标地址，Linux 系统中的根目录（/）或任意子目录（如/mnt）。
 |
        |\_netdev|防止客户端在网络就绪之前开始挂载文件系统。|
        |0（noresvport 后第一项）|非零值表示文件系统应由 dump 备份。对于 NAS，此值为 0。|
        |0（noresvport 后第二项）|该值表示 fsck 在启动时检查文件系统的顺序。对于 NAS 文件系统，此值应为 0，表示 fsck 不应在启动时运行。|

3.  执行`reboot`命令，重启云服务器 ECS。
4.  执行`mount -l`命令，查看挂载结果。 

    如果回显包含如下类似信息，说明挂载成功。

    ![挂载结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21207/156568690451407_zh-CN.png)

    挂载成功后，您还可以通过`df -h`命令，可以查看文件系统的当前容量信息。如果挂载失败，请参见[挂载失败的排查与处理方法](../cn.zh-CN/常见问题/挂载失败的排查与处理方法.md#)进行排查。

5.  挂载成功后，您可以在ECS上访问NAS文件系统，执行读取或写入操作。 

    您可以把NAS文件系统当作一个普通的目录来访问和使用，例子如下：

    ![读写操作](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18690/156568690554347_zh-CN.png)


## 极速型 NAS {#section_gsl_kkp_hhb .section}

您可以在 Linux 系统中配置 /etc/fstab 文件实现 NFS 文件系统自动挂载。

1.  登录[云服务器ECS](https://ecs.console.aliyun.com/)。
2.  打开 /etc/systemd/system/sockets.target.wants/rpcbind.socket 文件，注释掉IPv6相关的rpcbind参数，否则NFS的rpcbind服务自动启动会失败。 

    ``` {#codeblock_ytt_vbl_05p}
    vi /etc/systemd/system/sockets.target.wants/rpcbind.socket
    ```

    ![注释rpcbind参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21506/156568690551186_zh-CN.png)

    **说明：** 如果您是在CentOS6.x系统中配置自动重启，您还需执行以下两个操作。

    1.  执行`chkconfg netfs on`命令，保证netfs开机自启动。
    2.  打开/etc/netconfig配置文件，注释掉inet6相关的内容。

        ![注释inet6相关内容](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21506/156568690551194_zh-CN.png)

3.  打开/etc/fstab配置文件，添加以下命令。 

    ``` {#codeblock_tj5_65v_w2c}
    file-system-id.region.extreme.nas.aliyuncs.com:/share /mnt nfs vers=3,proto=tcp,noresvport,_netdev 0 0
    ```

    命令中各参数说明如下表所示。

    |参数|说明|
    |--|--|
    |挂载点| |
    |vers|文件系统版本，目前只支持nfsv3。|
    |\_netdev|防止客户端在网络就绪之前开始挂载文件系统。|
    |0（noresvport 后第一项）|非零值表示文件系统应由 dump 备份。对于 NAS，此值为 0。|
    |0（noresvport 后第二项）|该值表示 fsck 在启动时检查文件系统的顺序。对于 NAS 文件系统，此值应为 0，表示 fsck 不应在启动时运行。|
    |挂载选项|详情请参见[容量型/性能型NAS](#section_s5p_3m3_0zz)的挂载选项说明表。|

4.  执行`reboot`命令，重启云服务器 ECS。
5.  执行`mount -l`命令，查看挂载结果。 

    如果回显包含如下类似信息，说明挂载成功。

    ![挂载结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21506/156568690551183_zh-CN.png)

    挂载成功后，您还可以通过`df -h`命令，可以查看文件系统的当前容量信息。如果挂载失败，请参见[挂载失败的排查与处理方法](../cn.zh-CN/常见问题/挂载失败的排查与处理方法.md#)进行排查。

6.  挂载成功后，您可以在ECS上访问NAS文件系统，执行读取或写入操作。 

    您可以把NAS文件系统当作一个普通的目录来访问和使用，例子如下：

    ![读写操作](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18690/156568690554347_zh-CN.png)


