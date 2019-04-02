# How to use CPFS {#concept_cyg_wng_4gb .concept}

Cloud Paralleled File System \(CPFS\) is a parallel file storage service that is recently released by Alibaba Cloud. It is dedicated to providing high-performance and easy-to-access file storage.

## Manage file systems {#section_ecs_nr2_2hb .section}

For more information, see [Quick Start Guide](../../../../../intl.en-US/Quick Configuration Guide/Create file systems.md#) for instructions on how to create a file system. Currently, CPFS provides the subscription billing method. During a service period, you can **upgrade** the service to increase storage capacity, corresponding bandwidth, and IOPS performance. Before the service expires, you can **renew** the service to extend the service time.

## Mount a file system {#section_rw2_1s2_2hb .section}

CPFS is compatible with POSIX-based APIs. You can use one or more of these APIs to mount a CPFS file system. Alibaba Cloud provides a custom client application. You can use the following steps to install and configure the client application.

Take a CentOS operating system as an example. Proceed as follows:

1.  Install dependency packages in the following order: make, gcc, libyaml-devel, libtool, zlib-devel, glibc-headers, kernel-devel.

    You can run the following command to install packages:

    ```
    yum install -y make gcc libyaml-devel libtool zlib-devel glibc-headers kernel-devel
    ```

    **Note:** Ensure that the version of kernel-devel to be installed is the same as that of the kernel.

2.  Download the [Installation package of a CPFS client](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/108096/cn_zh/1553564531232/cpfs-client-1.2.1-centos.x86_64.rpm) and install the package on the server.

    Execute this command to install the package.

    ```
    rpm -ivh cpfs-client-1.0.dev-rc_2.x86_64.rpm
    ```

    -   Open the `/etc/cpfs/cpfs-client-autobuild.conf` configuration file, and modify the rebuild property as follows:

```
buildArgs=-j16
configArgs=--with-o2ib=no
```

        Save the file and run the `service cpfs-client rebuild` command.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147136/155419438241321_en-US.png)

    -   Open the `/etc/cpfs/cpfs-mounts.conf` configuration file, and add

        ```
        buildArgs=-j16
        configArgs=--with-o2ib=no
        ```

        View mount information

        ```
        cat /etc/cpfs/cpfs-mounts.conf
        192.168.5.179@tcp:/hpctest	/mnt/test
        ```

        Execute the service cpfs-client start command or the service cpfs-client stop command to start or stop the mount service.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147136/155419438241331_en-US.png)


