# 如何修改同时发起的NFS请求数量 {#task_1130493 .task}

NFS客户端对于同时发起的NFS请求数量进行了控制，默认编译的内核中此参数值为2，严重影响性能。本文介绍如何修改同时发起的NFS请求数量。

您可以通过以下两种方法修改同时发起的NFS请求数量。使用方法一修改完成后，需要重启服务器ECS，重启服务器可能影响您的业务使用。如果您不想重启服务器，可以使用方法二修改同时发起的NFS请求数量。

## 方法一 {#section_gz3_zjk_dtf .section}

1.  安装NFS客户端，详情请参见[安装NFS客户端](../../../../intl.zh-CN/控制台用户指南/挂载文件系统/手动挂载NFS文件系统.md#section_kvj_d02_szj)。
2.  执行以下命令，修改同时发起的NFS请求数量。 

    ``` {#codeblock_7iq_273_t1n}
    echo "options sunrpc tcp_slot_table_entries=128" >> /etc/modprobe.d/sunrpc.conf
    echo "options sunrpc tcp_max_slot_table_entries=128" >>  /etc/modprobe.d/sunrpc.conf
    ```

    **说明：** 您只需在首次安装NFS客户端后执行一次此操作（必须通过root用户操作），之后无需重复执行。

3.  重启云服务器ECS。 

    ``` {#codeblock_932_evh_gmk}
    reboot
    ```

4.  挂载文件系统，详情请参见[挂载NFS文件系统](../../../../intl.zh-CN/控制台用户指南/挂载文件系统/手动挂载NFS文件系统.md#section_spc_nlh_cfb)。
5.  执行以下命令查看修改结果。 

    如果返回值为128，则说明修改成功。

    ``` {#codeblock_31s_oz1_kxo}
    cat /proc/sys/sunrpc/tcp_slot_table_entries
    ```


## 方法二 {#section_5dr_c0j_0lo .section}

1.  安装NFS客户端，详情请参见[安装NFS客户端](../../../../intl.zh-CN/控制台用户指南/挂载文件系统/手动挂载NFS文件系统.md#section_kvj_d02_szj)。
2.  执行以下命令，修改同时发起的NFS请求数量。 

    ``` {#codeblock_iaq_91x_u7p}
    echo "options sunrpc tcp_slot_table_entries=128" >> /etc/modprobe.d/sunrpc.conf
    echo "options sunrpc tcp_max_slot_table_entries=128" >>  /etc/modprobe.d/sunrpc.conf
    ```

    **说明：** 您只需在首次安装NFS客户端后执行一次此操作（必须通过root用户操作），之后无需重复执行。

3.  挂载文件系统，详情请参见[挂载NFS文件系统](../../../../intl.zh-CN/控制台用户指南/挂载文件系统/手动挂载NFS文件系统.md#section_spc_nlh_cfb)。
4.  执行以下命令，再次修改同时发起的NFS请求数量。 

    ``` {#codeblock_tlt_4sn_2kj}
    sysctl -w sunrpc.tcp_slot_table_entries=128
    ```

5.  卸载文件系统，详情请参见[在Linux系统中卸载文件系统](../../../../intl.zh-CN/控制台用户指南/卸载文件系统/在Linux系统中卸载文件系统.md#)。
6.  重新挂载文件系统，详情请参见[挂载NFS文件系统](../../../../intl.zh-CN/控制台用户指南/挂载文件系统/手动挂载NFS文件系统.md#section_spc_nlh_cfb)。
7.  执行以下命令查看修改结果。 

    如果返回值为128，则说明修改成功。

    ``` {#codeblock_at8_dt0_gr1}
    cat /proc/sys/sunrpc/tcp_slot_table_entries
    ```


