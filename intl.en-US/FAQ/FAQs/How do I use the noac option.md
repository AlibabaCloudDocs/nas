# How do I use the noac option {#concept_hy2_hg3_ffb .concept}

## Problem {#section_h4v_53h_hfb .section}

A user mounts the same network file system on two ECS servers \(ESC-A and ESC-B\). The user writes data in append mode on ECS-A, and monitors file content changes with the `tail -f` command on ECS-B.

After data is written on ECS-A, the file content changes on ECS-B may experience latency of up to 30 seconds.

However, if a file is directly opened \(such as using `vi`\) on ECS-B under the same conditions, the updated content is visible immediately.

## Analysis {#section_rcj_w3h_hfb .section}

This is related to the `mount` option and the `tail -f` implementation.

The user uses the following mount command: `mount -t nfs4 /mnt/`

For file systems mounted on ECS-B using the NFS protocol, the kernel maintains a copy of metadata cache for the file and directory attributes. The cached file and directory attributes \(including permission, size, and time stamp\) are used to reduce the `NFSPROC_GETATTR RPC` requests.

The `tail -f` command uses `sleep+fstat` to monitor changes to the file attributes \(primarily the file size\), read files, and then output the results. However, file content output by using the `tail -f` command is dependent on the `fstat` result. Due to the metadata cache, the `fstat` command may not be monitoring real-time file attributes. Therefore, even if the file has been updated on the NFS server, the `tail -f` command cannot detect in real time whether the file has been changed or not, resulting in the latency.

## Solution {#section_mld_3jh_hfb .section}

Use the `noac` option of the `mount` command to disable the caching of file and directory attributes. The command is as follows:

`mount -t nfs4 -o noac /mnt/`

