Title: How to Shop for Free Online  Security Analysis of Cashier-as-a-Service Based Web Stores
Name: DINH DUY KHA
Student ID: 2019712308
# Summary
- Target System: The paper target third-party cashier (CaaS) providers such as PayPal, Amazon Payments
- Vulnerabilities + Exploitation: Commercial software, opensource software and close-sourced software are evaluated
	* NopCommerce
		- PayPal Integration: Paying an incorrect amount to Paypal to checkout from victim
			- Vulnerability: The logic of the merchant API finishOrder does not check for the gross value of the payment. The value can be freely modified by an attacker.
			- Exploit: The attacker modify the finishOrder API call with a malicious value to pay less than the intended value but still able to checkout.
		- Amazon Simple Pay Integration: Attacker paying himself to checkout from victim
		- Vulnerability: The CaaS sends the victim the payment confirmation that is signed, but from an invalid transaction. The victim, on receiving the message, only check some part of the response, which leads him to believe that the message is valid.
		- Exploit: The attacker make an account as a seller on Amazon. He makes an order that is pending payment on the victim store. The attacker then sends a finish order message to CaaS (but for his store), with the returnURL of the victim. CaaS will redirect the shopper (attacker) to the victim's store, which the information that the order has been paid.
- Interspire Exploits
	- PayPal Integration: Paying for a cheap order to checkout an expensive one
		- Vulnerability: As long as a signed order ID is found in the SUCCESS state (a session variable), the function updateOrderStatus function of CaaS will mark the corresponding order with the same ID as paid.
		- Exploit: An attacker create two login sessions. In the first session, the attacker select a cheap item, checkout, and delay the order finsh, which makes the SESSION["result"] value become success. Then, the attacker select an expensive item and make the payment fail. When it fail, it sends a signed orderID to the attacker. He use this orderID to set it to the first session and finish the checkout.
	- Paypal integration: Stealing payment notification and replay
		- Vulnerability: When orderID is not given, the CaaS will check for the cookie value ORDER_ID.
		- Exploit: The attacker set the OrderID to be empty and IPNhandler URL to his URL. This will make PayPal IPN handler send a signed by the CaaS. The attacker only need to place new order with the same price, set the cookie ORDER_ID to the ID of the order, call victim's IPN hander and replay   the message.
	- Google checkout integration: Adding item to the cart after checkout
		- Vulnerability: The order for transaction is not generated  until the CaaS send confirmation to the merchant through IPN. The process is also not atomic.
		- Exploit: After receiving IPN handler request, attacker can still call updateCart to change his cart, allowing him to checkout many more item.
	- Amazon Simple Pay Integration: Avoid payment: mentioned in other paper.
	- Amazon Integration: interdependency of message authenticity and certificate authenticity
		- Vulnerability: The SDK of amazon payment has a function that allow attackers to provide their own certificate. 
		- Exploit: The attacker acts as a fake CaaS and use his certificate to sign any URL. Because the certificate check is valid, it allows the attacker to send checkout messages to the merchant.
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

	