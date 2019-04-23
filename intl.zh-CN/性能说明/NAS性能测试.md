# NAS性能测试 {#concept_krf_y3s_qfb .concept}

您可以使用 FIO 进行吞吐和 IOPS 的性能测试。

## Linux 系统下的性能测试 {#section_g4z_xwb_bhb .section}

性能测试前，请注意以下事项：

-   确认sunrpc\_slot设置正确，详情请参考[常见问题](../../../../intl.zh-CN/常见问题/一般性问题/linux上NFS性能只有几MB速度.md#)文档说明。
-   吞吐最大不会超过 ECS 带宽。如果您的 ECS 带宽只有 1Gbps，则吞吐最大可达到 125MB/s。

如下提供一些通用的性能测试样例。

**说明：** 以下提供的预估值均为单台 ECS 测试的结果。要达到[文件存储 NAS](https://www.aliyun.com/product/nas) 官网性能指标，建议使用多台 ECS 进行测试。

-   随机读 IOPS 设置

    ```
    fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=libaio -sync=1 -rw=randread -bs=4K -size=1G -time_based -runtime=60 -name=Fio -directory=/mnt
    ```

    单机预估值：14k

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/155600167540406_zh-CN.png)

-   随机写 IOPS 设置

    ```
    fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=libaio -sync=1 -rw=randwrite -bs=4K -size=1G -time_based -runtime=60 -name=Fio -directory=/mnt
    ```

    单机预估值：10k

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/155600167640407_zh-CN.png)

-   随机读吞吐

    ```
    fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=libaio -sync=1 -rw=randread -bs=1M -size=1G -time_based -runtime=60 -name=Fio -directory=/mnt
    ```

    -   容量型单机预估值：150MB

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/155600167640408_zh-CN.png)

    -   性能型单机预估值：300MB
-   随机写吞吐

    ```
    fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=libaio -sync=1 -rw=randwrite -bs=1M -size=1G -time_based -runtime=60 -name=Fio -directory=/mnt
    ```

    -   容量型单机预估值：150MB![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/155600167740409_zh-CN.png)
    -   性能型单机预估值：600MB

## Windows 系统下的性能测试 {#section_u51_rxb_bhb .section}

假设 NAS 挂载到 Z：，fio 安装到 c:\\Program Files\\fio\\fio.exe 

-   随机读 IOPS 设置

    ```
    "c:\Program Files\fio\fio.exe" -name=Fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=windowsaio -sync=1 -rw=randread -bs=4K -size=1G -time_based -runtime=60 -group_reporting -directory=Z\:\
    ```

    单机预估值：14k

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/155600167540406_zh-CN.png)

-   随机写 IOPS 设置

    ```
    "c:\Program Files\fio\fio.exe" -name=Fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=windowsaio -sync=1 -rw=randwrite -bs=4K -size=1G -time_based -runtime=60 -group_reporting -directory=Z\:\
    ```

    单机预估值：10k

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/155600167640407_zh-CN.png)

-   随机读吞吐

    ```
    "c:\Program Files\fio\fio.exe" -name=Fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=windowsaio -sync=1 -rw=randread -bs=1M -size=1G -time_based -runtime=60 -group_reporting -directory=Z\:\
    ```

    -   容量型单机预估值：150MB

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/155600167640408_zh-CN.png)

    -   性能型单机预估值：300MB
-   随机写吞吐

    ```
    "c:\Program Files\fio\fio.exe" -name=Fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=windowsaio -sync=1 -rw=randwrite -bs=1M -size=1G -time_based -runtime=60 -group_reporting -directory=Z\:\
    ```

    -   容量型单机预估值：150MB

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/155600167740409_zh-CN.png)

    -   性能型单机预估值：600MB

