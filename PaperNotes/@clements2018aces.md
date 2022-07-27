---
title: ACES: Automatic Compartments for Embedded Systems
authors: Abraham A. Clements, Naif Saleh Almakhdhub, Saurabh Bagchi, Mathias Payer
year: 2018
published: [[]]
conference: 
---

Designed an automatic compartment system for bare metal code on [[ARM Cortex-M]]. The paper uses static analysis with LLVM and the [[Program Dependence Graph]] to partition the bare metal code into several compartments.  The memory isolation between compartments is enforced with the [[Memory Protection Unit]].
