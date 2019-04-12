# Performance issues of Server Message Block {#concept_e1j_kls_bhb .concept}

## Latency issues before you perform I/O operations {#section_lkc_4ls_bhb .section}

When you access a Server Message Block \(SMB\) server by using a mount point, you need to wait for several minutes before performing I/O operations.

What can I do to reduce the waiting period when accessing an SMB server?

## Solutions {#section_shp_3ns_bhb .section}

The waiting period that occurs is mainly caused by an NFS client or Web client.

-   Check whether an NFS client is installed. If the NFS client is no longer used, we recommend that you delete it.
-   Locate the following registry key. The path to the registry key is: `HKEY_LOCAL_MACHINE->System->CurrentControlSet->Control->NetworkProvider->Order-> ProviderOrder`.

    Assume that the value of the ProviderOrder key is `LanmanWorkstation,RDPNP,Nfsnp`. You need to remove `,Nfsnp` and restart the ECS instance.

-   When a Web client exists, this increases the latency when you access an SMB server by using a file manager. We recommend that you remove the Web client.

**Note:** When a client connects to an SMB server for the first time, the latency is higher than expected. Check whether you can communicate with the mount address of the SMB server by using the ping command, or check if the latency for the communication is as expected.

-   If a time-out error occurred while using the ping command, we recommend that you check the network settings.
-   If the latency is higher than expected, we recommend that you ping the IP address of the SMB server. When the latency to ping the IP address of a mount point is lower than the latency to ping the domain name of the mount point, the issue may be caused by the DNS settings. We recommend that you check the DNS settings.

## Procedure to solve performance issues {#section_sns_c4y_bhb .section}

1.  Modify the value of the ProviderOrder key. When the latency to access the SMB server is longer than usual, we recommend that you check this value.
2.  You can use fio to conduct a performance test to check the issue.

    ```
    fio.exe --name=./iotest1 --direct=1 --rwmixread=0 --rw=write --bs=4K --numjobs=1 --thread --iodepth=128 --runtime=300 --group_reporting --size=5G --verify=md5 --randrepeat=0 --norandommap --refill_buffers --filename=\\<mount point dns>\myshare\testfio1
    
    fio.exe --name=./iotest1 --direct=1 --rwmixread=0 --rw=write --bs=4K --numjobs=1 --thread --iodepth=128 --runtime=300 --group_reporting --size=5G --verify=md5 --randrepeat=0 --norandommap --refill_buffers --filename=\\<mount point dns>\myshare\testfio1
    ```

3.  For applications that use an SMB file system as data storage, try to perform read/write operations by using large data blocks. The smaller the data blocks, the more network resources are consumed. If you cannot modify the size of a data block, you can use BufferedOutputStream.

