# Use CPFS {#concept_cyg_wng_4gb .concept}

Cloud Paralleled File System \(CPFS\) is a parallel file storage service that is released by Alibaba Cloud. It is dedicated to providing high-performance and easy-to-access file storage.

## Manage file systems {#section_ecs_nr2_2hb .section}

For more information about how to create a file system, see [Quick Start](../../../../reseller.en-US/Quick Start/Create file systems.md#). CPFS only supports the subscription billing method. During a service period, you can **upgrade** the service to increase storage capacity, bandwidth, and IOPS performance. Before the service expires, you can **renew** the service to extend the service time.

## Mount a file system {#section_rw2_1s2_2hb .section}

CPFS is compatible with POSIX-based APIs. You can use one or more of these APIs to mount a CPFS file system. We recommend that you use the custom CPFS client. For example, you can install the custom CPFS client on the CentOS operating system as follows.

1.  Install dependency packages in the following order: make, gcc, libyaml-devel, libtool, zlib-devel, glibc-headers, and kernel-devel.

    ``` {#codeblock_0pe_a7m_z11}
    yum install -y make gcc libyaml-devel libtool zlib-devel glibc-headers kernel-devel
    ```

    **Note:** Ensure that the version of the kernel-devel package is the same as that of the kernel.

2.  Download the [Installation package of a CPFS client](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/108096/cn_zh/1553564531232/cpfs-client-1.2.1-centos.x86_64.rpm) and install the package on the server. Run the following command to install the package.

    ``` {#codeblock_pkx_2xv_yit}
    rpm -ivh cpfs-client-1.0.dev-rc_2.x86_64.rpm
    ```

    1.  Open the `/etc/cpfs/cpfs-client-autobuild.conf` configuration file, and modify the rebuild option as follows:

        ``` {#codeblock_7re_l7r_u83}
        buildArgs=-j16
        configArgs=--with-o2ib=no
        ```

    2.  Save the file and run the `service cpfs-client rebuild` command. This process takes about 10 minutes to complete.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147136/155868616241321_en-US.png)

3.  Open the `/etc/cpfs/cpfs-mounts.conf` configuration file, and add a file system and mount drive.

    ``` {#codeblock_po3_pm1_ezp}
    192.168.5.179@tcp:/hpctest	/mnt/test
    ```

4.  Run the service cpfs-client start command or the service cpfs-client stop command to start or stop the mount service.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147136/155868616241331_en-US.png)


