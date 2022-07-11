Title: Android on PC: On the Security of End-user Android Emulators
Name: DINH DUY KHA
StudentID: 2019712308
# Summary
- Target System:
	- Android emulators on PC
- Vulnerabilities & Exploitation:
	- User input processing:
		- Vulnerability: The input is transported as raw data or plaintext from the host OS (e.g., Windows Input Method (IME)) to Android IME through customized andoroid services. However, the interface (UDP, TCP, or virtual devices) are usually not protected and can be accessed by the attacker.
		- Exploits
			- Input spoofing: Knowing the format of the input, attackers can sends arbitrary inputs to Android IME to perform malicious actions
			- Input sniffing: The attacker can listen to the messages sent to Android IME and extract the information like key pressed.
	-  App installation:
		- Vulnerability: Android emulators allow all apps to access a shared folder containing the APK files for installation with READ_EXTERNAL_STORAGE permission. 
		- Exploits: Attackers can quickly replace the requested APK file with a modified APK for phishing, or malware and make the installer install unwanted apps.
	- Tab Management:
		- Vulnerability: Emulator introduces tab bars easily switch between apps. It is an additional feature implemented by the emulator and requires communication between the UI component and the android system to synchronize apps' states. However, the communication is not protected, so attackers can send spoofing messages to both sides.
		- Exploit: The attacker monitor the app's activity through the emulator. It inject malicious activity into a target app's activity to launch the malicious app. After, the malicious app send a spoofing message to the UI component to display the target tab as active, which hide the fact that the malicious app is actually in the foreground.
	- Shell and ADB
		- Vulnerability:
			- ADB: In most emulators, ADB is always active and expose unauthenticated channel to all users. ADB has been an attack vector on Android for a long time.
			- Exposed Shell: Aside from ADB, privileged shells are also exposed to the emulator, which is also unauthenticated.
		- Exploit: Attacker can gains root privileges of the android system and send any input events to the target through ADB and privileged shells.
- Evaluation
	- Six popular emulators are analyzed
	- All emulators are vulnerable to user input attacks. Four out of six is vulnerable to spoofing, two out of six is vulnerable to sniffing.
	- 3/6 emulators' apps installation are vulnerable
	- 4/6 emulators' tab management are vulnerable 
	- All emulators expose privileged shells and ADB 
- Defense
	- The author suggest application-layer protection (e.g., SSL or TLS) over the communication between emulator and the guest Android system. This eliminate most sppofing and sniffing attacks.
	- Linux's virtual devices should be protected with access control.
	- For apps installation, APK should be stored in private location
	- For ADB attacks, ADB security policies should be followed, as suggested by previous works.
- Future Work
	- Extends the threat model to also cover host-side attacks.
	- Cover the emulation of other operation systems like MacOS.
	- Automated approaches for vulnerability detection.
- Questions for presenter
	- Q1:  Would the emulators still be usable with SSL in place?  Are there alternative approaches to enable authenticated communication?
	- Q2: What are the use case of android emulator except from playing games? 
	- Q3: Can the attacker escape virtualization with the attacks?
	- Q4: To conform ADB security policies, what are the challenges faced by the emulator developers?
# Discussion
- Q1: Emulators are implemented with performance in mind. Put SSL over the communication channel would brings overhead to the system, which would bring delays to the system.
- Q2: Most emulators are used to emulate mobile games. Enhancing the security would introduce overheads to the system, which is not desirable. I think alternative approaches could be used in stead of redesigning the system, like warning before app installation, or scanning  for malware in APKs.
- Q3: Some of the introduced attacks can send spoofing messages to both the guest android system and the host windows. If there are host-side vulnerability, it can be leveraged to exploit the host system.
- Q4: Some of the features of Android emulators are placed there for the ease of use and development. For instance, the UI component and the android guest system is separated and use message-based communication channels. Enabling ADB security policies would ultimately requires more designing to enable the same functionalities.