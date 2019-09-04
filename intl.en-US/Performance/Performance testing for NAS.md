# Performance testing for NAS {#concept_krf_y3s_qfb .concept}

You can use fio to measure the throughput and IOPS of NAS in performance testing.

## Performance testing in Linux {#section_g4z_xwb_bhb .section}

Before conducting a performance test, note the following points:

-   Ensure that sunrpc\_slot is properly configured. For more information, see [FAQs](../../../../reseller.en-US/FAQ/Scale and Performance/Why is the speed of access to an NFS file system from a Linux client limited to several Mbit__s?.md#).
-   The maximum throughput will not exceed the bandwidth of an ECS instance. If the bandwidth of an ECS instance is 1 Gbit/s, the maximum throughput can reach 125 Mbit/s.

The following common testing examples are provided for your reference.

**Note:** Note: The following estimated values are all based on testing results for a single ECS instance. To reach the performance metrics recommended by the [Network Attached Storage](https://www.aliyun.com/product/nas) official site, we recommend that you use multiple ECS instances to perform a test.

-   Perform a random read test to measure IOPS

    ``` {#codeblock_lqt_wjx_3tz}
    fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=libaio -sync=1 -rw=randread -bs=4K -size=1G -time_based -runtime=60 -name=Fio -directory=/mnt
    ```

    Estimated value: 14,000

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/156758713540406_en-US.png)

-   Perform a random write test to measure IOPS

    ``` {#codeblock_i0b_p0p_chb}
    fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=libaio -sync=1 -rw=randwrite -bs=4K -size=1G -time_based -runtime=60 -name=Fio -directory=/mnt
    ```

    Estimated value: 10,000

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/156758713640407_en-US.png)

-   Perform a random read test to measure throughput

    ``` {#codeblock_nqq_q82_mkj}
    fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=libaio -sync=1 -rw=randread -bs=1M -size=1G -time_based -runtime=60 -name=Fio -directory=/mnt
    ```

    -   Estimated value for NAS Capacity: 150 Mbit/s

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/156758713640408_en-US.png)

    -   Estimated value for NAS Performance: 300 Mbit/s
-   Perform a random write test to measure throughput

    ``` {#codeblock_74u_kab_9ud}
    fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=libaio -sync=1 -rw=randwrite -bs=1M -size=1G -time_based -runtime=60 -name=Fio -directory=/mnt
    ```

    -   Estimated value for NAS Capacity: 150 Mbit/s![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/156758713740409_en-US.png)
    -   Estimated value for NAS Performance: 600 Mbit/s

## Performance testing in Windows {#section_u51_rxb_bhb .section}

Assume that you mount a NAS file system on Z: and install fio to the path c:\\Program Files\\fio\\fio.exe.

-   Perform a random read test to measure IOPS

    ``` {#codeblock_5da_tvt_9x8}
    "c:\Program Files\fio\fio.exe" -name=Fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=windowsaio -sync=1 -rw=randread -bs=4K -size=1G -time_based -runtime=60 -group_reporting -directory=Z\:\
    ```

    Estimated value: 14,000

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/156758713540406_en-US.png)

-   Perform a random write test to measure IOPS

    ``` {#codeblock_al0_fkl_3zy}
    "c:\Program Files\fio\fio.exe" -name=Fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=windowsaio -sync=1 -rw=randwrite -bs=4K -size=1G -time_based -runtime=60 -group_reporting -directory=Z\:\
    ```

    Estimated value: 10,000

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/156758713640407_en-US.png)

-   Perform a random read test to measure throughput

    ``` {#codeblock_doy_qiz_19k}
    "c:\Program Files\fio\fio.exe" -name=Fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=windowsaio -sync=1 -rw=randread -bs=1M -size=1G -time_based -runtime=60 -group_reporting -directory=Z\:\
    ```

    -   Estimated value for NAS Capacity: 150 Mbit/s

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/156758713640408_en-US.png)

    -   Estimated value for NAS Performance: 300 Mbit/s
-   Perform a random write test to measure throughput

    ``` {#codeblock_gu4_k0t_2i1}
    "c:\Program Files\fio\fio.exe" -name=Fio -numjobs=1 -iodepth=128 -direct=1 -ioengine=windowsaio -sync=1 -rw=randwrite -bs=1M -size=1G -time_based -runtime=60 -group_reporting -directory=Z\:\
    ```

    -   Estimated value for NAS Capacity: 150 Mbit/s

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41408/156758713740409_en-US.png)

    -   Estimated value for NAS Performance: 600 Mbit/s

