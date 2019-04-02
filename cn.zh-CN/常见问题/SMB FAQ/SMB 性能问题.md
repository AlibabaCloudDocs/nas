# SMB 性能问题 {#concept_e1j_kls_bhb .concept}

## 开始 IO 操作前的延迟问题 {#section_lkc_4ls_bhb .section}

当通过挂载点地址直接访问 SMB 服务器，在开始 IO 操作之前会有几分钟的等待时间。

应该通过什么操作减少访问时的等待时间？

## 解决方案 {#section_shp_3ns_bhb .section}

产生等待时间主要是 NFS Client 或 WebClient 造成的。

-   是否安装 NFS Client，如果用不到 NFS 服务，请删除。
-   查看注册表配置项。注册表路径：`HKEY_LOCAL_MACHINE->System->CurrentControlSet->Control->NetworkProvider->Order-> ProviderOrder`。

    比如，注册值为 ` LanmanWorkstation,RDPNP,Nfsnp`，请删除`,Nfsnp`，然后重启 ECS。

-   如果存在 webclient， 也会影响到文件浏览器登录 smb 服务，请删除。

**说明：** 客户端初次连接 SMB 服务器较慢时，可以 ping 挂载地址查看能否 ping 通，或者查看延时是否正。

-   无法 ping 通，请检查您的网络设置。
-   如果延时较长，请 ping 挂载 ip。如果 ping ip 比 ping dns 延时小很多，可能是 DNS 问题，请检查您的配置。

## 关于性能问题的解决步骤 {#section_sns_c4y_bhb .section}

1.  查看修改ProviderOrder的注册表值。初次访问等待时间久时，请先检查该值。
2.  使用 fio 进行性能测试，查看有无异常。

    ```
    fio.exe --name=./iotest1 --direct=1 --rwmixread=0 --rw=write --bs=4K --numjobs=1 --thread --iodepth=128 --runtime=300 --group_reporting --size=5G --verify=md5 --randrepeat=0 --norandommap --refill_buffers --filename=\\<mount point dns>\myshare\testfio1
    
    fio.exe --name=./iotest1 --direct=1 --rwmixread=0 --rw=write --bs=4K --numjobs=1 --thread --iodepth=128 --runtime=300 --group_reporting --size=5G --verify=md5 --randrepeat=0 --norandommap --refill_buffers --filename=\\<mount point dns>\myshare\testfio1
    ```

3.  查看程序，尽量以大数据块进行 IO 读写。如果数据块较小，会消耗更多的网络资源。如果不能修改数据块大小，可以使用BufferedOutputStream。

