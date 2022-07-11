# Reviewer Comments
```
============================================================================ 
DAC 2022 Reviews for Submission #699
============================================================================ 

Title: CAPACETI: Cryptographically-authenticated Intra-Process Resource Access Control on ARM
Authors: Kyuwon Cho, Hajeong Lim and Hojoon Lee


============================================================================
                            REVIEWER #1
============================================================================

---------------------------------------------------------------------------
Reviewer's Scores
---------------------------------------------------------------------------
           Clarity / Writing Style (1-5): 4
      Originality / Innovativeness (1-5): 3
    Impact of Ideas and/or Results (1-5): 4
            OVERALL RECOMMENDATION (1-5): 3

Summarize shortly the contributions of the paper in your own words.
---------------------------------------------------------------------------
In this paper, the authors have proposed a novel design called CAPACETI that enables intra-process access control of process resources through cryptographically-authenticated capability tokens. Experimental results have been given to support the authors' claim, including file I/O performance, application benchmark, etc.
---------------------------------------------------------------------------


Strengths
---------------------------------------------------------------------------
+ A novel intra-process resource access control scheme is proposed
+ Experimental results are given along with discussions
---------------------------------------------------------------------------


Weaknesses
---------------------------------------------------------------------------
- Related works can be more introduced to emphasize the advantage of the proposed work
---------------------------------------------------------------------------


Main Discussion of Paper
---------------------------------------------------------------------------
This paper proposed a design, called CAPACETI, for fine-grained cryptographically-authorized resource access control. The proposed technique is implemented with different aspects of experimental results. The evaluation of the applicability and performance of the proposed design through real-world applications is also given.

Major advantages of this paper:
1. The authors have proposed CAPACETI for fine-grained cryptographically-authorized resource access control on ARM
2. Experimental results, as well as the evaluation based on real-world applications, are provided to support the authors' claim

Things can be improved
1. The major contribution and overall arrangement of the paper can be more detailed provided in the Introduction Section.
2. Some spaces in the manuscript can be squeezed to give room for the other necessary description.
---------------------------------------------------------------------------


Most prominent Strength or Weakness
---------------------------------------------------------------------------
Overall contribution
---------------------------------------------------------------------------



============================================================================
                            REVIEWER #2
============================================================================

---------------------------------------------------------------------------
Reviewer's Scores
---------------------------------------------------------------------------
           Clarity / Writing Style (1-5): 4
      Originality / Innovativeness (1-5): 2
    Impact of Ideas and/or Results (1-5): 3
            OVERALL RECOMMENDATION (1-5): 3

Summarize shortly the contributions of the paper in your own words.
---------------------------------------------------------------------------
This paper presents a capability-based system for intra-process privilege reduction. The paper argues that ambient authority contributes to many vulnerabilities these days. It then designs and implements a capability-based intra-process isolation mechanism called CAPACETI that uses ARM PA to retrofit Linux with cryptographic access control. CAPACETI is implemented on  QEMU for security evaluation and on Raspberry Pi for projected overhead evaluation.
---------------------------------------------------------------------------


Strengths
---------------------------------------------------------------------------
+ Builds a capability system on ARM PA and Linux
+ The performance evaluation is extensive
---------------------------------------------------------------------------


Weaknesses
---------------------------------------------------------------------------
- Novelty is incremental
- Not properly compared/contrasted with the related work
- Security evaluation needs improvement
---------------------------------------------------------------------------


Main Discussion of Paper
---------------------------------------------------------------------------
Intra-process isolation is a nice approach for reducing the ambient authority problem. Implementing the principle of least privileges in various layers of the software stack has received much attention in recent years and for good reason. The monolithic design of software is a major contributor to the insecurity modern systems as the paper correctly identifies.

A strength of the approach presented in the paper is its reliance on ARM PA, which is a commodity hardware (and thus more likely to be adopted than research processors). Also using Linux is a plus because of its widespread usage. I also appreciate the amount of engineering and implementation CAPACETI must have taken.

The performance of the technique is also evaluated both using micro- and macro-benchmarking, which is a strength here. Overall, given the unavailability of ARM PA on development boards, the paper seems to have done the best achievable evaluation, which is security evaluation on QEMU and performance evaluation on RPis.  

The paper, however, suffers from some major weaknesses. Perhaps the most important weakness of the paper is its incremental novelty. Capability systems such as Capsicum and CHERI have long been studied in the security community. The paper primarily focuses on motivating capabilities and describing what they are instead of distinguishing this work from the prior work in this area. The one-sentence comparison ('On the other hand, our work explores intra-process  resource access control through adopting capabilities.') does not properly differentiate this work from CHERI's capability-based BSD or Capsicum. As such, the work seems rather incremental and its novelty is unclear. Other than instantiating capabilities using ARM PA, it is unclear what is novel/insightful here. I don't mean to belittle the work; such implementations can have great practical uses. Linux and ARM is different from BSD and CHERI, so such an implementation can be quite useful. I am just not sure the paper !
 has sufficient novelty for a research conference like DAC.

The security evaluation also needs improvement. The brute forcing attack is just one possible attack, and not a very effective one either. Blind ROP attack does not work based on pure brute force; it is a more clever attack based on  incrementally guessing 64-bit values one byte at a time. The paper needs to present a more compelling argument for guessing/forging capabilities is hard to do. While the paper mentions that security is evaluated on QEMU, the security evaluation section does not contain sufficient arguments on the difficulty of forgery, other than the brute forcing back-of-an-envelop calculations. For example, ARM PAC is vulnerable to reuse attacks (see [15]). Are those considered/mitigated? How?
---------------------------------------------------------------------------


Most prominent Strength or Weakness
---------------------------------------------------------------------------
Not properly compared/contrasted with the related work
---------------------------------------------------------------------------



============================================================================
                            REVIEWER #3
============================================================================

---------------------------------------------------------------------------
Reviewer's Scores
---------------------------------------------------------------------------
           Clarity / Writing Style (1-5): 3
      Originality / Innovativeness (1-5): 3
    Impact of Ideas and/or Results (1-5): 2
            OVERALL RECOMMENDATION (1-5): 2

Summarize shortly the contributions of the paper in your own words.
---------------------------------------------------------------------------
This paper employs ARM v8.3 Pointer Authentication to enable intra-process isolation of process resources primarily targeting Linux ARM systems and address the problem of ambient authority. It proposes a fine-grained cryptographically authorized capability-based access control scheme with capability tokens, mostly focusing on files as the target process resources to control access to. The paper further presents a security and performance evaluation of the proposed scheme.
---------------------------------------------------------------------------


Strengths
---------------------------------------------------------------------------
+ Builds a fine-grained security solution based on ARMv8.3 security primitives with minor Linux kernel changes.
+ Addresses ambient authority issue of capability-based access control systems.
+ Well-defined, minimal API.
+ State-of-the-art is well presented.
+ Good flow in the paper.
---------------------------------------------------------------------------


Weaknesses
---------------------------------------------------------------------------
- Limited applicability to deployed or to-be-deployed systems, and thus potential impact.
- Unclear threat model and lack of relatable examples of what CAPACETI aims to protect against.
- Readers would benefit from a more detailed comparison with existing solutions.
- Unclear what the developer effort, requirements, and steps to use CAPACETI are.
- Mostly clear, but the paper requires another pass of proof-reading for grammar and typos.
---------------------------------------------------------------------------


Main Discussion of Paper
---------------------------------------------------------------------------
This paper explores the use of ARM PACs for capability-based intra-process access control for (primarily) files on Linux systems. This is an interesting idea, leveraging existing security primitives to realize and benchmark security solutions such as capability-based access control. The overall flow of the paper is good, and the paper reads clearly (albeit it would benefit from another round of proof-reading to eliminate lingering grammatical errors and typos).

Applicability:
- By design, because it builds on ARM security primitives, the proposed scheme is limited to ARM systems and specifically ones that employ CPUs that support PAC. As the authors explain, no commercial platforms exist today that satisfy those requirements with the exception of proprietary Apple systems.
- Applicability of CAPACETI is proven on (and designed around) Linux OS. Implicitly, through its dependency on `files_lookup_fd_raw`, the current implementation of the solution is limited to Linux OS with kernel versions >=5.11 when this API was introduced in the Linux kernel. Evidently, the authors test using a Linux kernel v5.14. This limits its potential impact.

Technical comments:
- Readers would benefit from a more thorough technical comparison between the proposed scheme and existing solutions such as capsicum, seccomp, OpenBSD pledge, and eBPF. This would better position CAPACETI in the body of existing literature and solutions, and more clearly surface its contributions. Right now, it is unclear to the reviewer whether the fine-grained capability access control scheme of CAPACETI can be achieved by slightly revisiting existing techniques (perhaps without the hardware acceleration for cryptographic primitives), or if it introduces a fundamentally different scheme.
- The proposed technique repurposes the upper 16 bits of the *nix file descriptor for the capability descriptor, mentioning that they "are seldom in use". However, that is not technically sufficient and warrants further investigation. What happens in the seldom cases where those bits _are_ used? Does deploying CAPACETI mean that fewer file descriptors are available to the system for use? What are the implications of hijacking file descriptor entries for the OS's functionality?

Assessment:
- A major gap in assessing potential impact and applicability is the lack of explanation behind developer effort, time, and requirements for employing CAPACETI - something that is critical for adoption of this scheme. Although the authors include quantitative metrics such as lines-of-code changes required, this does not shed sufficient light behind what the level of expertise and effort required by a developer is.
- For the performance assessment, it is measured that initialization of a process takes a substantial performance hit because of `capaceti_init` call. It would be beneficial to further unpack that; depending on type of workload and process application, it is possible to have short-lived, rapidly dying and respawning processes. The authors could provide more substantive evidence as to their reasoning behind accepting the (significant) increase in process spawn cost, perhaps outlining some example use cases that CAPACETI is most suited for because they e.g., include long-lived processes.
- The security assessment is useful, however incomplete without defining a specific threat model within which CAPACETI is expected to operate.
- Understandably, due to lack of available platforms to empirically carry out performance tests the authors revert to heuristics-based assessment of performance impact of their proposed scheme. That could be revisited in the near future, as machines that employ the ARM Cortex-X1C or ARM Cortex-A78C are getting ready to enter the market. It is also interesting to explore whether the Enhanced Pointer Authentication in ARM v8.6 can be used in CAPACETI.
---------------------------------------------------------------------------


Most prominent Strength or Weakness
---------------------------------------------------------------------------
Exploration of the idea is not sufficiently rigorous, or well-positioned in the body of existing research to surface its concrete contribution and novelty.
---------------------------------------------------------------------------



============================================================================
                            REVIEWER #4
============================================================================

---------------------------------------------------------------------------
Reviewer's Scores
---------------------------------------------------------------------------
           Clarity / Writing Style (1-5): 4
      Originality / Innovativeness (1-5): 3
    Impact of Ideas and/or Results (1-5): 3
            OVERALL RECOMMENDATION (1-5): 2

Summarize shortly the contributions of the paper in your own words.
---------------------------------------------------------------------------
The authors propose CAPACETI, a cryptographically-authenticated resource access control framework for securely allocating software resources. The resources are split into individual units called "c-units," which are allocated and deallocated using verified pointers.
---------------------------------------------------------------------------


Strengths
---------------------------------------------------------------------------
1. Well written.
2. The design of CAPCETI is explained well.
---------------------------------------------------------------------------


Weaknesses
---------------------------------------------------------------------------
1. The CAPACETI framework is not clearly explained.
2. Flawed security analysis.
3. Poor evaluation.
---------------------------------------------------------------------------


Main Discussion of Paper
---------------------------------------------------------------------------
The authors propose CAPACETI, a cryptographically-authenticated resource access control framework for securely allocating software resources. The resources are split into individual units called "c-units," which are allocated and deallocated using verified pointers.

Strengths:
The paper is reasonably well written, easy-to-follow, and the authors explain the basics of CAPACETI well. 

Weaknesses:
1. A majority of the paper is spent on the design of CAPACETI, yet it falls short on explaining the practical working of the framework. The authors could have used an example use case (perhaps the same Lighttpd benchmark example or a code snippet) to illustrate the working). 
2. Does the user enable CAPACETI during runtime?
3. Does the user get fine-grained control? For example, if the user trusts most of the code and requires validation only for a particular function or library, does the current framework allow for this kind of fine-grained access control?
4. The author's claim regarding brute-force security is flawed. Brute-forcing, a 64-bit ASLR, requires 2^64 (10^18) tries, while brute-forcing CAPACETI needs only 2^16 (10^4) tries since the fd field is constant. Thus the relative brute-force security offered by CAPACETI is less. Perhaps the authors could elaborate on the security assumptions more clearly. 
5. How would CAPACETI handle context switches? Especially if the context switch is between a user-level process and an OS/kernel-level process (e.g., Interrupts). 
6. The experimental evaluation is done using one benchmark. Perhaps a benchmark series (E.g., MiBench) would be more apt and relevant.
---------------------------------------------------------------------------


Most prominent Strength or Weakness
---------------------------------------------------------------------------
The paper presents an interesting idea but the improper evaluation and the lack of clarity regarding the practical implementation and the flawed security analysis makes this a weak paper.
---------------------------------------------------------------------------
```