# 下载安装NFS传输加密客户端 {#task_zsp_dsn_mfb .task}

使用传输加密功能前，您需要下载并安装 NFS 传输加密客户端。

NFS 传输加密客户端支持以下操作系统：

-   Aliyun Linux 17.1
-   Red Hat Enterprise Linux \(以及衍生版 CentOS\) version 7 及以上
-   Ubuntu 16.04 LTS及以上
-   Debian 8及以上

NFS 传输加密客户端依赖以下内容，这些内容会在安装工具时自动安装。

-   NFS client \(nfs-utils 包或 nfs-common 包\)
-   Stunnel \(版本4.56或者以上\)
-   Python \(版本2.7或者以上\)
-   OpenSSL \(版本1.0.2或者更新\)

1.  登录[文件存储控制台](https://nas.console.aliyun.com/)。 
2.  选择区域**华北1**，选择一个类型为容量型，支持协议为 NFS 的文件系统，单击其名称。 

    **说明：** 如果在当前区域没有符合条件的文件系统，您可以新建一个类型为容量型，支持协议为 NFS 的文件系统。有关新建文件系统的详细步骤，请参阅[创建文件系统](../../../../../cn.zh-CN/快速配置指南/创建文件系统.md#)。

3.  在文件系统的详情页面，单击**客户端工具下载**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23838/155488523313834_zh-CN.png) 
4.  按照提示下载 rpm 或 deb 格式的安装包。 
5.  运行命令，安装 NFS 传输加密客户端。各系统中的安装命令如下： 
    -   Aliyun Linux/CentOS 7+：

        ```
        sudo yum update
        sudo yum install aliyun-alinas-utils-*.rpm
        ```

    -   Red Hat 7+：

        ```
        sudo yum update
        sudo yum --disablerepo=rhui-rhel-7-server-rhui-extras-debug-rpms install aliyun-alinas-utils-*.rpm
        ```

    -   Ubuntu 16+/Debian 8+：

        ```
        sudo apt update
        sudo dpkg –i aliyun-alinas-utils-*.deb（该步骤会报错，请忽略，直接执行下一步）
        sudo apt-get install –f
        sudo dpkg –i aliyun-alinas-utils-*.deb
        
        ```

6.  运行`man mount.alinas`命令，检查安装是否完成。 如果运行上述命令后能显示帮助文档，则说明客户端安装成功。

