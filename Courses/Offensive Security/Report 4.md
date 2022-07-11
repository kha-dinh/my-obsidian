Title: ROP is Still Dangerous: Breaking Modern Defenses
Name: DINH DUY KHA
Student ID: 2019712308
# Summary
- Target System: C programs with ROP defenses
- Vulnerabilities:
	- Some defeses ensure that every ret instruction must follow by a call instruction. However, ROP attack are still possible
	- Defenses that classify the execution as "normal" and "gadget" by be bypassed by using "normal" gadget
	- Some defenses that inspect the history to detect ROP attacks only store  a limited amount of history. Such defence can be bypassed by flushing the history to hide ROP attacks.
- Exploitation
	- Using call-preceded only ROP can by using only
	- Information hiding
	
- Evaluation
	- Real online stores are analyzed and are found to be vulnerable.
	- The paper also shows that the attacker can perform exploits while  keeping his anonymity.
	- Vulnerabilities are reported to merchants and CaaS providers
- Defense
	- Protocol verification tools can be used
	- Manual bug patches.
- Future Work
	- Only checkout functionality are analyzed. Other functions are future works, e.g., cancle, return, subscription, ...
- Questions for presenter
	- Q1: How is protocol verifier applied to CaaS?
	- Q2: What security guarantee does protocol verifier provides?
	- Q3: What do you think about fuzzing for finding bugs in protocol?
- Discussion
	- Q1: Most protocol verifier works on well-defined cryptographic protocols. However, the APIs for CaaS and merchants are arbitrary. There must be some challenges in applying them to APIs.
	- Q3: There have been many protocol fuzzing works recently. I wonder if they can find such bugs presented in the paper.

	