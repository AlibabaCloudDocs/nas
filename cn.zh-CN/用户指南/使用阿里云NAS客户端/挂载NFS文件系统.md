# 挂载NFS文件系统 {#concept_287083 .concept}

本文介绍在安装阿里云 NAS 客户端后，如何通过 Linux 命令挂载 NFS 文件系统。您可以选择手动挂载，也可以修改 ECS 实例中的配置文件，使其开机自动挂载。

## 手动挂载 {#section_7md_wv8_5t7 .section}

1.  挂载NFS文件系统。

    -   如果要挂载的是 vers=4.0 版本的文件系统，执行以下命令：

        其中file-system-id-xxxx.region.nas.aliyuncs.com:/ /mount-point请根据实际值替换。

        sudo mount -t alinas -o vers=4.0 file-system-id-xxxx.region.nas.aliyuncs.com:/ /mount-point

        **说明：** 

        不指定任何协议版本时，会默认使用 v4.0 进行挂载。

        挂载时，NAS 客户端会默认使用最佳挂载选项，您也可以参见下面表格添加选项。

    -   如果要挂载的是 vers=3 版本的文件系统，执行以下命令：

        其中file-system-id-xxxx.region.nas.aliyuncs.com:/ /mount-point请根据实际值替换。

        sudo mount -t alinas -o vers=3 file-system-id-xxxx.region.nas.aliyuncs.com:/ /mount-point

    挂载命令中的参数说明如下表所示：

    |参数|描述|
    |:-|:-|
    |**挂载点域名**|在[创建文件系统](../../../../cn.zh-CN/快速配置指南/创建文件系统.md#)时自动生成的挂载点域名，由file-system-id,region和nas.aliyuncs.com等信息组成，无需手工配置。 更多挂载点详情请参见[添加挂载点](../../../../cn.zh-CN/快速配置指南/添加挂载点.md#)。

 |
    |**mount-point**|NAS 挂载点，可以是 NAS 文件系统的根目录“/”或任意子目录。|
    |**vers**|文件系统版本，目前只支持 vers=3 和 vers=4.0。|

    在挂载文件系统时，还可以选择多种挂载选项，这些选项使用逗号分隔列表的形式，具体选项与说明如下表所示：

    |选项|说明|
    |:-|:-|
    |**rsize**|定义数据块的大小，用于在您的客户端与云中的文件系统之间读取数据。默认值：1048576|
    |**wsize**|定义数据块的大小，用于在您的客户端与云中的文件系统之间写入数据。默认值：1048576|
    |**hard**|指定在 NAS 暂时不可用的情况下，使用文件系统上某个文件的本地应用程序时应停止并等待该文件系统恢复在线状态。默认启用该参数。|
    |**timeo**|指定时长 \(单位为 0.1 秒\)，即 NFS 客户端在重试向云中的文件系统发送请求之前等待响应的时间。默认值：600 分秒。|
    |**retrans**|指定 NFS 客户端应重试请求的次数。默认值：2|

2.  执行df -h命令，检查挂载是否成功。

    若显示如下信息，则表示挂载成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/236142/155867892147837_zh-CN.png)


## 自动挂载 {#section_s7u_7v7_g7i .section}

在/etc/fstab文件中，添加如下脚本，开启自动挂载。其中file-system-id-xxxx.region.nas.aliyuncs.com请根据实际值替换。

 vi /etc/fstab 

``` {#codeblock_61t_yco_ld8}
file-system-id-xxxx.region.nas.aliyuncs.com local-mount-point alinas _netdev 0 0
```

## 问题定位 {#section_a2n_sn9_1lw .section}

Ubuntu 18.04 操作系统默认的 DNS 服务存在缺陷，导致安装在 Ubuntu 18.04 操作系统上的阿里云 NAS 客户端无法正常挂载 NFS 文件系统。若您的操作系统为此版本时，请关闭 systemd-resolve 的域名解析服务再执行挂载操作。

mv /etc/resolv.conf /etc/resolv.conf.bak

cp /run/systemd/resolve/resolv.conf /etc/

