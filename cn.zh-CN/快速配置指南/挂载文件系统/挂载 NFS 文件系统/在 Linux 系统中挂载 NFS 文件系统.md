# 在 Linux 系统中挂载 NFS 文件系统 {#concept_hpp_dkh_cfb .concept}

本文介绍在 Linux 系统中安装 NFS 客户端后，如何通过 Linux 挂载命令挂载 NFS 文件系统。

您可以使用文件系统的 DNS 名称或挂载目标的 DNS 名称，将 NAS 的 NFS 文件系统挂载至 ECS 实例。文件系统的 DNS 名称会自动解析为所连接 ECS 实例的可用区中挂载目标的 IP 地址。

## 挂载 NFS 文件系统命令 {#section_spc_nlh_cfb .section}

您可以运行以下命令，挂载 NFS 文件系统：

-   如果要挂载的是 NFSv4 文件系统，运行以下命令：

    ```
    sudo mount -t nfs -o vers=4.0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id-xxxx.region.nas.aliyuncs.com:/ /mount-point
    
    ```

    **说明：** 不同版本的客户端，挂载文件系统命令中使用的vers参数不同。如果输入`vers=4.0`出错，请使用`vers=4`。

-   如果要挂载的是 NFSv3 文件系统，运行以下命令：

    ```
    sudo mount -t nfs -o vers=3,nolock,proto=tcp, rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id-xxxx.region.nas.aliyuncs.com:/ /mount-point
    ```


## 参数说明 {#section_rxj_mlh_cfb .section}

挂载命令中的参数说明如下表所示：

|参数|描述|
|:-|:-|
|**挂载点域名**|在[创建文件系统](cn.zh-CN/快速配置指南/创建文件系统.md#)时自动生成的挂载点域名，由file-system-id,region和nas.aliyuncs.com等信息组成，无需手工配置。更多挂载点详情请参见[添加挂载点](cn.zh-CN/快速配置指南/添加挂载点.md#)。

|
|**mount-point**|NAS 挂载点，可以是 NAS 文件系统的根目录“/”或任意子目录。|
|**vers**|文件系统版本，目前只支持 nfsv3 和 nfsv4。|

在挂载文件系统时，还可以选择多种挂载选项，这些选项使用逗号分隔列表的形式，具体选项与说明如下表所示：

|选项|说明|
|:-|:-|
|**rsize**|定义数据块的大小，用于在您的客户端与云中的文件系统之间读取数据。建议值：1048576|
|**wsize**|定义数据块的大小，用于在您的客户端与云中的文件系统之间写入数据。建议值：1048576|
|**hard**|指定在 NAS 暂时不可用的情况下，使用文件系统上某个文件的本地应用程序时应停止并等待该文件系统恢复在线状态。建议启用该参数。|
|**timeo**|指定时长 \(单位为 0.1 秒\)，即 NFS 客户端在重试向云中的文件系统发送请求之前等待响应的时间。建议值：600 分秒。|
|**retrans**|指定 NFS 客户端应重试请求的次数。建议值：2|
|**noresvport**|指定在网络重连时使用新的 TCP 端口，保障在网络发生故障恢复的时候不会中断连接。建议启用该参数。|

**说明：** 配置参数时，应注意以下内容：

-   如果您必须更改 IO 大小参数 \(rsize 和 wsize\)，我们建议您尽可能使用最大值 \(1048576\)，以避免性能下降。
-   如果您必须更改超时参数 \(timeo\)，我们建议您使用 150 或更大的值。该 timeo 参数的单位为分秒 \(0.1 秒\)，因此 150 表示的时间为 15 秒。
-   建议您使用硬挂载选项。但是，如果您使用软挂载，则需要将 timeo 参数至少设置为 150 分秒。
-   避免设置不同于默认值的任何其他挂载选项。例如，更改读或写缓冲区大小，或禁用属性缓存，会导致性能下降。

## 查看挂载的 NFS 文件系统信息 {#section_upk_f4h_cfb .section}

挂载完成后，您可以运行以下命令查看已挂载的文件系统：

```
mount -l
```

您也可以查看已挂载文件系统的当前容量信息：

```
df -h
```

## 挂载文件系统参考信息 {#section_hcg_smv_fgb .section}

-   [挂载前注意事项](cn.zh-CN/快速配置指南/挂载文件系统/挂载前注意事项.md#)
-   [在Windows系统中挂载NFS文件系统](cn.zh-CN/快速配置指南/挂载文件系统/挂载 NFS 文件系统/在Windows系统中挂载NFS文件系统.md#)
-   [挂载 SMB 文件系统](cn.zh-CN/快速配置指南/挂载文件系统/挂载 SMB 文件系统.md#)

