# Mount an NFS file system in Linux {#concept_hpp_dkh_cfb .concept}

After installing an NFS client in Linux, you can mount an NFS file system to an ECS instance.

When you mount a NAS NFS file system to an ECS instance, you can use the DNS name of the file system or the target to which you want to mount the file system. The DNS name of the file system is automatically resolved to the IP address of the mount target in the available zone of the mounted ECS instance.

## Mounting command {#section_spc_nlh_cfb .section}

You can run either of the following commands to mount an NFS file system.

-   To mount an NFSv4 file system, run the following command:

    ``` {#codeblock_6k4_qjs_y1g}
    sudo mount -t nfs4 -o vers=4.0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id-xxxx.region.nas.aliyuncs.com:/ /mount-point
    						
    ```

    If you fail to mount the file system, run the following command:

    ``` {#codeblock_5zi_tqv_o0v}
    sudo mount -t nfs4 rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id-xxxx.region.nas.aliyuncs.com:/ /mount-point
    						
    ```

    **Note:** The value of the vers parameter varies with the client version. If an error occurs when you use `vers=4.0` in the command, use `vers=4`.

-   To mount an NFSv3 file system, run the following command:

    ``` {#codeblock_dnk_0rp_hhx}
    sudo mount -t nfs -o vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id-xxxx.region.nas.aliyuncs.com:/ /mount-point
    ```


## Parameter description {#section_rxj_mlh_cfb .section}

The following table describes the parameters used in the mounting command.

|Parameter|Description|
|:--------|:----------|
|**Domain name of the mount point**|Indicates the domain name of the mount point, which consists of information such as file-system-id,region and nas.aliyuncs.com. This parameter is automatically generated when you [Create a file system](reseller.en-US/Quick Start/Create a file system.md#) and does not need to be set manually.|
|**mount-point**|Indicates the mount point of the NAS file system, which can be the root directory "/" or any sub-directory in the NAS file system.|
|**vers**|Indicates the file system version. Only NFSv3 and NFSv4 are supported.|

You can specify multiple options when mounting a NAS file system. The options are separated by commas in the command. The following table describes the options.

|Option|Description|
|:-----|:----------|
|**rsize**|Specifies the size of data blocks. Data is read by blocks between the client and the file system deployed in the cloud. Recommended value: 1048576|
|**wsize**|Specifies the size of data blocks. Data is written by blocks between the client and the file system deployed in the cloud. Recommended value: 1048576|
|**hard**|Specifies whether the data transmission stops and waits for a temporarily unavailable file system to be recovered when you use the local application of a file stored in the file system. We recommended that you enable the hard parameter.|
|**timeo**|Specifies the time \(in 0.1 second\) that the NFS client waits for the response before resending a request to the NAS file system deployed in the cloud. Recommended value: 600|
|**retrans**|Specifies the number of times that the NFS client resends requests. Recommended value: 2|
|**noresvport**|Specifies that a new TCP port is used for network reconnection to ensure that the connection between the file system and the ECS instance will not be ended during network failure recovery. We recommend that you enable the noresvport parameter.|

**Note:** You must note the following points when configuring the mounting parameters:

-   If you have to modify the values of I/O parameters \(rsize and wsize\), we recommend that you set the parameters to the maximum value \(1048576\) to prevent performance degradation.
-   If you have to modify the value of the time-out parameter \(timeo\), we recommend that you set the parameter to a value not less than 150. The unit of the timeo parameter is 0.1 second. Therefore, the value 150 indicates that the actual time-out period is 15 seconds.
-   We recommend that you enable the hard option. If you do not enable the hard option, set the timeo parameter to a value not less than 150.
-   For other mounting options, use their respective default values. For example, do not modify the read or write buffer size or disable the attribute buffer because these operations result in performance degradation.

## View mounting information {#section_upk_f4h_cfb .section}

After the mounting succeeds, you can run the following command to view the mounted file system:

``` {#codeblock_ak1_a6y_3pg}
mount -l
```

You can also run the following command to view the capacity information about the mounted file system:

``` {#codeblock_lq3_pbw_soy}
df -h
```

