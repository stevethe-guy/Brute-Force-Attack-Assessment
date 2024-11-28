# Brute-Force-Attack-Assessment
Objective
The goal of this Capture the Flag (CTF) project was to investigate a brute force attack and achieve the following objectives:
1.	Identify the attacker's IP address.
2.	Determine which accounts were affected.
3.	Extract timestamps of attack activity using utmpdump.
4.	Verify if the attacker created any accounts.
5.	Analyse the duration of each SSH session to estimate time spent.
________________________________________
Findings
1. Attacker’s IP Address
The attacker utilized the IP address 65.2.161.68, originating from Mumbai, India. This IP was verified using the curl command to query public geolocation services:
•	Details of the Attacker's IP:
o	IP Address: 65.2.161.68
o	City: Mumbai
o	Region: Maharashtra
o	Country: India
o	Coordinates: 19.0728, 72.8826
o	ISP: Amazon.com, Inc.
 
________________________________________
2. Compromised Accounts
   
At least two accounts were affected during the attack:
•	Root account: Accessed multiple times by the attacker.
•	Cyberjunkie: A new account created by the attacker with elevated privileges via sudo.
________________________________________
3. Failed Login Attempts and Successful Attempts

Looking at the auth.log, numerous failed attempts were detected for multiple accounts, indicating a brute-force method. These were then followed by successful attempts to gain access to the system.
 
________________________________________
4. Activity Timestamps

Using the command grep Accepted auth.log, successful login attempts were extracted from system authentication logs. These logs revealed the following timestamps for granted access:
•	March 6, 06:19:54: Root access from IP 203.101.190.9 (a potential earlier probe or a secondary attack vector).
•	March 6, 06:32:44: Root access from IP 65.2.161.68.
•	March 6, 06:37:34: Cyberjunkie account accessed from IP 65.2.161.68.
________________________________________
5. Unauthorized Account Creation/Persistence
   
The attacker created a new account named "cyberjunkie". This account was granted administrative privileges using sudo, giving the attacker elevated access to the system. This confirms that the attacker established persistence on the system.

6. Duration of SSH Sessions
   
Based on the analysis of the logs, the attacker maintained SSH sessions for an average duration of 5 minutes. This indicates short bursts of activity, likely to minimize detection.
 
Suggestions to Prevent Brute Force Attacks

1.	Use Strong Authentication Measures:
o	Enforce key-based authentication for SSH instead of passwords.
o	Enable multi-factor authentication (MFA) for all accounts.
2.	Limit Login Attempts:
o	Implement tools like Fail2Ban or DenyHosts to block IPs after repeated failed login attempts.
3.	Monitor and Secure Privileged Accounts:
o	Regularly audit accounts with sudo privileges.
o	Disable unused or suspicious accounts promptly.
4.	Enable Network Restrictions:
o	Use IP whitelisting to restrict SSH access to trusted IPs only.
o	Deploy geofencing to block traffic from regions unrelated to your operations.
5.	Deploy Real-Time Monitoring Tools:
o	Use Intrusion Detection Systems (IDS) and SIEM solutions to monitor logs and detect anomalies in real-time.
6.	Enforce Strong Password Policies:
o	Require complex, unique passwords for all accounts.
7.	Conduct Regular System Updates:
o	Patch SSH services and other software regularly to fix vulnerabilities.
8.	Educate Users:
o	Provide training on security best practices, such as recognizing phishing attempts and avoiding weak passwords.
________________________________________
Conclusion

The analysis revealed critical vulnerabilities in the system exploited by the attacker, such as weak credentials and lack of login restrictions. Immediate implementation of the suggested measures will significantly reduce the risk of future brute force attacks and enhance overall system security.
