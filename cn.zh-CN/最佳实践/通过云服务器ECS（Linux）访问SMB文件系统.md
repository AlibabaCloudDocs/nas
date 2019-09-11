# 通过云服务器ECS（Linux）访问SMB文件系统 {#task_1580275 .task}

本文主要介绍如何将SMB文件系统挂载至云服务器ECS（Linux）并进行读写操作。

-   在需要创建文件系统的地域，已有可用的云服务器ECS（Linux）。

    SMB文件系统现在官方支持如下的Linux分发版本，本文中，如果没有特别声明，也只针对以下几个Linux分发版本。

    -   CentOS 7.6 64bit （3.10.0-957.5.1.el7.x86\_64）
    -   Ubuntu 18.04 64bit（4.15.0-48-generic）
    -   Debian 9.9 64bit（4.9.0-9-amd64）
    -   Suse Enterprise Server 12 SP2 64bit（4.4.74-92.35-default）
    -   OpenSUSE 42.3 64bit（4.4.90-28-default）
    -   Aliyun Linux（4.19.34-11.al7.x86\_64）
    -   CoreOS（4.19.43-coreos VersionID=2079.4.0）
    **说明：** 由于Linux一些早期版本的SMB内核客户端在某些关键场景有缺陷，用户如果使用非官方支持的Linux分发版本，阿里云不能保证该SMB文件系统的可靠性。

