# Billing method {#concept_27523_zh .concept}

NAS is billed in two methods: Pay-As-You-Go and subscription

## Pay-As-You-Go {#section_nvd_mk1_hfb .section}

NAS Pay-As-You-Go storage is billed based on actual usage per hour. The charge is based on the maximum usage \(peak value\) of bucket occurring within the billed hour.

The bucket is defined as the total length of all objects in a NAS file system \(excluding directories\). Each object is 4 KB in length.

**Note:** A NAS file system pre-allocates space for sparse files. This space is included in buckets, and is therefore included in the billing amount.

## Subscription {#section_hgz_hl1_hfb .section}

NAS subscription storage packages can be more cost-effective than the Pay-As-You-Go billing method, depending on your business requirements. If your requirements exceed your defined subscription package, any excess resource usage is billed as Pay-As-You-Go. Subscription packages are available for the following regions:

-   China East 1 \(Hangzhou\)
-   China North 2 \(Beijing\)
-   China East 2 \(Shanghai\)
-   China South 1 \(Shenzhen\)
-   China North 1 \(Qingdao\)
-   Asia Pacific SE 1 \(Singapore\)

Storage capacity ranges from 500 GB up to 1 PB, and the duration of a storage package can be one month, six months, or one year.

**Note:** 

-   Each file system can only be assigned one storage package.
-   A storage package is only allowed to be upgraded within its validity period.
-   You cannot downgrade a storage package subscription.
-   Currently, only capacity type storage is available for subscription.

For more billing information, see NAS pricing page.

