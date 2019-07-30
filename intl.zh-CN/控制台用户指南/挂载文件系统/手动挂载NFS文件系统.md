# 手动挂载NFS文件系统 {#concept_hpp_dkh_cfb .task}

本文档介绍如何在Linux系统中安装NFS客户端并通过挂载命令挂载NFS文件系统。

## 前提条件 {#section_b22_6c8_4of .section}

1.  已创建文件系统，详情请参见[创建文件系统](cn.zh-CN/控制台用户指南/管理文件系统.md#section_5jo_0kj_jn5)。
2.  已添加挂载点，详情请参见[添加挂载点](cn.zh-CN/控制台用户指南/管理挂载点.md#section_6xi_a3u_zkq)。

## 步骤一：安装NFS客户端 {#section_kvj_d02_szj .section}

在Linux系统中将NFS文件系统挂载至云服务器ECS，您需要先安装NFS客户端。

1.  登录[云服务器ECS](https://ecs.console.aliyun.com/)。
2.  运行以下命令，安装NFS客户端。
    -   如果您使用CentOS、Redhat、Aliyun Linux操作系统，运行以下命令：

        ``` {#d7e458}
        sudo yum install nfs-utils
        ```

    -   如果您使用Ubuntu或Debian操作系统，运行以下命令：

        ``` {#d7e464}
        sudo apt-get update
        ```

        ``` {#d7e467}
        sudo apt-get install nfs-common
        ```

3.  修改同时发起的NFS请求数量， 详情请参见[如何修改同时发起的NFS请求数量](../cn.zh-CN/常见问题/一般性问题/如何修改同时发起的NFS请求数量.md#)。

    NFS客户端对于同时发起的NFS请求数量进行了控制，默认编译的内核中此参数值为2，严重影响性能。


## 步骤二：挂载NFS文件系统 {#section_spc_nlh_cfb .section}

您可以使用文件系统的DNS名称或挂载目标的DNS名称，将NFS文件系统挂载至云服务器ECS。文件系统的DNS名称会自动解析为所连接云服务器ECS的可用区中挂载目标的IP地址。

1.  登录[云服务器ECS](https://ecs.console.aliyun.com/)。
2.  挂载NFS文件系统。

    -   如果您使用的是容量型/性能型NAS，请参见以下命令进行挂载。
        -   如果您要挂载NFSv4文件系统，运行以下命令：

            ``` {#codeblock_r13_7ie_u65}
            sudo mount -t nfs -o vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
            									
            ```

            如果挂载失败，请尝试以下命令：

            ``` {#codeblock_hq6_l9e_62j}
            sudo mount -t nfs4 -o rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
            									
            ```

        -   如果您要挂载NFSv3文件系统，运行以下命令：

            ``` {#codeblock_2dp_8fn_rth}
            sudo mount -t nfs -o vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
            ```

    -   如果您使用的是极速型NAS，请参见以下命令进行挂载。

        ``` {#codeblock_c1t_wx4_aik}
        sudo mount -t nfs -o vers=3,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.extreme.nas.aliyuncs.com:/share /mnt
        ```

    挂载命令中的参数说明如下表所示：

    |参数|描述|
    |:-|:-|
    |**挂载点**| 挂载点包括挂载点域名和挂载点路径，请根据实际值替换。

    -   挂载点域名：添加挂载点时自动生成，无需手工配置。
    -   挂载点路径：挂载的目标地址，Linux 系统中的根目录”/”或任意子目录（如/mnt）。
 |
    |**vers**|文件系统版本。     -   容量型/性能型NAS：支持nfsv3和nfsv4。
    -   极速型NAS：支持nfsv3。
 |

    在挂载文件系统时，还可以选择多种挂载选项，这些选项使用逗号分隔列表的形式，具体选项与说明如下表所示：

    |选项|说明|
    |:-|:-|
    |**rsize**|定义数据块的大小，用于在您的客户端与云中的文件系统之间读取数据。建议值：1048576|
    |**wsize**|定义数据块的大小，用于在您的客户端与云中的文件系统之间写入数据。建议值：1048576|
    |**hard**|指定在NAS暂时不可用的情况下，使用文件系统上某个文件的本地应用程序时应停止并等待该文件系统恢复在线状态。建议启用该参数。|
    |**timeo**|指定时长（单位为 0.1 秒），即 NFS 客户端在重试向云中的文件系统发送请求之前等待响应的时间。建议值：600 分秒。|
    |**retrans**|指定NFS客户端应重试请求的次数。建议值：2|
    |**noresvport**|指定在网络重连时使用新的TCP端口，保障在网络发生故障恢复的时候不会中断连接。建议启用该参数。|

    **说明：** 配置参数时，应注意以下内容：

    -   如果您必须更改IO大小参数 （rsize和wsize），我们建议您尽可能使用最大值 （1048576），以避免性能下降。
    -   如果您必须更改超时参数 （timeo），我们建议您使用150或更大的值。该timeo参数的单位为分秒 （0.1 秒），因此150表示的时间为15秒。
    -   不建议使用soft选项，有数据一致性风险。如果您要使用soft选项，相关风险需由您自行承担。
    -   避免设置不同于默认值的任何其他挂载选项。如果更改读或写缓冲区大小或禁用属性缓存，会导致性能下降。
3.  执行`mount -l`命令，查看挂载结果。

    如果回显包含如下类似信息，说明挂载成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21207/156447328551407_zh-CN.png)

    挂载成功后，您还可以通过`df -h`命令，可以查看文件系统的当前容量信息。


