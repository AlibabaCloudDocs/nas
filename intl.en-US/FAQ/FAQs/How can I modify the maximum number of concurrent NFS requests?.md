# How can I modify the maximum number of concurrent NFS requests? {#task_1130493 .task}

The maximum number of concurrent requests from an NFS client is limited to 2 by default, which reduces NFS performance. This topic describes how to modify the maximum number of concurrent NFS requests.

You can use one of the following methods to modify the maximum number of concurrent NFS requests. After using method 1 to modify the maximum number, you must restart the ECS instance. This may affect business continuity. You can use method 2 to modify the maximum number of concurrent NFS requests without restarting the ECS instance.

## Method 1 {#section_gz3_zjk_dtf .section}

1.  Install an NFS client. For more information, see [Install an NFS client](../../../../reseller.en-US/Console User Guide/Mount a file system/Mount an NFS file system in Linux.md#section_kvj_d02_szj).
2.  Use the following commands to modify the maximum number of concurrent NFS requests.

    ``` {#codeblock_wqw_zkk_90c}
    echo "options sunrpc tcp_slot_table_entries=128" >> /etc/modprobe.d/sunrpc.conf
    echo "options sunrpc tcp_max_slot_table_entries=128" >>  /etc/modprobe.d/sunrpc.conf
    ```

    **Note:** You only need to perform the modification once after the NFS client is installed for the first time with root permissions. Then, you do not need to repeat the modification.

3.  Use the following command to restart the ECS instance.

    ``` {#codeblock_y24_usz_mnv}
    reboot
    ```

4.  Mount a file system. For more information, see [Mount an NFS file system](../../../../reseller.en-US/Console User Guide/Mount a file system/Mount an NFS file system in Linux.md#section_spc_nlh_cfb).
5.  Use the following command to verify the modification results.

    If the returned value is 128, the maximum number is modified.

    ``` {#codeblock_n56_nt4_s76}
    cat /proc/sys/sunrpc/tcp_slot_table_entries
    ```


## Method 2 {#section_5dr_c0j_0lo .section}

1.  Install an NFS client. For more information, see [Install an NFS client](../../../../reseller.en-US/Console User Guide/Mount a file system/Mount an NFS file system in Linux.md#section_kvj_d02_szj).
2.  Use the following commands to modify the maximum number of concurrent NFS requests.

    ``` {#codeblock_fiu_vvi_wqh}
    echo "options sunrpc tcp_slot_table_entries=128" >> /etc/modprobe.d/sunrpc.conf
    echo "options sunrpc tcp_max_slot_table_entries=128" >>  /etc/modprobe.d/sunrpc.conf
    ```

    **Note:** You only need to perform the modification once after the NFS client is installed for the first time with root permissions. Then, you do not need to repeat the modification.

3.  Mount a file system. For more information, see [Mount an NFS file system](../../../../reseller.en-US/Console User Guide/Mount a file system/Mount an NFS file system in Linux.md#section_spc_nlh_cfb).
4.  Use the following command to modify the maximum number of concurrent NFS requests again.

    ``` {#codeblock_ef9_6rj_s5m}
    sysctl -w sunrpc.tcp_slot_table_entries=128
    ```

5.  Unmount a file system. For more information, see [../../../../dita-oss-bucket/SP\_111/DNnas1882233/EN-US\_TP\_21508.md\#](../../../../reseller.en-US/Console User Guide/Unmount a file system/Unmount a file system in Linux.md#).
6.  Re-mount a file system. For more information, see [Mount an NFS file system](../../../../reseller.en-US/Console User Guide/Mount a file system/Mount an NFS file system in Linux.md#section_spc_nlh_cfb).
7.  Use the following command to verify the modification results.

    If the returned value is 128, the maximum number is modified.

    ``` {#codeblock_1fv_0iu_m9m}
    cat /proc/sys/sunrpc/tcp_slot_table_entries
    ```


