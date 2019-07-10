# 在Linux系统中卸载文件系统 {#task_f5r_3kk_2fb .task}

本文介绍如何在云服务器ECS（ Linux 系统）中卸载文件系统。

1.  登录[云服务器 ECS](https://ecs.console.aliyun.com/)。
2.  执行`umount /mnt`命令，卸载NFS文件系统。 

    其中，/mnt目录请使用实际值替换。

    卸载命令格式：`umount /挂载的目录地址`。

    **说明：** 

    建议您不要指定任何其他umount选项，并避免修改任何其他umount选项的默认值。

    在卸载过程中，如果提示device is busy，则需要先杀掉正在使用此NAS的进程。

    1.  安装fuser。
        -   CentOS、Redhat、Aliyun Linux操作系统自带fuser，无需安装。
        -   Ubuntu或Debian操作系统：执行`apt install -y fuser`命令进行安装。
    2.  执行`fuser -mv <挂载点本地路径>`命令，查看当前正在使用此NAS的进程pid（pid为kernel的进程不需要处理）。
    3.  执行`kill <pid>`命令，杀掉进程。
3.  执行`mount -l`命令，查看卸载结果。 

    如果回显中未找到您挂载的NAS文件系统信息，表示该文件系统已卸载成功。


