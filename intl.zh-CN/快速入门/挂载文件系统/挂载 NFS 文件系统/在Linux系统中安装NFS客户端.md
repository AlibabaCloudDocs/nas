# 在Linux系统中安装NFS客户端 {#task_all_hsg_cfb .task}

要在 Linux 系统中将 NAS 的 NFS 文件系统挂载至 ECS 实例，您需要安装 NFS 客户端。

1.  使用 ECS 实例的公有 DNS 名称和用户名进行登录，连接至 ECS 实例。 
2.  运行以下命令，安装 NFS 客户端。 
    -   如果您使用 CentOS 操作系统，运行以下命令：

        ```
        sudo yum install nfs-utils
        ```

    -   如果您使用 Ubuntu 或 Debian 操作系统，运行以下命令：

        ```
        sudo apt-get install nfs-common
        ```


