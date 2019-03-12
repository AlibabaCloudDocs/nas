# CPFS user guide {#concept_cyg_wng_4gb .concept}

Cloud Paralleled File System \(CPFS\) is the paralleled file storage service provided by Alibaba Cloud. It focuses on providing high-performance file storage and access.

You can use CPFS as follows:

1.  Create a file system.
    1.  Log on to the [NAS console](https://nas.console.aliyun.com/) and select CPFS on the left-side navigation pane.
    2.  Click **Create File System**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/119749/155237308738079_en-US.png)

    3.  On the purchase page, make settings according to your requirements as follows:

        -   Specify the region and zone in which you want to create the CPFS file system and the capacity of the file system
        -   Specify the VPC and VSwitch for the CPFS file system that you want to create in the specified region. If you have not created a VPC, create one in the [VPC console](https://vpc.console.aliyun.com/).
        -   Select the number of CPFS file system instances that you want to create and the service duration of the instances.

        Currently, CPFS is billed in the subscription method. You can upgrade the storage capacity as needed during the service duration and renew the service after the service expires.

2.  Manage a file system.

    After purchasing a CPFS file system instance, return to the NAS console. The instance that your purchased will be created within a short period, as shown in the following figure.

    It takes about 10 minutes before a purchased CPFS instance is created. The following figure shows a created CPFS instance.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/119749/155237308738079_en-US.png)

    You can click **Manage** to view detailed information about the instance, click **Upgrade** to upgrade the instance, or click **Renew** to renew the service.

3.  Use a file system.

    You can use a created CPFS file system after mounting it to an ECS instance on the client.

    1.  Download and install the client.
    2.  Configure a mount point for the CPFS file system.

        Use the mount point shown in the console to make mount settings.

    3.  Mount the CPFS file system to an ECS instance.
    4.  Use the CPFS file system.

        CPFS supports POSIX semantics, allowing you to use common Linux commands \(such as `ls`\) to access and manipulate CPFS file systems.


