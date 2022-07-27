---
title: D-Box: DMA-enabled Compartmentalization for Embedded Applications
authors: Alejandro Mera, Yi Hui Chen, Ruimin Sun, Engin Kirda, Long Lu
year: 2022
published: [[]]
conference: 
---

The paper cover the protection of DMA in embedded device [[Compartmentalization]], which is missing in previous work. 

The compartments are clearly separated into *tasks* in the [[Real-time OS]]. Hence, there is no automatic compartmentalization used ([[@clements2018aces]]). The paper allows developer to pass policies in the form of *resource* and *capability* of each task. Resources are just the memory region used for the task stack. The  capabilities is the DMA capabilities to perform DMA.



Most of the design is based on FreeRTOS-MPU; the regions of [[Memory Protection Unit]]  is explicitly splitted into regions with specialized functionalities. For example, there are separated regions for
- kernel stack & heap
- Task stack
- Task code
- Syscall code
- kernel code, etc.



There are also use-defined regions. User-defined region is given smaller number than kernel regions so that it cannot overwrite kernel ([[Memory Protection Unit]]). The paper also modifies the kernel so make sure that user-defined regions of different users (the task stack) cannot overlap. 


Compared to static analysis to determine the regions, the authors claim that this method is precise.  However, this requires that the source code is clearly separated into tasks, so it is not a fair comparison.


A separated and trusted *DMA Task* is used to perform DMA request to the DMA controller.  For DMA access control, the paper introduce a "capability-based" model;  each requests' *source* and *destination* is used to authenticate the transfer. For write, *source* must be within the user's memory, and *destination* must have the capability (e.g., write).
