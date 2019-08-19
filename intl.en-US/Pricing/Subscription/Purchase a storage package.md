# Purchase a storage package {#concept_27524_zh .task}

Network Attached Storage \(NAS\) supports the subscription billing method. You can create a file system before attaching a storage package. You can also create a file system when you purchase a storage package.

## Purchase a storage package {#section_5al_h93_03c .section}

1.  Log on to the [NAS console](https://partners-intl.console.aliyun.com/#/nas).
2.  Choose **NAS** \> **File System List** and click **Buy Package**.
3.  Select the required configurations and click **Buy Now**.

    **Note:** You must attach a storage package to a file system. A file system can have only one storage package attached. You can select the ID of an existing file system or click **Create File System and Bind Package** to create a new file system.

4.  After the payment is complete, find the target file system, click Details next to the file system to open the **File System Details** page. You can view the information of the attached storage package.

## FAQ {#section_5xx_fqq_u9o .section}

-   When will a storage package take effect?

    A storage package takes immediate effect after the payment for the storage package is complete.

-   Can I refund a storage package?

    You can only refund an intact storage package. For more information about refunds, submit a ticket to Alibaba Cloud Customer Service.

-   What will happen after a storage package expires?

    If you fail to renew a storage package after the storage package expires, you are charged for the used space by using the pay-as-you-go billing method.

-   What will happen if the used space of a file system exceeds the maximum capacity of a storage package?

    You are only charged by using the pay-as-you-go billing method for the extra space that is not included in your storage package.

    For example, you purchase a storage package of 100 GB. However, the actual used space exceeds 100 GB. You will be charged by using the pay-as-you-go billing method for the extra space that exceeds 100 GB.

-   Can I purchase multiple storage packages for a file system?

    No, you can only attach a maximum of one storage package to a file system. If you require a storage package with a higher specification or longer duration, you can perform the [EN-US\_TP\_18688.dita\#concept\_53974\_zh](EN-US_TP_18688.dita#concept_53974_zh) action on the existing storage package.

-   Is the storage capacity of a file system limited by the capacity of a storage package?

    No, the storage capacity of a file system bears no relation to the capacity of a storage package. You are charged by using the pay-as-you-go billing method for the extra space that exceeds the maximum capacity of a storage package.

    For example, you create a NAS Performance file system and attach a storage package of 5 GB because the maximum capacity of the file system can reach 10 PB.


