The address space is divided into different areas.
IO devices are directly mapped into the address space
![[Pasted image 20220727110104.png | 200 ]]

The [[Memory Protection Unit]] allows the permission setting of different memory regions within the address space 

There are privileged and unprivileged execution mode. Privileged mode can access the entire address space. Peripherals are only accessible in privileged.

Exception handler are executed in privileged mode. Code in unprivileged mode create software exception with SVC (supervisor call) instruction.

