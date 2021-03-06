# 挂载极速型NAS {#task_1079076 .task}

本文档介绍如何快速创建文件系统，并将其挂载至云服务器ECS（Linux系统）上。

1.  已注册阿里云账号，并完成实名认证。

    如果没有，请先注册阿里云账号，详情请参见[阿里云账号注册流程](../../../../cn.zh-CN/.md#)。

2.  已开通NAS服务。

    首次登录[NAS控制台](https://nas.console.aliyun.com/)时，根据页面提示开通NAS服务。

3.  已完成云资源访问授权。

    首次使用极速型NAS时，根据页面提示，完成AliyunNASMangeENIRole角色授权。

    **说明：** 目前只支持主账号使用极速型NAS。

    ![云资源访问授权](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/868664/156896713751079_zh-CN.png)

4.  在需要创建文件系统的地域，已有可用的专有网络VPC。

    如果没有，请创建专有网络VPC，详情请参见[创建专有网络和交换机](创建专有网络和交换机../../SP_22/DNVPC11885991/ZH-CN_TP_2434.dita#concept_isl_ghv_rdb/section_ufw_rhv_rdb)。

5.  在需要创建文件系统的地域，已有可用的云服务器ECS，并将此云服务器ECS归属到已创建的专有网络VPC下。

    如果没有，请购买云服务器ECS，详情请参见[创建ECS实例](../../../../cn.zh-CN/个人版快速入门/创建ECS实例.md#)。


## 步骤一：创建文件系统 {#section_4fn_6z2_1ly .section}

1.  登录[NAS控制台](https://nas.console.aliyun.com/)。
2.  选择**极速型NAS** \> **文件系统列表**，单击**创建文件系统**。
3.  在创建文件系统页面，配置相关参数。 此处以极速型NAS（按量后付费）为例。 

    |参数|说明|
    |--|--|
    |地域| 选择要创建文件系统的地域。

**说明：** 不同地域的文件系统与云服务器ECS不互通。

 |
    |可用区| 可用区是指在同一地域内，电力和网络互相独立的物理区域。

 单击下拉框选择可用区，建议和云服务器ECS在同一可用分区。

**说明：** 同一地域不同可用区之间的文件系统与云服务器ECS互通。

 |
    |协议| 选择**NFS**。

**说明：** 极速型NAS只支持NFS v3。

 |
    |类型| 包括**标准型**和**高级型**。

 |
    |容量| 选择合适的容量。

 |
    |吞吐| 选择合适的吞吐。

 |

4.  单击**确定**，创建文件系统。

## 步骤二：添加挂载点 {#section_isv_j9n_awm .section}

在文件存储NAS中，需要通过挂载点将文件系统挂载至云服务器ECS。极速型NAS只支持专有网络类型的挂载点，具体操作如下所示。

**说明：** 每个文件系统最多可添加1个挂载点。

1.  登录[NAS控制台](https://nas.console.aliyun.com/)。
2.  选择**极速型NAS** \> **文件系统列表**。
3.  找到目标文件系统，单击**添加挂载点**。
4.  在**添加挂载点**页面，配置相关参数。 

    |参数|说明|
    |--|--|
    |VPC网络| 选择已创建的VPC网络。如果还未创建 ，请单击[点击前往VPC控制创建VPC网络](https://vpc.console.aliyun.com/)进行创建。

**说明：** 必须与云服务器ECS选择一样的VPC网络和交换机。

 |
    |交换机| 选择VPC网络下创建的交换机。

 |
    |权限组| 选择**VPC 默认权限组（全部允许）**或已创建的权限组。

**说明：** 初始情况下，每个账号都会自动生成一个VPC默认权限组，允许同一VPC环境下的任何IP地址都可以通过该挂载点访问文件系统。如果您要创建权限组，详情请参见[管理权限组](../../../../cn.zh-CN/控制台用户指南/管理权限/管理权限组.md#)。

 |

5.  单击**确定**，创建挂载点。

## 步骤三：安装NFS客户端 {#section_mvh_b2e_ri3 .section}

在Linux系统中将NFS文件系统挂载至云服务器ECS，您需要先安装NFS客户端。

1.  登录[云服务器ECS](https://ecs.console.aliyun.com/)。
2.  运行以下命令，安装NFS客户端。 
    -   如果您使用CentOS、Redhat、Aliyun Linux操作系统，运行以下命令：

        ``` {#d6e491}
        sudo yum install nfs-utils
        ```

    -   如果您使用Ubuntu或Debian操作系统，运行以下命令：

        ``` {#d6e497}
        sudo apt-get update
        ```

        ``` {#d6e500}
        sudo apt-get install nfs-common
        ```

3.  修改同时发起的NFS请求数量， 详情请参见[如何修改同时发起的NFS请求数量](../../../../cn.zh-CN/常见问题/规模与性能/如何修改同时发起的NFS请求数量.md#)。 NFS客户端对于同时发起的NFS请求数量进行了控制，默认编译的内核中此参数值为2，严重影响性能。

## 步骤四：挂载文件系统 {#section_6ig_f8k_s6o .section}

您可以使用文件系统的DNS名称或挂载目标的DNS名称，将NFS文件系统挂载至云服务器ECS。文件系统的DNS名称会自动解析为所连接云服务器ECS的可用区中挂载目标的IP地址。

1.  登录[云服务器ECS](https://ecs.console.aliyun.com/)。
2.  挂载NFS文件系统。 

    ``` {#codeblock_ft8_kd0_x8u}
    sudo mount -t nfs -o vers=3,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.extreme.nas.aliyuncs.com:/share /mnt
    ```

    如果执行挂载命令报错，请参见[挂载失败的排查与处理方法](../../../../cn.zh-CN/控制台用户指南/挂载文件系统/挂载失败的排查与处理方法.md#)进行排查。

    挂载命令中的参数说明如下表所示：

    |参数|描述|
    |:-|:-|
    |挂载点| 挂载点包括挂载点域名和挂载点路径，请根据实际值替换。

    -   挂载点域名：添加挂载点时自动生成，无需手工配置。
    -   挂载点路径：挂载的目标地址，Linux 系统中的根目录（/）或任意子目录（如/mnt）。
 |
    |vers|文件系统版本，目前只支持nfs v3。|
    |挂载选项| 挂载文件系统时，可选择多种挂载选项，详情请参见[手动挂载NFS文件系统](../../../../cn.zh-CN/控制台用户指南/挂载文件系统/手动挂载NFS文件系统.md#)中的[挂载选项说明表](cn.zh-CN/控制台用户指南/挂载文件系统/手动挂载NFS文件系统.md#table_2uc_odz_vk9)。

 |

3.  执行`mount -l`命令，查看挂载结果。 

    如果回显包含如下类似信息，说明挂载成功。

    ![查看挂载结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/868664/156896713851085_zh-CN.png)

4.  挂载成功后，您可以在ECS上访问NAS文件系统，执行读取或写入操作。 

    您可以把NAS文件系统当作一个普通的目录来访问和使用，例子如下：

    ![读写操作](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18690/156896713854347_zh-CN.png)


## 常见错误排查 {#section_se8_r5u_jkl .section}

如果挂载失败，请参见[挂载失败的排查与处理方法](../../../../cn.zh-CN/控制台用户指南/挂载文件系统/挂载失败的排查与处理方法.md#)进行排查。