-   网络连通
    -   云服务器ECS（Linux）需要和SMB文件系统在可连通的同一个用户网络中（比如在同一个VPC ）。
    -   检查文件系统白名单，确保云服务器ECS（Linux）已经被授权访问该SMB文件系统。
    -   确保端口445处于打开状态，SMB通过TCP端口445通信。

        如果端口445未打开，请在目标ECS实例的安全组中添加关于端口445的安全组规则，详情请参见[添加安全组规则](../../../../../intl.zh-CN/安全/安全组/添加安全组规则.md#)。

-   已创建SMB文件系统，详情请参见[创建文件系统](../intl.zh-CN/控制台用户指南/管理文件系统.md#section_5jo_0kj_jn5)。
-   已添加挂载点，详情请参见[添加挂载点](../intl.zh-CN/控制台用户指南/管理挂载点.md#section_6xi_a3u_zkq)。
-   软件要求

    Linux分发版本都预装了内核客户端，您还需安装cifs-util工具包。

    -   如果您使用Ubuntu、Debian操作系统，使用apt-get包管理器进行安装

        ``` {#codeblock_c8u_ftu_es6}
        sudo apt-get update
        ```

        ``` {#codeblock_rup_brf_b4w}
        sudo apt-get install cifs-utils
        ```

    -   如果您使用RHEL、CentOS、Aliyun Linux操作系统，使用yum包管理器进行安装

        ``` {#codeblock_gky_h2e_tru}
        sudo yum install cifs-utils
        ```

    -   如果您使用OpenSUSE、SLES12-SP2操作系统，使用使用zypper或者yast工具进行安装

        ``` {#codeblock_hhe_4l0_iys}
        sudo zypper install cifs-utils
        ```

        ``` {#codeblock_nrd_vqh_i04}
        sudo yast2 -> Software -> Software Management, 然后安装cifs-utils
        ```

    -   如果您使用阿里云支持的CoreOS分发版本，通过以下方法进行安装
        1.  配置SELINUX

            ``` {#codeblock_jeh_t1b_bne}
            sed -i 's/SELINUXTYPE=mcs/SELINUXTYPE=targeted/' /etc/selinux/config
            ```

        2.  在CoresOS上自行编译cifs-utils

            您可以执行以下命令启动一个Fedora容器用以编译cifs-utils客户端工具或者下载阿里云官方提供使用的CoreOS版本的cifs-utils工具，并拷贝至/tmp/或者/bin目录。

            ``` {#codeblock_c06_e3c_u73}
            $ docker run -t -i -v /tmp:/cifs fedora /bin/bash
            
            fedora # yum groupinstall -y "Development Tools" "Development Libraries"
            
            fedora # yum install -y bzip2
            
            fedora # curl https://download.samba.org/pub/linux-cifs/cifs-utils/cifs-utils-
            
            6.9.tar.bz2 --output cifs-utils-6.9.tar.bz2;
            
            fedora # bunzip cifs-utils-6.9.tar.bz2; && tar xvf cifs-utils-6.9.tar
            
            fedora # cd cifs-utils-6.9; ./configure && make
            
            fedora # cp mount.cifs /cifs/
            
            fedora # exit
            ```


## 挂载文件系统 {#section_9sq_p2c_vtp .section}

1.  使用root用户或者sudo enabled客户端管理员用户，登录云服务器ECS（Linux）。
2.  执行以下命令，挂载文件系统。 

    ``` {#codeblock_en5_7p9_l8v}
    mount -t cifs //xxx-crf23.eu-west-1.nas.aliyuncs.com/myshare /mnt -o vers=2.1,guest,uid=0,gid=0,dir_mode=0755,file_mode=0755,mfsymlinks,cache=strict,rsize=1048576,wsize=1048576
    ```

    挂载命令格式：mount -t cifs //<挂载点域名\>/myshare <挂载目录\> -o <挂载选项\>

    |参数|说明|
    |--|--|
    |文件系统类型|SMB文件系统，必须使用-t cifs。|
    |挂载点域名|创建文件系统挂载点时，自动生成的挂载点域名，请根据实际值替换。挂载点详情请参见[../DNnas1882233/ZH-CN\_TP\_18694\_V10.dita\#task\_27531\_zh](../DNnas1882233/ZH-CN_TP_18694_V10.dita#task_27531_zh)。|
    |myshare|SMB的share名称，不允许变更。|
    |挂载目录|您要挂载的目标目录，如/mnt/sharepath。|
    |挂载选项（option）|通过 -o 指定挂载选项     -   （必选）vers：支持2.1 和 3.0协议版本。
    -   （必选）guest：在认证方面，现在只支持基于ntlm认证协议的guest挂载。即使用username=guest、password=guest或者guest。

**说明：** 服务器支持ntlm, ntlmv2和ntlmssp。缺省时，SMB客户端和服务器会协商一个可接受的ntlm认证协议；或者您在挂载时，通过"sec" option可以选择一个自己期望的值（ntlm, ntlmv2 或者ntlmssp）。

    -   （可选）uid：挂载成功后，文件所属的用户。如果未设置uid，则默认uid=0。
    -   （可选）gid：挂载成功后，文件所属的用户组。如果未设置gid，则默认gid=0。
    -   （可选）dir\_mode：向用户授予目录的读取、写入和执行权限。必须以0开头，如0755、0644等。如果未设置dir\_more ，则默认dir\_mode=0755。
    -   （可选）file\_mode：向用户授予普通文件的读取、写入和执行权限。必须以0开头，如0755、0644等。如果未设置file\_mode，则默认file\_mode=0755。
    -   （可选）mfsymlinks：需要用以支持symbol link功能。
    -   （可选）cache：
        -   cache=strict：设置SMB客户端使用客户端缓存。如果未设置cache，则默认cache=strict。
        -   cache=none：设置SMB客户端不使用客户端缓存。
    -   （可选）rsize：用来设置读数据包的最大限制。一般不需要设置，使用缺省值1048576即可。
    -   （可选）wsize：用来设置内写数据包的最大限制，一般不需要设置，使用缺省值1048576即可。
    -   （可选）atime|relatime：如果您的业务不是对文件的访问时间极为敏感请不要在挂载时使用atime选项，缺省时会使用relatime方式挂载。
 **说明：** 

    -   被授权的云服务器（Linux）管理员拥有对SMB文件系统的绝对控制权。
    -   您可以使`mount | grep cifs`命令查询自己的挂载点信息。
    -   如果您使用非官方支持的Linux分发版本，强烈建议使用内核在3.10.0-514以上的版本。如果Linux kernel版本小于等于3.7，一定要在挂载选项中显示设置cache=strict参数。您可以使`uname -a`命令检查当前内核版本。
 |

3.  执行`mount -l`命令，查看挂载结果。 

    如果回显包含如下类似信息，说明挂载成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1253385/156819099754720_zh-CN.png)

4.  挂载成功后，您可以在ECS（Linux）上访问NAS文件系统，执行读取或写入操作。 

    您可以把NAS文件系统当作一个普通的目录来访问和使用，例子如下：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18690/156819099754347_zh-CN.png)


## 经典使用场景 {#section_6xk_1hd_bzj .section}

不同使用场景，可选择不同的挂载选项，比较经典的使用场景及挂载选项配置如下所示。

-   云服务器ECS（Linux）共享访问场景

    在多个云服务器ECS（Linux）中需要共享访问文件系统数据，但没有用户权限控制要求，被授权的云服务器ECS（Linux）管理员可以使用如下方法在各个云服务器ECS（Linux）上执行挂载。

    ``` {#codeblock_bbm_mfx_4i6}
     mount -t cifs //smbfs.hangzhou-g.aliyun.com/myshare /mnt/sharepath -o vers=2.1,guest,mfsymlinks
    ```

-   多用户Home Directory场景

    在多个云服务器ECS（Linux）中需要共享访问文件系统数据时，如果有权限控制需求，可以通过挂载时指定uid、gid、dir\_mode、file\_mode来满足要求。

-   云服务器ECS（Linux） WebServer共享访问场景

    在多个云服务器ECS（Linux）上安装WebServer\(如apache\)，并且SMB文件系统做共享文件存储。

    **说明：** 

    -   SMB文件系统主要特点是共享访问、横向扩展、高可用，和本地硬盘由于实现机理不同，某些场景的小文件访问性能上会稍微有一些差距。对于WebServer场景，如果想要达到极致性能，可以考虑只将需要共享的文件放在SMB文件系统上，而将不需要共享访问的WebServer程序等放在本地硬盘。
    -   WebServer应用通常网络协议通讯负载较大，我们为这个场景做了专门的WebServer加速功能，您可以联系阿里云NAS团队申请开通。
-   云服务器ECS（Windows）和云服务器ECS（Linux）共享访问

    如果您需要同时从云服务器ECS（Windows）和云服务器ECS（Linux）访问SMB文件系统的内容。这个场景下，云服务器ECS（Linux）挂载时一定要使用客户端缓存，即设置cache=strict或者缺省方式挂载。


如果您在使用中遇到问题，请参见[通过云服务器ECS（Linux）访问SMB文件系统的问题排查](../intl.zh-CN/常见错误排查/通过云服务器ECS（Linux）访问SMB文件系统的问题排查.md#)。

