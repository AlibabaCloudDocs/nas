# 安装阿里云NAS客户端 {#concept_287082 .task}

阿里云 NAS 客户端为 Linux 系统提供了 NFS 文件系统的挂载与访问服务。通过阿里云 NAS 客户端挂载 NFS 文件系统，可以避免因为网络抖动引起的 IO 卡顿问题，为用户带来更好的使用体验。

阿里云 NAS 客户端会占用您机器上的本地端口 60000，请确保此端口可用。

目前，阿里云 NAS 客户端支持以下操作系统。

-   CentOS 6.x
-   CentOS 7.x
-   Ubuntu 14.04
-   Ubuntu 16.04
-   Ubuntu 18.04
-   Debian 8.9
-   Debian 9.2

阿里云 NAS 客户端依赖以下软件包（在安装阿里云 NAS 客户端时自动安装）。

-   NFS Client（nfs-utils 或者 nfs-common）
-   Python（2.6.x 或者 2.7.x）
-   Haproxy（任意版本）

不同的操作系统，有不同的安装命令，请根据您的操作系统选择合适的安装命令。

## 安装CentOS {#section_gfr_v90_7l0 .section}

1.  配置软件源。 
    -   如果您使用 CentOS 6.x 操作系统，请执行以下命令配置软件源。

        ``` {#codeblock_u20_l5t_nwd}
        wget -O /etc/yum.repos.d/alinas.repo http://mirrors.aliyun.com/opsx/alinas/centos6.repo
        ```

    -   如果您使用 CentOS 7.x 操作系统，请执行以下命令配置软件源。

        ``` {#codeblock_jp0_g83_19c}
        wget -O /etc/yum.repos.d/alinas.repo http://mirrors.aliyun.com/opsx/alinas/centos7.repo
        ```

2.  更新软件源。 

    ``` {#codeblock_5qq_vko_xk2}
    sudo yum update
    ```

3.  安装阿里云 NAS 客户端。 

    ``` {#codeblock_er3_bfa_8yf}
    sudo yum install aliyun-alinas-utils
    ```

4.  检查安装结果。 

    执行如下命令，如果输出帮助信息，则说明安装成功。

    ``` {#codeblock_cvo_n87_r84}
    /sbin/mount.alinas –h
    ```


## 安装Ubuntu/Debian {#section_uzg_y2p_bco .section}

1.  配置软件源。 

    ``` {#codeblock_04m_59o_ckg}
    curl http://mirrors.aliyun.com/opsx/alinas/opsx@service.alibaba.com.gpg.key | apt-key add -
    ```

    ``` {#codeblock_0yi_2aj_zqv}
    curl -o /etc/apt/sources.list.d/alinas.list http://mirrors.aliyun.com/opsx/alinas/ubuntu.list
    ```

2.  更新软件源。 

    ``` {#codeblock_z39_j4z_2l5}
    sudo apt update
    ```

3.  安装阿里云 NAS 客户端。 

    ``` {#codeblock_xoq_jq6_2tl}
    sudo apt install aliyun-alinas-utils
    ```

4.  检查安装结果。 

    执行如下命令，如果输出帮助信息，则说明安装成功。

    ``` {#codeblock_1c8_55l_q9u}
    /sbin/mount.alinas –h
    ```


## 后续操作 {#section_65w_co2_ged .section}

当阿里云 NAS 客户端有更新时，您可以参见如下命令进行升级。

-   如果您使用 CentOS 操作系统，可以执行以下命令进行升级。

    ``` {#codeblock_28r_9rf_xq1}
    sudo yum update aliyun-alinas-utils
    ```

-   如果您使用 Ubuntu/Debian 操作系统，可以执行以下命令进行升级。

    ``` {#codeblock_cmb_ul0_vcm}
    sudo apt install --only-upgrade aliyun-alinas-utils
    ```


