# Can I switch the type of Apsara File Storage NAS file systems? {#concept_1545972 .concept}

This topic describes how to switch the type of an Apsara File Storage NAS file system.

You cannot switch the type of the file system after it is created.

You can create a new file system if you no longer want to use the original file system.

-   If the file system does not store any data
    1.  Create a new file system and mount it on an ECS instance. For more information, see [Quick start](../../../../reseller.en-US/Quick Start/NAS Capacity and NAS Performance/Mount a file system on an ECS instance running Linux.md#).
    2.  Delete the original file system.
-   If the file system stores data
    1.  Create a new file system and mount it on an ECS instance. For more information, see [Quick start](../../../../reseller.en-US/Quick Start/NAS Capacity and NAS Performance/Mount a file system on an ECS instance running Linux.md#).
    2.  Migrate the data in the original file system to the new system. For more information, see [Migrate data between Apsara File Storage NAS file systems](../../../../reseller.en-US/Migrate data between NAS file systems/Background information.md#).
    3.  Delete the original file system.

