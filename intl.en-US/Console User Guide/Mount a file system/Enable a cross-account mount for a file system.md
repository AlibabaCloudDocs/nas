# Enable a cross-account mount for a file system {#task_tkk_hdn_xgb .task}

This topic describes how to enable a cross-account mount for a file system.

By default, you can only mount a file system on an ECS instance that is owned by the same account as that of the file system. Assume that you have multiple Alibaba Cloud accounts and want to allow mutual access between a file system and an ECS instance from different accounts. At this point, you must establish a connection between VPCs that host the file system and the ECS instance respectively.

You can use Alibaba Cloud Cloud Enterprise Network \(CEN\) to connect VPCs owned by different accounts.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132369/156654837539653_en-US.png)

1.  Create a CEN instance by using Account A. 
    1.  Log on to the [CEN console](https://cen.console.aliyun.com/).
    2.  On the Instances page, click **Create CEN Instance**.
    3.  Configure the CEN instance. 

        ![Configure the CEN instance](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/156654837639616_en-US.png)

        |Name|Description|
        |----|-----------|
        |Name| The name of the CEN instance.

 The name must be 2 to 128 characters in length and start with a letter. A name can contain letters, digits, underscores \(\_\), and hyphens \(-\).

 |
        |Description| The description of the CEN instance.

 The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.

 |
        |Attach Network| You can attach networks owned by this account or a different account to a CEN instance. For more information, see [../../SP\_17/DNBACK1834571/EN-US\_TP\_3049.dita\#task\_1563531](../../SP_17/DNBACK1834571/EN-US_TP_3049.dita#task_1563531).

 |

    4.  Retrieve the ID of the new CEN instance, which is cbn-xxxxxxxxxx4l7.
2.  Authorize Account A to attach a network owned by Account B. 
    1.  Log on to the [VPC console](https://vpcnext.console.aliyun.com/) by using Account B.
    2.  In the left-side navigation pane, select **VPCs**.
    3.  Locate the target VPC, and click **Manage**.
    4.  On the VPC Details page, locate the CEN cross-account authorization information section, and click **CEN Cross-Account Authorization**.
    5.  In the Attach to CEN dialog box, enter the Peer Account UID and Peer Account CEN ID, and click **OK**. 

        ![attach to CEN](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132369/156654837639688_en-US.png)

3.  Attach a network by using Account A. 
    1.  Log on to the [CEN console](https://cen.console.aliyun.com/) by using Account A.
    2.  On the Instances page, locate the target instance, and click **Manage**.
    3.  On the Networks tab, click **Attach Network** to configure the network. 

        ![configure the network](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132369/156654837639689_en-US.png)

        |Name|Description|
        |----|-----------|
        |Account|Select **Different Account** tab.|
        |Owner Account|The ID of the account that owns the target network. Enter the ID of Account B.|
        |Network Type|The type of network to be attached. Valid values: VPC, Virtual Border Router \(VBR\), and Cloud Connect Network \(CCN\). Select VPC.|
        |Region|The region that hosts the network.|
        |Networks|The name of the network to be attached.|

    4.  After the configuration is complete, click **OK**.
4.  Mount a file system. 
    -   For more information about how to mount an NFS file system on an ECS instance running Linux, see [Mount an NFS file system](reseller.en-US/Console User Guide/Mount a file system/Mount an NFS file system.md#).
    -   For more information about how to mount an SMB file system on an ECS instance running Windows, see [Mount an SMB file system](reseller.en-US/Console User Guide/Mount a file system/Mount an SMB file system.md#).

