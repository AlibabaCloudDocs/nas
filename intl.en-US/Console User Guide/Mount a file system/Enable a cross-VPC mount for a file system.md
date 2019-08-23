# Enable a cross-VPC mount for a file system {#task_bnk_22m_xgb .task}

This topic describes how to enable a cross-VPC mount for a file system.

Typically, you can only mount a file system on an ECS instance that is hosted by the same VPC as that of the mount point. If the mount point and the ECS instance are not in the same VPC, you can use Cloud Enterprise Network \(CEN\) to establish a connection between both VPCs.

You can use CEN to establish a connection between different VPCs that are located in the same region. You can enable a cross-VPC mount for the file system after the connection is established.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/156654869739613_en-US.png)

1.  Create a CEN instance. 
    1.  Log on to the [CEN console](https://cen.console.aliyun.com/).
    2.  On the Instances page, click **Create CEN Instance**.
    3.  Configure the CEN instance. 

        ![Configure the CEN instance](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/156654869739616_en-US.png)

        |Name|Description|
        |----|-----------|
        |Name| The name of the CEN instance.

 The name must be 2 to 128 characters in length and start with a letter. A name can contain letters, digits, underscores \(\_\), and hyphens \(-\).

 |
        |Description| The description of the CEN instance.

 The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.

 |
        |Attach Network| You can attach networks owned by this account or a different account to a CEN instance. For more information, see [Networks](Networks../../SP_17/DNBACK1834571/EN-US_TP_3049.dita#task_1563531).

 |

2.  Attach a network. 
    1.  On the Instances page, locate the target instance, and click **Manage**.
    2.  On the Networks tab, click **Attach Network** to configure the network. 

        ![configure the network](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/156654869739622_en-US.png)

        |Name|Description|
        |----|-----------|
        |Account|Select the **Your Account** tab.|
        |Network Type|The type of network to be attached. Valid values: VPC, Virtual Border Router \(VBR\), and Cloud Connect Network \(CCN\). Select VPC.|
        |Region|The region that hosts the network. Select China \(Qingdao\).|
        |Networks|The name of the network to be attached. Select a VPC network.|

    3.  Repeat the preceding steps to attach another VPC network to the CEN instance to establish a connection between the two VPCs.
3.  Mount a file system. 
    -   For more information about how to mount an NFS file system on an ECS instance running Linux, see [Mount an NFS file system](intl.en-US/Console User Guide/Mount a file system/Mount an NFS file system.md#).
    -   For more information about how to mount an SMB file system on an ECS instance running Windows, see [Mount an SMB file system](intl.en-US/Console User Guide/Mount a file system/Mount an SMB file system.md#).

