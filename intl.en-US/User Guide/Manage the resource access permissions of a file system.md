# Manage the resource access permissions of a file system {#concept_27533_zh .concept}

You can grant Resource Access Management \(RAM\) users the permissions to operate Network Attached Storage \(NAS\) file systems. We recommend that you log on and operate NAS file systems as a RAM user to follow best practices for security.

## NAS operations that you can authorize in RAM {#section_lzl_4pm_hfb .section}

You can authorize a RAM user one or more of the following permissions to operate NAS file systems.

|Action|Description|
|------|-----------|
|DescribeFileSystems|List all file systems.|
|DescribeMountTargets|List all mount points.|
|DescribeAccessGroup|List all permission groups.|
|DescribeAccessRule|List all permission group rules.|
|CreateMountTarget|Add a mount point for a file system.|
|CreateAccessGroup|Create permission groups.|
|CreateAccessRule|Create permission group rules.|
|DeleteFileSystem|Delete file systems.|
|DeleteMountTarget|Delete mount points.|
|DeleteAccessGroup|Delete permission groups.|
|DeleteAccessRule|Delete permission group rules.|
|ModifyMountTargetStatus|Enable or disable mount points.|
|ModifyMountTargetAccessGroup|Modify the permission group of a mount point.|
|ModifyAccessGroup|Modify permission groups.|
|ModifyAccessRule|Modify permission group rules.|

## NAS resources that you can authorize in RAM {#section_hwb_hqm_hfb .section}

You can only define RAM policies for the following resources:

|Resource|Description|
|--------|-----------|
|\*|Indicates all NAS resources.|

## Example {#section_jrm_kqm_hfb .section}

The following policy allows read-only access to all NAS resources.

```
{
  "Version": "1",
  "Statement": [
    {
      "Action": "nas:Describe*",
      "Resource": "*",
      "Effect": "Allow"
    }
  ]
}

```

