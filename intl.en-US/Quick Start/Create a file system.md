# Create a file system {#concept_27526_zh .concept}

To create a file system in NAS, follow these steps:

1.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).
2.  Click **Create File System** in the upper right corner.

    **Note:** 

    -   The maximum storage capacity of a file system is 1 PB for the SSD performance type and 10 PB for the capacity type. Fees are charged based on the actual usage.
    -   Each account can create up to 10 file systems.
3.  On the Create File System page, set the parameters.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18690/154417335421054_en-US.png)

    The parameters are described as follows:

    -   **Region**: Select the region where you want to create the file system.

        **Note:** A file system or computing node in a region cannot communicate with a file system or computing node in another region.

    -   **Storage Type**: You can select **SSD performance-type** or **Capacity-type**.
    -   **Protocol Type**: You can select **NFS \(including NFSv3 and NFSv4\)** or **SMB \(2.0 and later\)**.

        The NFS protocol and SMB protocol apply to ECS instances in Linux and Windows separately for file sharing.

    -   **Zone**: You can view all zones in the selected region in the drop-down list.

        **Note:** 

        -   A file system or computing node in a zone can communicate with a file system or computing node in a different zone but of the same region.
        -   To reduce cross-zone latency, we recommend that you select the zone of the ECS instance where you want to mount your file system.
4.  Click **OK**.

