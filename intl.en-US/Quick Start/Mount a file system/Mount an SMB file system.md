# Mount an SMB file system {#concept_zb5_1rh_cfb .concept}

You can mount a NAS SMB file system to an ECS instance in Windows.

## Prerequisites {#section_zlq_3j1_dfb .section}

Before mounting an SMB file system to an ECS instance, ensure that the following two Windows system services are enabled:

-   Workstation
-   TCP/IP NetBIOS Helper

## Mounting command {#section_pgk_srh_cfb .section}

You can run a command in the following format to mount an SMB file system:

```
net use <target mounting drive> \\<domain name of the mount point>\myshare
```

## Parameter description {#section_skz_dsh_cfb .section}

-   Target mounting drive: Indicates the target drive to which you want to mount the SMB file system in the current Windows system. A space must be added between "use" and "\\\\".
-   Domain name of the mount point: Indicates the domain name of the mount point, which is automatically generated when you create the mount point of the file system.
-   myshare: Indicates the fixed SMB share name, which cannot be changed.

## Example {#section_dyj_bsh_cfb .section}

If you want to mount an SMB file system to drive Z, run the following command:

```
C:\> net use z: \\file-system-id-xxxx.region.nas.aliyuncs.com\myshare

```

## View mounting information {#section_ypf_4sh_cfb .section}

After mounting the SMB file system, you can run the following command in the Windows command-line tools to view the mounted file system.

```
net use
```

