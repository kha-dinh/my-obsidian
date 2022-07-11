Title: Exploiting the Laws of Order in Smart Contracts
Name: DINH DUY KHA
Student ID: 2019712308

- Target System: Smart Contracts
- Vulnerabilities:
	- The concurrent execution model of smart contracts creates bugs that arise from the ordering of events.
	- There are two types of event-ordering bugs, *off-chain asynchronous callbacks* and *on-chain transaction ordering*.
		- Off-chain asynchronous callback vulnerability exploits the callback functions that return asynchronously. For instance, in the Casino smart contract, when multiple  players place bets concurrently, all bet are are accepted but only one is rewarded when winning.
		- On-chain transaction ordering is sometime the smart contract fail to order multiple requests.
- Exploitation
	- The author developed a dynamic analysis technique to find bugs in concurrent events of smart contract.
	- Symbolic execution is used to enumerate different paths and input values of the smart contract. The baseline DSE is augmented to recognize events in happen-before relations. 
-  Evaluation
	- The system is used to find bugs in 5000 open-source smart contract.
	- The results shows 836 event ordering violations.
- Defense
	- No defense is proposed
- Future Work
	- Automatically fixing concurrency bugs.
- Questions for presenter
	- Q1. Can these kind of bug be determined with static code analysis?
	- Q2. What can of source code transformation can eliminate those kind of ordering bugs?
- Discussion
	- The system raise a lot of false positive. It is a future direction to determine a EO violation is exploitable or not.
	- Symbolic execution is an expensive approach that requires a lot of computation power and time. It is interesting to combine it with fuzzing techniques.
