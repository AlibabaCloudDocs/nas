# 通过云服务器ECS（Linux）访问SMB文件系统的问题排查 {#concept_1580359 .concept}

本文详细列出了从云服务器ECS（Linux）访问SMB文件系统时的常见问题、原因与解决方案。

## 无法挂载SMB文件系统 {#section_eqa_mer_pey .section}

通常原因：

-   使用了低版本或者不兼容的Linux操作系统版本，SMB文件系统支持如下的Linux分发版本。
    -   CentOS 7.6 64bit （3.10.0-957.5.1.el7.x86\_64）
    -   Ubuntu 18.04 64bit（4.15.0-48-generic）
    -   Debian 9.9 64bit（4.9.0-9-amd64）
    -   Suse Enterprise Server 12 SP2 64bit（4.4.74-92.35-default）
    -   OpenSUSE 42.3 64bit（4.4.90-28-default）
    -   Aliyun Linux（4.19.34-11.al7.x86\_64）
    -   CoreOS（4.19.43-coreos VersionID=2079.4.0）
-   客户端上未安装CIFS挂载工具（cifs-utils）或者mount.cifs不在PATH指定的命令搜寻目录中。
-   云服务器ECS（Linux）和SMB文件系统的网络不通。

    -   云服务器ECS（Linux）和SMB文件系统不属于同一个阿里云用户。
    -   云服务器ECS（Linux）和SMB文件系统不在同一个阿里云地域（region）。
    -   云服务器ECS（Linux）和SMB文件系统不处于可连通的网络（VPC或经典网络）中。

        **说明：** NAS支持本地挂载，如果Linux客户端在用户IDC中，可能是该IDC和SMB文件系统所处的的网络（VPC或经典网络）没有通过阿里云高速通道连接成功。

    -   SMB文件系统的白名单设置不允许云服务器ECS（Linux）连接。
    -   云服务器ECS（Linux）防火墙设置为不允许访问SMB文件系统的IP地址或445端口。
    -   云服务器ECS（Linux）试图通过不受支持的TCP端口连接，现在SMB只支持445端口。
    **说明：** 

    您可以通过`ping <VolumeDomainName>`和 `telnet <VolumeDomainName> 445`检查连通性。

    如果端口445未打开，请在目标ECS实例的安全组中添加关于端口445的安全组规则，详情请参见[添加安全组规则](../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

-   云服务器ECS（Linux）管理员没有root权限或者没有被设置为有mount命令的sudo权限。
-   挂载时使用的文件系统类型不是cifs。
-   挂载时使用的vers选项既不是2.1也不是3.0。
-   挂载时没有指定guest方式挂载。
-   挂载时指定的uid、gid、dir\_mode或者file\_mode不正确。
-   挂载的目标目录的SELINUX设置不正确。
-   云服务器ECS（Linux）挂载连接数太多，超过了单文件系统挂载上限（1000）。这个在容器场景较容易发生。

解决方案：

1.  参见[通过云服务器ECS（Linux）访问SMB文件系统](../../../../cn.zh-CN/最佳实践/通过云服务器ECS（Linux）访问SMB文件系统.md#)及上述可能原因，自行排查。
2.  检查/var/log/messages和dmesg输出，自行排查。
3.  联系阿里云NAS团队排查。

    同时请提供Linux版本信息、具体挂载命令、/var/log/messages和dmesg输出。


## 文件系统性能不佳 {#section_hrg_428_p2v .section}

如果SMB文件系统性能不佳，您可以从以下方面进行排查。

-   原因1：SMB单个文件系统的吞吐能力与存储量是相联系的。单文件系统的吞吐（读+写）上限与当前存储量呈线性关系。

    解决方案：使用fio工具来测试SMB文件系统性能，详情请参见[NAS性能测试](../../../../cn.zh-CN/性能说明/NAS性能测试.md#)。

-   原因2：云服务器ECS（Linux）的单机网络带宽较小。

    解决方案：使用多个云服务器ECS（Linux）达到文件系统的总体预期性能。

-   原因3：禁用了SMB文件系统的客户端缓存。

    解决方案：在挂载SMB文件系统时，cache=none表示禁用缓存，默认或者cache=strict表示使用缓存；您可以通过`sudo mount | grep cifs`命令检查所用的选项是否正确。

-   原因4：没有设置合适的SMB客户端的I/O大小。

    解决方案：根据业务需求调整rsize/wsize，缺省值：1048576。

-   原因5：云服务器ECS（Linux）的CPU或内存的规格过低，或被其它业务占有过多。

    解决方案：选择合适的云服务器ECS（Linux）规格、检查系统其它应用资源，确保系统满足CPU和内存要求。 您可以通过`top`命令检查系统cpu、mem使用情况。

-   原因6：挂载时使用了atime选项。

    解决方案：如果您的业务不是对文件的访问时间（atime）极为敏感请不要在挂载时使用atime选项。

-   原因7：遇到大量小文件频繁读、少量写但需要写时通知的WebServer场景。

    解决方案：您可以在客户端配置该WebServer（如Apache）产品特定的缓存机制或者联系阿里云NAS团队开通WebServer场景加速功能。


## 迁移/复制文件系统中的文件时速度缓慢 {#section_e7b_fhw_xgb .section}

如果已经排除了上述文件系统本身的性能问题，则可能原因是您没有使用并发式迁移/复制文件。您可以通过以下开源工具进行迁移/复制。

-   [GNU Parallel](https://github.com/martymac/fpart) 

    **说明：** 

    -   根据系统资源，选择合适的线程数。
    -   示例：find \* -type | parallel --will-cite -j 10 cp \{\} /mnt/smb/ &
-   [Fpart](https://github.com/martymac/fpart)
-   [Fpsync](https://github.com/martymac/fpart/blob/master/tools/fpsync)
-   [multi](https://github.com/pkolano/mutil)

## 访问文件系统时，报错：Permission denied {#section_8i1_xfh_84q .section}

原因：Linux管理员在挂载时使用了不正确的uid、gid、file\_mode、dir\_mode。

解决方案：检查是否正确设置了uid、gid、file\_mode、dir\_mode等挂载选项，详情请参见[通过云服务器ECS（Linux）访问SMB文件系统](../../../../cn.zh-CN/最佳实践/通过云服务器ECS（Linux）访问SMB文件系统.md#)。

## 文件名大小写变更 {#section_8q1_l27_fm1 .section}

SMB文件系统对文件名大小写不敏感，和Windows系统保持一致。但在文件名大小写改名这个场景暂时没有支持。

您可以先从大写文件名改成一个其它名字的文件，再改成小写文件名，反之亦然。

## 不能改变文件owner，文件/目录mode {#section_hb7_l5k_cab .section}

现在暂时不支持动态改变，只能在挂载时指定，详情请参见[通过云服务器ECS（Linux）访问SMB文件系统](../../../../cn.zh-CN/最佳实践/通过云服务器ECS（Linux）访问SMB文件系统.md#)。

## 不能使用ACL {#section_z5v_3ve_8tn .section}

暂时不支持使用ACL，如果您有强烈需求，请联系阿里云NAS团队。

## 不能创建符号链接文件 {#section_bcg_1m4_4aa .section}

原因：挂载时没有选择mfsymlinks选项，或者使用了2.0协议版本挂载。

解决方案：挂载文件系统时，使用2.1/3.0协议并且添加mfsymlinks选项。

## SMB挂载点无响应 {#section_xdu_zdp_v6k .section}

原因：在Linux内核为3.10.0-514之前的Linux分发版中，SMB内核驱动在并发场景有时会crash（内核stack如下所示），导致挂载点无法被访问。内核日志中有如下类似信息：

``` {#codeblock_5q0_ern_1vq}
...
[<ffffffffc03c9bc1>] cifs_oplock_break+0x1f1/0x270 [cifs]
[<ffffffff810a881a>] process_one_work+0x17a/0x440
[<ffffffff810a8d74>] rescuer_thread+0x294/0x3c0
...
```

解决方案：

-   使用cache=none重新挂载（性能会受影响）。
-   升级云服务器ECS（Linux）的操作系统。

