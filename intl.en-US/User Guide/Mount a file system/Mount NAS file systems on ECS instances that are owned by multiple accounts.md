# Mount NAS file systems on ECS instances that are owned by multiple accounts {#task_tkk_hdn_xgb .task}

This section describes how to mount NAS file systems on ECS instances that are owned by multiple accounts.

By default, you can only mount NAS file systems on ECS instances that are in the same account. If data transit is required between ECS instances that are owned by multiple UID accounts in an enterprise account and a NAS file system, you only need to establish a connection between the VPC that the ECS instance is located and the VPC that the NAS file system is located. You can connect multiple VPCs by using Cloud Enterprise Network \(CEN\).

## Configure a connection between VPCs {#section_crp_jgn_xgb .section}

CEN enables connections between VPCs that belong to multiple accounts. After connections between VPCs are established, ECS instances that are in one VPC can access NAS file systems in another VPC, even if the VPCs belong to different accounts.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132369/156265508639653_en-US.png)

1.  Create a CEN instance using account A
    1.  Log on to the [CEN console](https://cen.console.aliyun.com/).
    2.  On the Instances page, click **Create CEN Instance**.
    3.  Configure the CEN instance as shown in the following figure.

        \[DO NOT TRANSLATE\]

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/156265508639616_en-US.png)

        The options are described as follows:

        |Option|Description|
        |------|-----------|
        |Name| Enter the name of the CEN instance.

 The name can be 2 to 128 characters in length and can contain numbers, letters, Chinese characters, hyphens \(-\), and underscores \(\_\). It must start with a letter or a Chinese character.

 |
        |Description| Enter the description of the CEN instance.

 The description can be 2 to 256 characters in length. It cannot start with `http://` or `https://`.

 |
        |Attach networks| You can attach networks in your account or another account to a CEN instance. For more information, see [Networks](https://www.alibabacloud.com/help/doc-detail/66001.htm).

 |

    4.  Obtain the ID of the new CEN instance.

        In this example, the CEN instance ID is cbn-xxxxxxxxxx4l7.

2.  Account B authorizes account A to attach its network instance

    On the VPC Details page, you can authorize another account to attach networks that are owned by the current account. Proceed as follows:

    1. Log on to the [VPC console](https://vpcnext.console.aliyun.com/) using account B.

    2. In the left-side navigation pane, select **VPCs**.

    3. Click the instance ID of the target VPC.

    4. In the CEN cross account authorization information section, click **CEN Cross Account Authorization**.

    In the Attach to CEN dialog box, enter Peer Account UID and Peer Account CEN ID, and then click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132369/156265508639688_en-US.png)

3.  Attach a network by using account A

    After the authorization is complete, you can attach a network as follows.

    1.  Log on to the [CEN console](https://cen.console.aliyun.com/) using account A.
    2.  On the Instances page, locate the newly created CEN and click **Manage** in the Actions column.
    3.  On the CEN page, click **Attach Network** to configure the network.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132369/156265508739689_en-US.png)

        The options are described as follows:

        |Option|Description|
        |------|-----------|
        |Account|Select **Different Account**.|
        |Owner Account|Enter a peer account ID. Enter the account ID of account B.|
        |Network Type|Select the type of network to attach to the instance. You can select one of the following values: VPC, Virtual Border Router \(VBR\), and CloudConnectNetwork \(CCN\). Select VPC.|
        |Region|The region where the network is located. Select China \(Qingdao\).|
        |Networks|Select a network to attach. Select a VPC instance.|

4.  Verify the mounting result

    Log on to the ECS instance to verify the mounting result.

    ``` {#codeblock_scb_veg_rby}
    [root@ ~]#sudo mount -t nfs -o vers=4.0,vpc2<the domain name of the mount point>:/ /mnt
    [root@iZbp18jc3nwxdiy5e1vkkaZ ~]# df -h
    Filesystem                                       Size  Used Avail Use% Mounted on
    /dev/vda1                                         40G  1.8G   36G   5% /
    devtmpfs                                         1.9G     0  1.9G   0% /dev
    tmpfs                                            1.9G     0  1.9G   0% /dev/shm
    tmpfs                                            1.9G  472K  1.9G   1% /run
    tmpfs                                            1.9G     0  1.9G   0% /sys/fs/cgroup
    tmpfs                                            379M     0  379M   0% /run/user/0
    082e54b989-ciq13.cn-hangzhou.nas.aliyuncs.com:/  1.0P     0  1.0P   0% /mnt
    ```


