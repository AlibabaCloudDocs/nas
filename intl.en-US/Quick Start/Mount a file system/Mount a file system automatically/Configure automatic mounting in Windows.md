# Configure automatic mounting in Windows {#task_bmh_dkk_2fb .task}

You can create a mounting script in the Windows operating system and then create a scheduled task, so that a NAS file system can be automatically mounted.

1.  Create a script named nas\_auto.bat in Windows and add the following mounting command to it. Then, save the script to the disk where you want to mount the file system. 
    -   To mount an SMB file system, add the following command to the script:

        ```
        net use Z: \\fid-xxxx.cn-shanghai.nas.aliyuncs.com\myshare 
        ```

        **Note:** 

        Change the drive letter \(Z:\) and the domain name of the mount point \(fid-xxxx.cn-shanghai.nas.aliyuncs.com\) to actual values.

        For details about the mounting command, see [Mount an SMB file system](reseller.en-US/Quick Start/Mount a file system/Mount an SMB file system.md#) .

2.  In the Control Panel of Windows, select **Administrative Tools**, and then select **Schedule tasks**. 
3.  In Task Scheduler, select **Action** \> **Create Task**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154322585812128_en-US.png)

 
4.  On the **General** tab, enter the **Name** of the scheduled task, and then select **Run whether user is logged on or not** and **Run with the highest privileges**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154322585812129_en-US.png)

 
5.  On the **Triggers** tab, click **New**. Then, select **At log on** for **Begin the task**, and select **Enabled** in **Advanced settings**. After that, click **OK**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154322585812130_en-US.png)

 
6.  On the **Actions** tab, click **New**. Then, select**Start a program** for **Actions**, and then select the created nas\_auto.bat script in **Program/script**. After that, click **OK**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154322585812131_en-US.png)

 
7.  On the **Conditions** tab, select **Start only if the following network connection is available**, and then select **Any connection**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154322585812132_en-US.png)

 
8.  On the **Settings** tab, select **If the running task does not end when requested, force it to stop**, and then select **Do not start a new instance** for **If the task is already running, then the following rule applies**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154322585812133_en-US.png)

 
9.  Click **OK**. 
10. Restart the server to check whether the task is successfully created. If the system displays the following information, the scheduled task can be normally executed:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154322585812134_en-US.png)


