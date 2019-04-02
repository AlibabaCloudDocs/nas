# How do I avoid exceptions when multiple processes and multiple clients write the same log file at the same time {#concept_45213_zh .concept}

NAS enables multiple clients to share and write files in the same namespace using the NFS protocol. However, the NFS protocol does not support Atomic Append semantics.

## Problem {#section_dqt_xch_hfb .section}

When multiple processes/clients write the same file \(for example, the same log\) at the same time, and each process independently maintains context information \(such as file descriptor or write location\), there may be coverage, crossover, and disordered content.

## Solution {#section_rm5_zh1_mfb .section}

Two solutions are provided:

-   \(Recommended\) Allow different processes/clients to write to different files in the same file system, and then consolidate these files during your analysis. This solution is preferable as it can mitigate problems caused by concurrent writing without the need for any filelock or alterations to performance.
-   Use the flock with seek method to ensure the atomicity and consistency of writing. The flock with seek method is a relatively time-consuming operation, that may significantly affect performance. The following steps detail how to implement the flock with seek method in Linux.

## Flock with seek method { .section}

As the NFS protocol does not support Atomic Append semantics, when multiple processes/clients write the same file \(for example, the same log\) at the same time, there may be coverage content. In Linux, you can simulate Atomic Append on the NFS file system by using flock + seek to protect and support concurrent append writing to the same file.

You can use flock + seek as follows:

1.  Call `fd = open(filename, O_WRONLY | O_APPEND | O_DIRECT)` to open the file by means of append writing, and specify O\_DIRECT \(bypass Page Cache to write directly\) to acquire file descriptor `fd`.
2.  Call `flock(fd, LOCK_EX|LOCK_NB) to get the filelock`. In case of failure \(for example, the filelock is already in use\), the system returns an error. Retry or perform error handling.
3.  Call `lseek(fd, 0, SEEK_END)` to point the current file offset \(cfo\) of the `fd` to the end of the file.
4.  Perform normal write operations. The insert location is the end of the file. The filelock can prevent overwriting.
5.  Call `flock(fd, LOCK_UN)` to release the filelock after the write operation.

The following is a simple C language sample program.

```language-c
#define _GNU_SOURCE
#include<stdlib.h>
#include<stdio.h>
#include<fcntl.h>
#include<string.h>
#include<unistd.h>
#include<sys/file.h>
#include<time.h>

const char *OUTPUT_FILE = "/mnt/blog";
int WRITE_COUNT = 50000;

int do_lock(int fd)
{
    int ret = -1;
    while (1)
    {
        ret = flock(fd, LOCK_EX | LOCK_NB);
        if (ret == 0)
        {
            break;
        }
        usleep((rand() % 10) * 1000);
    }
    return ret;
}

int do_unlock(int fd)
{
    return flock(fd, LOCK_UN);
}

int main()
{
        int fd = open(OUTPUT_FILE, O_WRONLY | O_APPEND | O_DIRECT);
        if (fd < 0)
        {
                printf("Error Open\n");
                exit(-1);
        }
        for (int i = 0; i < WRITE_COUNT; ++i)
        {
                char *buf = "one line\n";

                /* Lock file */
                int ret = do_lock(fd);
                if (ret ! = 0)
                {
                        Printf ("lock error \ n ");
                        exit(-1);
                }

                /* Seek to the end */
                ret = lseek(fd, 0, SEEK_END);
                if (ret < 0)
                {
                        printf("Seek Error\n");
                        exit(-1);
                }

                /* Write to file */
                int n = write(fd, buf, strlen(buf));
                if (n <= 0)
                {
                        printf("Write Error\n");
                        exit(-1);
                }

                /* Unlock file */
                ret = do_unlock(fd);
                if (ret ! = 0)
                {
                        printf("UnLock Error\n");
                        exit(-1);
                }
        }
        return 0;
}

```

For more information, see [Linux file locking mechanisms - Flock, Lockf, and Fcntl](http://www.hackinglinuxexposed.com/articles/20030616.html?spm=a2c63.o282931.a3.1.74705713AcQIeG).

**Note:** To use`flock()` on the NAS file system, your Linux kernel version must be 2.6.12 or later. If your Linux kernel uses an earlier version, use `fcntl()`.

