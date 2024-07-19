# Analyze Network Attacks

## Scenario
You work as a security analyst for a travel agency that advertises sales and promotions on the company’s website. The employees of the company regularly access the company’s sales webpage to search for vacation packages their customers might like.

One afternoon, you receive an automated alert from your monitoring system indicating a problem with the web server. You attempt to visit the company’s website, but you receive a connection timeout error message in your browser.

You use a packet sniffer to capture data packets in transit to and from the web server. You notice a large number of TCP SYN requests coming from an unfamiliar IP address. The web server appears to be overwhelmed by the volume of incoming traffic and is losing its ability to respond to the abnormally large number of SYN requests. You suspect the server is under attack by a malicious actor.

You take the server offline temporarily so that the machine can recover and return to a normal operating status. You also configure the company’s firewall to block the IP address that was sending the abnormal number of SYN requests. You know that your IP blocking solution won’t last long, as an attacker can spoof other IP addresses to get around this block. You need to alert your manager about this problem quickly and discuss the next steps to stop this attacker and prevent this problem from happening again. You will need to be prepared to tell your boss about the type of attack you discovered and how it was affecting the web server and employees.

## Objective

To analyze and document a recent security incident affecting the travel agency's website. This report will identify the type of network attack responsible for the service interruption, explain how the attack occurred, and detail its negative impact on the website's functionality. Through this analysis, the report aims to provide insights into mitigating similar attacks in the future and improving overall network security posture.

### Skills Learned

- Identification and analysis of network intrusion attacks
- Utilization of packet sniffing tools (like Wireshark) for traffic analysis
- Understanding the impact of denial-of-service (DoS) attacks on web server performance
- Communication of technical findings and recommendations

### Tools Used

- Packet sniffer (Wireshark) for capturing and analyzing network traffic
- Word processing software for document creation

## Steps

### Step 1: Initial Appearance and Normal Response to Attacker's SYN Requests

When the attacker (IP address: 203.0.113.0) first appears in the log (items 52-54), the web server responds normally by acknowledging the attacker's SYN request with a SYN, ACK packet sequence. During this time:
- Log Details: Entries 52-54 show the first contact between the attacker and the web server.
- Normal Response: The web server responds to the SYN request, indicating it's ready to establish a connection.

At this point, the web server can still handle regular visitor traffic, as seen with successful interactions from other users (highlighted in green). For example, an employee (IP: 198.51.100.14) completes a handshake and requests a webpage (entries 55, 56, 58, 60, 62).

![image](https://github.com/user-attachments/assets/046ea05b-be3f-4cd6-9d2a-1451d5d1a6ae) 

> *Ref 1: Normal SYN requests and server responses before the attack intensifies.*

### Step 2: Escalation of Attack and Impact

In the following rows of the log, the web server begins to struggle due to a high volume of SYN requests from the attacker (IP: 203.0.113.0). The attacker intensifies the attack by sending multiple SYN requests per second. Rows highlighted in yellow indicate failed communication attempts between legitimate employees (green entries) and the web server.

Two types of errors appear:

- 504 Gateway Time-out: This error occurs when the web server fails to respond promptly, causing the gateway server to send an error to the visitor's browser.
- RST, ACK Packet: The web server sends this packet to visitors if it doesn't receive the expected SYN, ACK packet, terminating the connection attempt.

These errors demonstrate the impact of the SYN flood attack, disrupting normal operations and causing timeouts for legitimate users.

![image](https://github.com/user-attachments/assets/535aff87-3766-4e2c-b4c4-aadfdda6cb33) 

> *Ref 2: Escalating SYN requests and the server's initial difficulties in handling them.*

### Step 3: Web Server Overwhelmed and Stoppage

Continuing through the log, it can be observed that past log 125, the web server stops responding to legitimate visitor traffic. Instead, visitors start consistently encountering errors, preventing them from establishing or maintaining connections with the server. Only entries related to the attack (from IP 203.0.113.0) are logged at this point. Indicating a direct denial of service (DoS) SYN flood attack from a single source.

![image](https://github.com/user-attachments/assets/5dce9836-191e-431e-ad52-06d3d725360c) 

> *Ref 3: Server overload with continuous SYN requests and error messages experienced by legitimate visitors.*

### Step 4: Write the Cybersecurity Incident Report

The report below documents the type of network attack that was identified and explains how it disrupts normal website operations.

> [!IMPORTANT]
> [Cybersecurity Incident Report: Network Attack Analysis](https://docs.google.com/viewer?url=https://github.com/user-attachments/files/16277210/Cybersecurity.Incident.Report_.Network.Attack.Analysis.docx)
