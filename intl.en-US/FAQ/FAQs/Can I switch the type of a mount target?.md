# Can I switch the type of a mount target? {#concept_1698383 .concept}

This topic describes how to switch the type of a mount target.

If you have added a mount target for a file system, you cannot switch the type of the mount target. You can create a new mount target and mount the file system on the instance again.

For example, you have created an Apsara File Storage NAS Capacity file system and have mounted the file system on an instance through a mount target in a classic network. If you want to switch the mount target in a virtual private cloud \(VPC\), perform the following steps:

**Note:** You can add two mount targets for an Apsara File Storage NAS Capacity file system or an Apsara File Storage NAS Performance file system. However, you can only add one mount target in a VPC for an Apsara File Storage NAS Extreme file system.

1.  Add a mount target in a VPC. For more information, see [Add a mount target](../../../../reseller.en-US/Console User Guide/Manage mount targets.md#section_6xi_a3u_zkq).
2.  Unmount the file system which is mounted on the instance through the mount target in a classic network. For more information, see [Unmount a file system](../../../../reseller.en-US/Console User Guide/Unmount a file system/Unmount a file system from an ECS instance running Linux.md#).
3.  Use the mount target in the VPC to mount the file system on the same target path of the instance. For more information, see [Mount a file system](../../../../reseller.en-US/Console User Guide/Mount a file system/Precautions.md#).
4.  Make sure that no client is mounted on the instance in the [NAS console](partners-intl.console.aliyun.com/#/nas).

    You can click the **The client is mounted** button in the mount point section of the file system details page to view the mounted clients.

5.  Disable the mount target in the classic network.
6.  After you make sure that your business is not adversely affected, delete the mount target in the classic network.

