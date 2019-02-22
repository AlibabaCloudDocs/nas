# Access NAS from the local IDC through NAT Gateway {#concept_57628_zh .concept}

This document introduces how to access NAS using the NAT Gateway for scenarios involving mounting a file system in NAS from your local IDC or VPCs if they are located in different regions.

## Background {#section_wcw_t2b_mfb .section}

When using NAS, a file system \(NFS\) created within a region can only be mounted on ECS instances within the same region. ECS instances in different regions, and servers in your own IDC, are not allowed to mount the file system directly.

To mount a file system on ECS instances in different regions, or on your IDC servers, you can use Express Connect between different VPCs or between the IDC and the VPC. While Express Connect is suitable for long-term connection, deploying Express Connect may be costly for some users.

A more cost-effective solution for uploading small amounts of offline data to NAS is to use the NAT Gateway to access Alibaba Cloud NAS from the Internet.

## Limits {#section_gd2_w2b_mfb .section}

-   If the EIP and VPC are connected, any user who obtains the EIP can use the mount point corresponding to the EIP without any additional permissions required.

-   Each EIP and port can only be mapped to one mount point. Therefore, multiple EIP addresses are required to visit multiple mount points at the same time.


## Network architecture {#section_tfw_x2b_mfb .section}

The following figure shows the network architecture of using a NAT Gateway to access Alibaba Cloud NAS from the Internet.

The architecture is implemented as follows:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155080448113110_en-US.png)

1.  Create a NAS file system, and add a mount point for the file system.
2.  Create a NAT gateway, and add a bandwidth package for the NAT gateway to get an EIP address.
3.  Add DNAT forwarding entries for the NAT gateway.

## Procedure {#section_zb4_bfb_mfb .section}

1.  Create a file system in the NAS console.
2.  Add a mount point for the file system. Note that you must create a VPC mount point to support the use of NAT.
3.  Connect to your ECS instance, and ping the mount point address to get the mount point IP address. An example output is as follows:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155080448113114_en-US.png)

4.  [Create a NAT gateway](../../../../../reseller.en-US/Quick Start/Create a NAT gateway.md#).
5.  [Bind an EIP](../../../../../reseller.en-US/Quick Start/Bind an EIP.md#) then add the bandwidth package to the NAT gateway.
6.  [Add a DNAT entry](../../../../../reseller.en-US/Quick Start/Add a DNAT entry.md#) to create a DNAT entry.
    -   For **Public IP**, select the EIP created in Step 5.
    -   For **Private IP**, enter the mount point IP address you want to access.
    -   For **Port Settings**, select **All ports**. You can also select the ports needed by the NFS or SMB protocols.
7.  Verify the NFS mounting. Configure the DNAT to an NFS mount point. Example outputs are as follows:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155080448113121_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155080448113119_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155080448113120_en-US.png)


