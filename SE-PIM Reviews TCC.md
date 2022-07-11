# Reviewer 1 
> - It is better for this paper to discuss the memory allocation and lockdown mechanism under a multi-tenant environment. In cloud computing, multiple host enclaves can share the same memory bank. SE-PIM uses a simple direct mapping for host logical memory space and device physical space, and according to 4.4.1 the lockdown mechanism is realized with “range registers”. Will these techniques still work when multiple enclaves are considered?  
> -  In section 7.2.2, the paper presents that “Despite having a lower throughput than direct memory access, the interface is faster than most ORAM implementations”. It is desirable to plot the relationship between throughput and block size of ORAM in Figure 10 for better illustration.  
> - How does SE-PIM handle large data sets and intensive computation? SE-PIM can handle maximum data set of 512 MB when 8 PIM cores are used. What if the data set is much larger? Another question is how many CPU cores are used in the “CPU-only” experiment in Figure 11. If only one CPU core is used, this means that two SE-PIM cores can achieve comparable computation with one CPU core. Considering that one machine can have tens of CPU cores, it concerns me how can SE-PIM handle tasks with intensive computation requirements.
- R1 say there should be comparison between SE-PIM data movement and ORAM
- We should explain that that sufficient CPU cores are used,  so the data movement is the bottleneck
- It should be exlained how SE-PIM work in multi-tentant / multi-enclave enviroment

# Reviewer 2
> 1) Will PIM overwhelm the usage of memory? How can you guarantee the cloud also can provide sufficient memory for such a design?  
> 2) For the threat model, can you provide some actual scenarios in real world which can help justify whether the attacks are doable in practice? For example, do you consider a piece of malware which can compromise the OS? Or a hacker which can physically approach the victim device?  
> 3) Can you discuss some preliminary mitigation strategies against the row hammer attack, the electromagnetic side-channel and power side-channel attack, etc, rather than simply consider them out-if-scope?  
> 4) Can you justify why your assumptions are reasonable? For example, why the tightly integrated PIM-enabled memory bank is secure from physical attacks?  
> 5) The design requires modifying the hardware, but the evaluation is based on some sort of simulation. Can you briefly discuss if there is any potential gap between the actual implementation and the simulation?  
> 6) Security analysis could be a bit more formal.

- 1) The use of SE-PIM will not overwhelm the usage of memory. This is because SE-PIM memory modules can operate as a traditional DRAM memory when not used for confidential computing.  Hence, the total amount of memory available to the cloud user remains the same. However, we assume that the cloud will provide SE-PIM module with confidential computing capabilities, on top of 
- To better demonstrate the actual attack scenario, we introduced an example of how . We also included demonstrate why probing 
- Should mention row-hammer mitigation methods 
- Discuss the potential gap between hardware and simulation