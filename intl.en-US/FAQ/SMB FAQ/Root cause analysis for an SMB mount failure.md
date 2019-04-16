# Root cause analysis for an SMB mount failure {#concept_fpq_xwf_2hb .concept}

You can use the following steps to troubleshoot the issue when you fail to mount an SMB file system on a Windows-based instance.

1.  Check whether the mount command is correct. For example, a redundant forward slash \(`/`\) exists, you are missing a backslash \(`\`\), or space is missing. Additionally, you must keep myshare in the mount command. The sample format of a command that you can use to mount an SMB file system is illustrated as follows:

    ```
    net use  <the target drive>  \\<the domain name of a mount point>\myshare
    ```

2.  Check your current version of Windows. Currently, you can only mount an SMB file system on an ECS instance that runs Windows 2008 R2 and later, excluding Windows 2008.
3.  Check that the protocol type is SMB. You cannot mount an NFS file system using the SMB protocol as shown in the following figure. \[DO NOT TRANSLATE\]

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/149028/155538220241401_en-US.png)

4.  Ensure that the permission group of the SMB file system includes the internal IP address or the VPC IP address of the ECS instance on which the SMB file system is mounted.
5.  When you add a mount point in a classic network, ensure that both the ECS instance where the mount point is located and the NAS file system that you mounted are owned by the same Alibaba UID.
6.  Check whether the Alibaba UID is in the overdue state.
7.  Check whether you can ping the mount address of the mount point and latency is as expected.
8.  If you ping the mount address, check whether you can connect to the mount point using the `telnet <the domain name of the mount point> 445` command.
9.  Ensure that the NetBIOS over TCP/IP and workstation services are enabled on the ECS instance where the mount point is located.

