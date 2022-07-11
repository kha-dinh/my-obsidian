Title: Touching the Untouchables Dynamic Security  Analysis of the LTE Control Plane 
Name: DINH DUY KHA
Student ID: 2019712308
# Summary
- Target System: The control component of Long Term Evolution (LTE) networks
- Vulnerabilities
	- Invalid plain messages
	- Invalid security protected messages
	- Bypassing mandatory security procedure
- Exploitation
	- Generate test cases for each  is using predetermined rules
	- Classify the unintended behaviours using a simple decision tree classifier
- Evaluation
	- Two tier-1 carrier networks and comercial networks are tested
	- The test found that RRC connection procedure is not encrypted or integrity protected (MAC), allowing attackers to inject spoofing messages
	- Some parts of the protocol does not have integrity checking
	- Replayed messages are accepted in some cases, which violate integrity
	- Some security procedure can be bypassed, such ass key agreement procedure.
- Defense
	- Protocol verification tools can be used
	- Manual bug patches.
- Future Work
	- Trying on different carrier and vendors
	- Extending to stateful fuzzing
	- 5G standard
- Questions for presenter
	- Q1: Can static protocol verifier be applied to find errors?
	- Q2:  How would the system perform in 5G standard?
- Discussion
	- Q2: In 5G standard, there could be some change to the network infrastructure and the protocol.


	