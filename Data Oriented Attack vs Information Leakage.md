Recent researches seems to focus on those two sub-policy of [[Memory Safety]]. 

Data-oriented Attack exploit the arbitrary write attack vector.
Could be prevented by data integrity: Data could only be written by allowable subjects.

Information Leakage exploit arbitrary leak attack vector.
Information leaks allows attacker to leak secret data, bypassing ALSR/stack canaries.
Spectre BCB (Bounds Check Bypass) could leak information
