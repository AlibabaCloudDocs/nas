# 使用 SFTP 上传下载 NAS 文件系统数据 {#task_gyq_l12_ggb .task}

本文档介绍如何使用 SFTP 上传下载 NAS 文件系统数据。

SFTP 的传输速度依赖于 ECS 的外网带宽，可根据业务需求配置适当的网络带宽。

1.  在 NAS 文件系统所在区域购买一台 CentOS 操作系统的 ECS 实例。 
2.  登录 ECS 实例并修改配置文件 /etc/ssh/sshd\_config。 
    1.  将原 `sshd_config`配置文件中的 `subsystem` 行注释掉，新增一行 Subsystem sftp internal-sftp。

        ```
        # override default of no subsystems
        #Subsystem      sftp    /usr/libexec/openssh/sftp-server
        Subsystem     sftp   internal-sftp
        ```

    2.  在 `sshd_config` 文件末尾添加如下内容。其中 /usr/sftp 为用户的 sftp 根目录，此处名字仅作为参考，可以根据实际情况修改。

        ```
        X11Forwarding no
        AllowTcpForwarding no
        ForceCommand internal-sftp
        ChrootDirectory /usr/sftp
        ```

3.  使用命令 groupadd sftp 添加用户组。 
4.  使用命令 useradd -g sftp -s /sbin/nologin -M sftp 添加用户并设置为 SFTP 组。 
5.  设置 SFTP 用户密码。 

    ```
    [root@localhost ~]# passwd sftp
    更改用户 sftp 的密码 。
    新的密码：
    无效的密码：密码少于 8 个字符
    输入密码新的密码：
    passwd:所有的身份验证令牌已经成功更新。
    ```

6.  创建 SFTP 用户的根目录、属主和属组，并修改权限（755）。 

    ```
    [root@localhost ~]# cd /usr
    [root@localhost usr]# mkdir sftp
    [root@localhost usr]# chown root:sftp sftp
    [root@localhost usr]# chmod 755 sftp
    ```

7.  在 SFTP 的目录中创建 NAS 挂载目录。 

    ```
    [root@localhost usr]# cd sftp/
    [root@localhost sftp]# mkdir file
    [root@localhost sftp]# chown sftp:sftp file
    ```

8.  执行以下命名将 NAS 文件系统挂载到 /usr/sftp/file 目录。 

    ```
    sudo mount -t nfs -o vers=4.0
    91fd04a7b7-cvn49.cn-zhangjiakou.nas.aliyuncs.com:/ /usr/sftp/file
    ```

9.  执行 `service sshd restart` 命令重启 sshd 服务。 
10.  使用 SFTP 客户端登录 SFTP 服务，账号密码为前面配置 SFTP 的账号密码。下图使用的是 winscp 工具，可根据实际情况使用支持 SFTP 协议的客户端连接。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83085/155437026635227_zh-CN.png)

 

