# Mount NAS file systems on ECS instances that are located in multiple VPCs {#concept_bnk_22m_xgb .concept}

This section describes how to mount NAS file systems on ECS instances that are located in multiple VPCs.

By default, when you mount a NAS file system on an ECS instance, ensure that the ECS instance and the NAS file system are located in the same VPC network. However, in most deployments, the VPC of an ECS instance is different from the VPC of a NAS mount point. You can connect VPCs by using Cloud Enterprise Network \(CEN\).

## Configure a connection between VPCs {#section_kmv_trm_xgb .section}

CEN enables connections between instances that are located in multiple VPCs but in the same region. After the connection is established, the ECS instance in VPC1 can directly communicate with the ECS instance and the NAS mount point in VPC2 by using the ping command.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/155375161339613_en-US.png)

1.  Create a CEN instance
    1.  Log on to the [CEN console](https://cen.console.aliyun.com/).
    2.  On the CEN page, click **Create CEN Instance**.
    3.  Configure the CEN instance as shown in the following figure.

        \[DO NOT TRANSLATE\]

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/155375161339616_en-US.png)

        The options are described as follows:

        |Option|Description|
        |------|-----------|
        |Name| Enter the name of the CEN instance.

 The name can be 2 to 128 characters in length and can contain numbers, letters, Chinese characters, hyphens \(-\), and underscores \(\_\). It must start with a letter or a Chinese character.

 |
        |Description| Enter the description of the CEN instance.

 The description can be 2 to 256 characters in length. It cannot start with `http://` or `https://`.

 |
        |Attach a network|You can attach networks in your account or another account to a CEN instance. For more information, see [Networks](https://help.aliyun.com/document_detail/66001.html#concept-gbk-1mh-tdb).|

2.  Examples
    1.  On the Instances page, locate the newly created instance and click **Manage** in the Actions column.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/155375161339619_en-US.png)

    2.  On the CEN page, click **Attach Network** to configure the network as shown in the following figure.

        \[DO NOT TRANSLATE\]

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/155375161339622_en-US.png)

        The options are described as follows:

        |Option|Description|
        |------|-----------|
        |Account|Select **Your Account**.|
        |Network Type|Select the type of network to attach to the instance. You can select one of the following values: VPC, Virtual Border Router \(VBR\), and CloudConnectNetwork \(CCN\). Select VPC.|
        |Region|The region where the network is located. Select China \(Qingdao\).|
        |Networks|Select a network to attach. Select a VPC network.|

        Repeat the preceding procedure to attach two VPC networks to the same CEN instance. At this point, the connection between two VPCs is established.

3.  Verify the mounting result

    Log on to the ECS instance to verify the mounting result.

    ```
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


