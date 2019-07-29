# Enable an automatic mount at startup for an SMB file system {#task_bmh_dkk_2fb .task}

This topic describes how to create a mount script and a scheduled task to enable an automatic mount at startup for an SMB file system.

## Prerequisites {#section_qxx_g4r_16u .section}

1.  You have created a file system. For more information, see [Create file systems](intl.en-US/Console User Guide/Manage file systems.md#section_5jo_0kj_jn5).
2.  You have created a mount point. For more information, see [Create a mount point](intl.en-US/Console User Guide/Manage mount points.md#section_6xi_a3u_zkq).
3.  Ensure that the following Windows services are started:
    -   Workstation

        1.  Choose **All Programs** \> **Accessories** \> **Run**, or press `Win+R` and enter `services.msc` to open the Services console.
        2.  Locate the Workstation service and ensure that the status of the service is **Started**.

            The Workstation service is started by default.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156438409042055_en-US.png)

    -   TCP/IP NetBIOS Helper

        Perform the following steps to start the TCP/IP NetBIOS Helper service:

        1.  Open **Network and Sharing Center** and click the active network connection.
        2.  Click **Properties** to open the Local Area Network Properties dialog box. Double-click **Internet Protocol Version 4 \(TCP/IPv4\)** to open the Internet Protocol Version 4 \(TCP/IPv4\) Properties dialog box, and then click **Advanced**.
        3.  In the Advanced TCP/IP Settings dialog box, choose **WINS** \> **Enable NetBIOS over TCP/IP**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156438409042056_en-US.png)


## Procedure {#section_asn_ci4_x0r .section}

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
2.  Create a script file named nas\_auto.bat and add the following command to the file.

    ``` {#codeblock_ad0_f5r_ff5}
    net use D: \\file-system-id.region.nas.aliyuncs.com\myshare 
    ```

    The format of the command used to mount the file system is `net use <the drive of the mount target> \\<the domain name of a mount point>\myshare`.

    -   The drive of the mount target: the target drive on which you need to mount a file system.
    -   The domain name of a mount point: the domain name generated when you create the mount point for a file system. For more information, see [Create a mount point](intl.en-US/Quick Start/NAS Capacity and NAS Performance/Mount a file system on an ECS instance running Windows.md#).
    -   myshare: indicates the name of an SMB share. You cannot change the name.
    **Note:** 

    Ensure that the name of the target mount drive is unique on the target ECS instance.

3.  Create a scheduled task.
    1.  Open the Control Panel and choose **Administrative Tools** \> **Task Scheduler**.
    2.  In the Task Scheduler window, choose **Actions** \> **Create Task**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156438409012128_en-US.png)

    3.  Select the **General** tab, enter the **Name** of the task, and select **Run whether user is logged on or not** and **Run with highest privileges**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156438409112129_en-US.png)

    4.  Select the **Triggers** tab, click **New**, select **Logon** in the **Begin the task** field, select **Enabled** in the **Advanced Settings** section, and click **OK**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156438409112130_en-US.png)

    5.  Select the **Actions** tab, click **New**, select **Start a program** in the **Action** field, select the nas\_auto.bat file in the **Program/script** field, and click **OK**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156438409112131_en-US.png)

    6.  Select the **Conditions** tab, and select **Start only if the following network connection is available**. Select **Any connection** in the **Network** section.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156438409112132_en-US.png)

    7.  Select the **Settings** tab, select **If the running task does not end when requested, force it to stop**, and select **Do not start a new instance** in the **If the task is already running, then the following rule applies** field.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156438409112133_en-US.png)

    8.  Click **OK**.
    9.  Restart the ECS instance to verify if the scheduled task is created.

        An example of a successfully created task is shown in the following figure.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156438409212134_en-US.png)

4.  Open the command prompt and run the `net use` command to verify the mount results.

    An example of a successful mount is shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156438409249545_en-US.png)


