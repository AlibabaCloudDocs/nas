# Troubleshoot mount issues {#concept_1614284 .concept}

This topic describes how to troubleshoot and fix mount issues.

## Mount an NFS file system on an ECS instance running Linux {#section_b4i_yf0_l1x .section}

-   Enable automatic troubleshooting by using a script

    You may fail to mount an NFS file system on an ECS instance running Linux due to many issues. You can use the following script to troubleshoot a mount issue and find the root cause.

    1.  Log on to a Linux ECS instance on which you fail to mount a file system.
    2.  Use the following commands to download and run the check\_alinas\_nfs\_mount.py script. Then, you can follow instructions provided by the script to resolve mount issues.

        ``` {#codeblock_dpn_el7_rzo}
        wget -N https://code.aliyun.com/nas_team/nas-client-tools/raw/master/linux_client/check_alinas_nfs_mount.py -P /tmp/
        ```

        ``` {#codeblock_wrr_uso_469}
        python2.7 /tmp/check_alinas_nfs_mount.py file-system-id.region.nas.aliyuncs.com:/ /mnt
        ```

        In the preceding command, file-system-id.region.nas.aliyuncs.com:/ indicates the domain name of the mount point, and /mnt indicates the target mount directory. You need to replace the domain name and the target mount directory based on your business requirements.

        After all issues are resolved, a specific mount command is displayed and a prompt appears indicating that troubleshooting is complete.

        **Note:** During the running of a script, you need to respond to questions prompted by the script. We recommend that you log on to the Alibaba Cloud console and confirm the related information about each answer. Then, enter **Yes** or **No** as the answer to the question to continue the script until the root cause is found.

    3.  Copy and run the mount command to enable the mount of a file system.
-   More known issues

    Several errors prompted by the mount command cannot be fixed by using the script. You can use the following methods to fix these errors.

    -   An error occurred while mounting the subdirectory of a file system

        Error message: mount.nfs: access denied by server while mounting xxxx.nas.aliyuncs.com:/<dir\>

        **Note:** If an error message indicating "Permission denied" occurs, you can use the script to troubleshoot the issue.

        An error occurs when you attempt to mount a subdirectory of a NAS file system on an ECS instance but the subdirectory does not exist. You can first mount the root directory of the NAS file system. After the root directory is mounted, you can create a subdirectory on the NAS file system and mount the subdirectory again.

    -   An error occurred while mounting a file system on two instances with duplicate names

        Error message: mount.nfs: Operation not permitted. This error occurs when you mount an NFSv4-compliant file system. However, you need to mount an NFSv3-compliant file system.

        For several kernel versions of Linux, an error may occur in the following scenario: You attempt to mount a file system on an ECS instance with the same name as that of another ECS instance on which the file system is already mounted. You can perform the following steps to fix the issue:

        1.  Run the following command on the ECS instance on which you fail to mount a file system.

            ``` {#codeblock_ee0_vtw_gaz}
            echo "install nfs /sbin/modprobe --ignore-install nfs nfs4_unique_id=`cat /sys/class/dmi/id/product_uuid`" >> /etc/modprobe.d/nfs.conf
            ```

        2.  Restart the ECS instance during off-peak hours.

            You can also unmount all available NFS file systems and use the `rmmod` command to uninstall the nfsv4 and nfs kernel modules.

        3.  Re-mount the NFS file system.

## Mount an SMB file system on an ECS instance running Windows {#section_txh_rdh_dfn .section}

-   Enable automatic troubleshooting by using a script

    You may fail to mount an SMB file system on an ECS instance running Windows due to many issues. You can use the following script to troubleshoot a mount issue and find the root cause.

    1.  Log on to a Windows ECS instance on which you fail to mount a file system.
    2.  Use the following commands to download and run the check\_alinas\_nfs\_mount.py script. Then, you can follow instructions provided by the script to resolve mount issues.

        ``` {#codeblock_gl1_0b3_sbw}
        wget https://code.aliyun.com/nas_team/nas-client-tools/blob/master/windows_client/alinas_smb_windows_inspection.ps1 -OutFile alinas_smb_windows_inspection.ps1
        ```

        ``` {#codeblock_t0v_vp6_dvm}
        .\alinas_smb_windows_inspection.ps1 -MountAddress abcde-123.region-id.nas.aliyuncs.com -Locale zh-CN
        ```

        In the preceding command, abcde-123.region-id.nas.aliyuncs.com indicates the domain name of the mount point. You need to replace the domain name based on your business requirements.

-   More known issues

    For more information, see [Causes and solutions of SMB mount failures](reseller.en-US/FAQ/SMB FAQ/Causes and solutions of SMB mount failures.md#). You can find the corresponding solution to any possible error code.


