# Pricing {#concept_27523_zh .concept}

This topic describes billing items and billing methods for NAS. You can familiarize yourself with the pricing structure of NAS through this topic.

## Billing items {#section_twj_hkz_2fb .section}

NAS supports the subscription and pay-as-you-go billing methods. The two billing methods are both based on the used space of a file system.

|Billing item|Calculation|
|------------|-----------|
|Used space|Charges are incurred for the maximum used space of a file system within an hour. Used space indicates the total size of all files on a file system, excluding directories. The basic storage unit is 4 KB even if a file is less than 4 KB. For example, if the size of a file is 3 KB, the file will be stored in a storage unit of 4 KB. **Note:** NAS allocates extra space to a file system for backup. Therefore, charges for the extra space are added to the total cost of a file system.

 |

## Billing methods {#section_5k8_biq_lbe .section}

NAS supports the subscription and pay-as-you-go billing methods.

-   [Pay-as-you-go](reseller.en-US/Pricing/Pay-as-you-go.md#)Pay-as-you-go is a billing method that you can use to pay for a service after you use the service. Expenses incurred within an hour are deducted from the balance at the next hourly interval. For example, if you receive a bill at 9:30, the bill includes the expenses from 8:00 to 9:00. The basic billing unit is one hour. Each expense is paid by the hour even if the usage time of a file system is less than one hour.

    **Note:** Assume that you receive a bill at 9:30. However, the bill may only include the expenses from 7:00 to 8:00 due to a system delay.

-   [Subscription \(Storage Package\)](reseller.en-US/Pricing/Subscription/Purchase a storage package.md#): After you purchase a storage package, it covers a specified amount of consumed resources that you use. A storage package is more cost-effective.

    **Note:** 

    -   If the used space of a file system exceeds the maximum capacity of a storage package, charges incurred for the extra space is paid by using the pay-as-you-go billing method.
    -   You can attach only one storage package to each file system.
    -   During the validity period of a storage package, you cannot downgrade the storage package.
    For example, you purchase a storage package of 500 GB for File System A. During a period from 7:00 to 8:00, the maximum used space of File System A is 800 GB. Therefore, 500 GB of the total 800 GB is covered by the storage package. Charges incurred for the remaining 300 GB are paid by using the pay-as-you-go billing method.


For more information about the pricing structure of NAS, see Pricing.

## FAQ {#section_9wy_f82_17v .section}

-   Are charges incurred after I activate NAS？

    No, no charge is incurred if you only activate NAS.

-   After you delete all data on a file system, the storage capacity of the file system is unchanged. However, you are still being charged for use of the storage capacity.

    The used space of a file system is displayed on a bill and in the NAS console. The value of the used space only indicates the maximum storage capacity for the file system over the last hour. You need to wait a few minutes until the value changes.


