# CPFS 使用指南 {#concept_cyg_wng_4gb .concept}

CPFS 是阿里云新上线的并行文件存储服务，专注于提供高性能的文件存储和访问能力。

## 管理文件系统 {#section_ecs_nr2_2hb .section}

请参见[快速配置指南](../../../../../cn.zh-CN/快速配置指南/创建文件系统.md#)来创建文件系统。CPFS 服务目前采用预付费模式（即包年包月），服务期间您可以根据自身业务增长情况，选择**升级**来提高存储容量和对应的带宽和 IOPS 性能。在服务到期之前，您可以选择**续费**来延长使用时间。

## 文件系统的挂载使用 {#section_rw2_1s2_2hb .section}

文件存储 CPFS 兼容 POSIX 接口，通过标准挂载就可以使用。我们提供定制化的客户端软件，请按照以下步骤进行安装配置。

本环境为 CentOS 操作系统。步骤如下：

1.  请先安装以下依赖包：make、gcc、libyaml-devel、libtool、zlib-devel、glibc-headers、kernel-devel

    安装命令为：

    ```
    yum install -y make gcc libyaml-devel libtool zlib-devel glibc-headers kernel-devel
    ```

    **说明：** 请确保安装的 kernel-devel 版本和 kernel版本一致。

2.  下载 [CPFS 客户端安装包](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/108096/cn_zh/1553564531232/cpfs-client-1.2.1-centos.x86_64.rpm)，安装到服务器端。

    安装命令为：

    ```
    rpm -ivh cpfs-client-1.0.dev-rc_2.x86_64.rpm
    ```

    -   编辑配置文件`/etc/cpfs/cpfs-client-autobuild.conf`中的rebuild选项。

```
buildArgs=-j16
configArgs=--with-o2ib=no
```

        保存后运行`service cpfs-client rebuild`命令，10分钟左右完成客户端的 rebuild。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147136/155383645741321_zh-CN.png)

    -   编辑配置文件`/etc/cpfs/cpfs-mounts.conf`，增加文件系统和挂载目录信息。

        ```
        buildArgs=-j16
        configArgs=--with-o2ib=no
        ```

        查看挂载信息：

        ```
        cat /etc/cpfs/cpfs-mounts.conf
        192.168.5.179@tcp:/hpctest	/mnt/test
        ```

        通过service cpfs-client start/stop 来启动或停止挂载服务。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147136/155383645741331_zh-CN.png)


