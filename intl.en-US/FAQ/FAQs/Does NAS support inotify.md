# Does NAS support inotify {#concept_48118_zh .concept}

While inotifywait is commonly used in combination with rsync to backup/synchronize data on a quasi-real-time basis, it may not work properly on NAS file systems due to the implementation of inotify.

## How inotify works {#section_rhv_ngh_hfb .section}

inotify is a sub-module of the Linux kernel, and inotifywait is the user-mode interface of inotify. inotify is realized at the VFS layer. When file operations reach the VFS layer, the inotify module sends the operation type \(creation/deletion/attribute change, and so on\) and operation object \(file name\) to the user-mode, and the user-mode inotifywait then outputs the operation information to the user.

## Problem {#section_q5f_qgh_hfb .section}

Because inotify is implemented at the VFS layer of the kernel, the local kernel cannot recognize operations made by a remote client on the NFS file system. Therefore, inotify cannot recognize modifications on files made by the remote client.

If you Mount the same NAS file system simultaneously on Client A and Client B, and enable inotifywait at Client A to monitor the mounted directory, the following occurs:

-   inotifywait recognizes operations on files in the mounted directory on Client A.
-   inotify cannot recognize any operation on files in the mounted directory on Client B.

## Solution {#section_mgy_dhh_hfb .section}

An alternative solution is to use [FAM](http://oss.sgi.com/projects/fam/doc.html).

FAM is a library used for monitoring files or directories, and it is fully implemented in user-mode. You then only need to run a daemon in the background to regularly scan the directory and check for file changes.

However, using FAM has the following issues:

-   You must write a program to call the FAM interface implementation function.
-   In scenarios with a large number of files, using FAM may have poor performance and consume a lot of resources. Furthermore, it cannot ensure real-time monitoring.

