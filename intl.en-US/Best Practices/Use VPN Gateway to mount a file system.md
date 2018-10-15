# Use VPN Gateway to mount a file system {#concept_54998_zh .concept}

## Limits {#section_z3q_4ph_hfb .section}

You can use Alibaba Cloud Network Attached Storage \(NAS\) to mount a file system created within a region on ECS instances only within that same region.

You cannot directly mount a file system on ECS instances in other regions. You also cannot directly mount a file system on the servers in your own data center.

For example, a file system \(NFS or SMB\) created in the East China 1 region cannot be directly mounted to an ECS instance in the North China 1 region.

To mount a file system on ECS instances in different regions, or on your IDC servers, you can use Express Connect. Using Express Connect, you can connect different VPCs or connect the data center and the VPC. However, deploying Express Connect will incur additional costs.

## Solutions { .section}

Using the VPN Gateway service of Alibaba Cloud, you can access Alibaba Cloud VPC from your data centers and connect to VPCs in different regions. The VPN Gateway service allows NAS users to deploy the following network topology and mount the file system using two methods:

-   Mount the file system on the servers in your IDC

-   Mount the file system on ECS instances in different regions


![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18705/153960883613109_en-US.png)

## Mount the file system on the servers in your IDC { .section}

1.  Log on to the NAS console, create a file system, and add VPC mount points to the file system.
2.  Log on to the VPC console, create a VPN connection to connect the VPN Gateway within the VPC and the VPN Gateway within your IDC. For more information, see [Configure a site-to-site connection](../../../../reseller.en-US/IPsec-VPN Quick Start/Configure a site-to-site connection.md#).

After completing these configurations, you can verify the connectivity between the IDC server and the ECS instance or the mount point of the file system in VPC by using the `ping` command. After confirming IP addresses at both ends can be pinged, you can mount the file system within the VPC onto the server at the side of VPN Gateway within your IDC..

## Mount the file system on ECS instances in different regions { .section}

Two methods are available for mounting the file system on ECS instances in different regions.

For method 1, you must build a VPN Gateway by using an ECS server within VPC2. This method is suitable if you have already deployed similar gateway services. If you do not have such an environment, you may use method 2.

-   Method 1

    1.  Log on to the NAS console, create a file system, and add VPC mount points to the file system within VPC1.
    2.  Build a user VPN Gateway as a User Gateway by using an ECS server within VPC2 in another region. This ECS must have an Internet IP address to connect with the VPN Gateway within VPC1.

        **Note:** If you want to know how to build a VPN Gateway by using an ECS server, you can see tutorials on the Internet, for example, [Using StrongSwan for IPSec VPN on CentOS 7](https://www.vultr.com/docs/using-strongswan-for-ipsec-vpn-on-centos-7).

    3.  Log on to the VPC console, create a VPN connection, and connect VPN Gateways within VPC1 and VPC2 \(the one created in Step 2\). For more information, see [Configure a site-to-site connection](../../../../reseller.en-US/IPsec-VPN Quick Start/Configure a site-to-site connection.md#).
    4.  Add a static route for other ECS instances within VPC2, and set the target CDIR block to the same as that of VPC1. Set the net-hop node as the gateway \(the one created in Step 2\) within VPC2.
    After completing these configurations, you can verify the connectivity between VPC1 and the ECS instance or the mount point of the file system in VPC2 by using the `ping` command. After confirming IP addresses at both ends can be pinged, you can mount the file system within VPC1 onto other ECS instances within VPC2.

-   Method 2

    1.  Log on to the NAS console, create a file system, and add VPC mount points to the file system within VPC1.
    2.  Log on to the VPC console, and create a VPN Gateway. For more information, see [Configure a site-to-site connection](../../../../reseller.en-US/IPsec-VPN Quick Start/Configure a site-to-site connection.md#).
    3.  Log on to the VPC console, and create a VPN Gateway within VPC2 in another region.
    4.  Create user gateways respectively with IP addresses of VPN Gateways created in Step 2 and Step 3. For more information, see [Configure a site-to-site connection](../../../../reseller.en-US/IPsec-VPN Quick Start/Configure a site-to-site connection.md#).
    5.  Create a VPN connection to connect VPN Gateways which were created in Steps 2 and 3. For more information, see [Configure a site-to-site connection](../../../../reseller.en-US/IPsec-VPN Quick Start/Configure a site-to-site connection.md#).
    6.  Add routes for the two VPCs. For VPC1, set the target CIDR block as the intranet IP address of VPC2, and the next-hop node as the gateway within VPC1. For VPC2, set the target CIDR block as the intranet IP address of VPC1, and the next-hop node as the gateway within VPC2. For more information, see [Configure a site-to-site connection](../../../../reseller.en-US/IPsec-VPN Quick Start/Configure a site-to-site connection.md#).
    After completing these configurations, you can verify the connectivity between VPC1 and the ECS instance or the mount point of the file system in VPC2 by using the `ping` command. After confirming IP addresses at both ends can be pinged, you can mount the file system within VPC1 onto other ECS instances within VPC2.


## Benefits { .section}

-   VPN Gateway service:

    -   Solves connectivity issues.
    -   Provides secure access \(encrypted communication based on IPsec\).
    -   Greatly reduces user cost in comparison to Express Connect.
-   However, when you access the file system through a VPN, the I/O performance is limited. The limitations are based on the Internet bandwidth and latency between the IDC server and VPC or between the different VPCs.


