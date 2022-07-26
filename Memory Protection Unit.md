Is an *optional* component of [[ARM Cortex-M]] processors that allows simple memory permissions of memory regions. Compared to traditional [[Page-table Permissions]], it does not offer address translation.

The MPU can be  configured to have 8/16 memory regions. with different permisisons. A region must be minimum 32B, and, size power of 2, align to its size. Each region has a number, in case there are overlap between regions, the region with the higher number will be selected. There is a background region number -1 that is accessible by privileged software that provide access to primary partition.

