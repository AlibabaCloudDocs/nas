# Terms {#concept_27519_zh .concept}

The following table lists some terms used in NAS.

|Term|Description|
|----|-----------|
|Mount point|A mount point is the access address of the file system in a VPC or classic network. Each mount point is mapped to a domain name. When using the `mount` command, you can specify the domain name of the mount point to mount the corresponding NAS file system to a local destination.|
|Permission group|A permission group acts as a whitelist in NAS. You can add rules to a permission group to specify access permissions for an IP address or an IP segment.**Note:** Each mount point must be assigned with a permission group.

|
|Authorized object|An authorized object is an attribute of a permission group rule. It represents the target to which a permission group rule is applied.In a VPC, an authorized object can be a single IP address or an IP segment.

In a classic network, an authorized object can only be a single IP address \(generally the intranet IP address of an ECS instance\).

|

