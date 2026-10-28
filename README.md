# Practical-hacking-
Practical 1: Network Scanning Using Nmap and Zenmap
1. Aim
To perform network scanning using Nmap and Zenmap, identify open ports, detect services and understand different scanning techniques.
2. Requirements
- Nmap
- Zenmap (GUI front-end of Nmap)
- Computer with a permitted lab target
3. Procedure
Step 1: Check network configuration
ipconfig /all


Step 2: Check target connectivity
ping 192.168.56.102


Step 3: Perform host discovery
nmap -sn 192.168.1.0/24


Step 4: Perform port scanning
nmap 192.168.56.102
nmap -p 22,80,443 192.168.56.102


Step 5: Detect services and versions
nmap -sV 192.168.56.102
nmap -sC -sV 192.168.56.102 -oN scan_results.txt


Step 6: Perform different scan types
nmap -sS -p 1-100 192.168.56.102
nmap -sF -p 1-100 192.168.56.102
nmap -sN -p 1-100 192.168.56.102
nmap -sX -p 1-100 192.168.56.102
nmap -sA -p 1-100 192.168.56.102


- -sS — SYN Scan
- -sF — FIN Scan
- -sN — NULL Scan
- -sX — XMAS Scan
- -sA — ACK Scan

Step 7: SNMP and NetBIOS enumeration
nmap -sU -p 161 192.168.56.102
nmap --script nbstat.nse -p 137 192.168.56.102

Note: Ye sample IPs PDF se hain. Actual scanning sirf instructor ke provided, authorized lab target par karna.

4. Observation
Nmap identifies active hosts, port states and available services. In my observed output, the host was reported as up, but all 1000 scanned TCP ports were filtered.

5. Result
Network scanning was studied using Nmap and Zenmap. Different scanning techniques, port states, service detection and basic firewall filtering were examined.
_____________________________________________________________________________________________________________________________________________________________________________________________________

Practical 2: Network Commands — Ping, Ifconfig, Netstat, Traceroute
1. Aim
To study network commands used to check host reachability, interface configuration, active connections and the path packets take to a destination.

2. Requirements
- Windows Operating System
- Command Prompt / PowerShell
  
3. Procedure
Step 1: Ping — Check host reachability
ping 192.168.56.102


Step 2: IPConfig — Display network configuration
ipconfig /all


Step 3: Netstat — Display active connections and listening ports
netstat -ano


Step 4: Traceroute — Display the path to a destination
tracert 8.8.8.8


4. Observation
1. Ping: Displays replies, packet loss and round-trip time.
2. IPConfig: Displays IP address, subnet mask, default gateway and MAC address.
3. Netstat: Displays active connections, listening ports and process IDs (PIDs).
4. Traceroute: Displays the network hops between the computer and the destination.

5. Result
The network commands were studied to check host reachability, view network configuration, identify active connections and trace the route to a destination.
____________________________________________________________________________________________________________________________________________________________________________________________________________________

Practical 3: Reconnaissance and WHOIS

1. Aim
1. To perform passive and active footprinting of a target domain using public information.
2. To use WHOIS lookup and search engines to gather domain information.
3. To perform DNS enumeration using different DNS record types.

2. Requirements
- Windows Operating System
- Command Prompt / PowerShell
- Web browser
- WHOIS lookup tool

3. Procedure:
   
Step 1: Resolve the domain's IP address
nslookup www.google.com


Step 2: Check different DNS records
nslookup -type=A google.com
nslookup -type=MX google.com
nslookup -type=NS google.com
nslookup -type=TXT google.com
nslookup -type=CNAME www.google.com


Step 3: Perform Reverse DNS lookup
nslookup 142.251.152.119


Step 4: Perform WHOIS lookup
whois google.com


If the WHOIS command is unavailable in Windows, use an online WHOIS lookup tool.

Step 5: Inspect HTTP headers
curl -I https://google.com


Step 6: Perform search-engine reconnaissance
site:google.com filetype:pdf
site:google.com inurl:login
site:google.com intitle:"login"


Enter these queries into a web search engine.

Step 7: Save DNS information to a file
nslookup example.com > footprint_dns.txt


4. Observation
1. DNS lookup provides the IP address associated with a domain.
2. DNS records provide information about mail servers, name servers and text records.
3. WHOIS provides domain registration information.
4. HTTP headers provide server response and security-related information.
5. Search engines help find publicly indexed information.

5. Result
Reconnaissance and WHOIS lookup were studied to collect publicly available domain information and perform DNS enumeration.
_____________________________________________________________________________________________________________________________________________________________________________________________________________

Practical 4: Password Security, Dictionary Attacks, CrypTool
1. Aim
1. To study password entropy, hashing and salting.
2. To demonstrate a dictionary attack using a test password.
3. To understand encryption and hashing using CrypTool.
  
2. Requirements
- Windows Operating System
- Python 3
- CrypTool
- Windows PowerShell

3. Procedure
Step 1: Check Python installation
python --version


If it does not work, try:
py --version


Step 2: Calculate password entropy

import math

pwd = input("Enter a test password: ")
charset = 0

if any(c.islower() for c in pwd):
    charset += 26
if any(c.isupper() for c in pwd):
    charset += 26
if any(c.isdigit() for c in pwd):
    charset += 10
if any(not c.isalnum() for c in pwd):
    charset += 32

entropy = len(pwd) * math.log2(charset) if charset else 0

print("Length:", len(pwd))
print("Estimated entropy:", round(entropy, 1), "bits")



Step 3: Demonstrate salted and unsalted hashing

import os
import hashlib

password = b"TestPass123"

print(hashlib.sha256(password).hexdigest())
print(hashlib.sha256(password).hexdigest())

s1 = hashlib.scrypt(password, salt=os.urandom(16),
                    n=16384, r=8, p=1, dklen=20).hex()
s2 = hashlib.scrypt(password, salt=os.urandom(16),
                    n=16384, r=8, p=1, dklen=20).hex()

print("Salted hash 1:", s1)
print("Salted hash 2:", s2)


Step 4: Demonstrate a dictionary attack on a test password

import hashlib

my_password = "password123"
target_hash = hashlib.sha256(my_password.encode()).hexdigest()

wordlist = ["123456", "qwerty", "password123", "letmein", "admin"]

for word in wordlist:
    if hashlib.sha256(word.encode()).hexdigest() == target_hash:
        print("Password found:", word)
        break
else:
    print("Not found in wordlist")


Step 5: Check file integrity using SHA-256

Run these commands in Windows PowerShell:
"Hello, Cryptography Lab!" | Set-Content message.txt
Get-FileHash .\message.txt -Algorithm SHA256


Change the text and calculate the hash again:
"Hello, Cryptography Lab!!" | Set-Content message.txt
Get-FileHash .\message.txt -Algorithm SHA256


Step 6: Perform encryption and hashing using CrypTool
1. Open CrypTool.
2. Select the Encrypt/Decrypt menu and choose a cipher such as AES or RSA.
3. Enter plaintext and generate a key.
4. Observe the ciphertext.
5. Open the Hash menu and select SHA-256 or MD5.
6. Enter text and observe the hash digest.
7. Change one character and observe the difference in the hash.

4. Observation
1. Password entropy estimates password strength.
2. Unsalted hashes of the same password are identical.
3. Salting produces different stored hash values for the same password.
4. A dictionary attack checks candidate passwords against a target hash.
5. A small wordlist may find a weak password but may not find a strong password.
6. A small change in the input produces a very different hash.
   
5. Result
Password entropy, hashing, salting, dictionary attacks, file integrity checking and encryption using CrypTool were studied.
_____________________________________________________________________________________________________________________________________________________________________________________________________________________

Practical 5: Wireshark & Network Traffic Analysis
1. Aim
1. To capture and inspect network packets.
2. To identify common protocols such as DNS, ICMP, TCP and ARP.
3. To use display filters to find relevant network traffic.

2. Requirements
- Windows Operating System
- Wireshark
- Windows PowerShell
- Internet connection

3. Procedure
Step 1: Check network configuration

Open PowerShell and execute:
ipconfig /all


Identify the active network adapter and IPv4 address.

Step 2: Generate sample network traffic

Generate ICMP traffic using Ping:
ping example.com


Generate DNS activity:
Resolve-DnsName example.com


Step 3: Capture packets in Wireshark
1. Open Wireshark.
2. Select the active network interface, such as Wi-Fi or Ethernet.
3. Click Start Capturing.
4. Run the above commands in PowerShell.
5. Stop the capture.
6. Inspect the captured packets.

Step 4: Apply display filters

Enter these filters in Wireshark's display filter bar.
Filter	Purpose
arp	Displays ARP packets
dns	Displays DNS traffic
icmp	Displays ICMP packets, including Ping
tcp	Displays TCP packets
ip.addr == 192.168.56.102	Displays packets involving the specified IP address

Step 5: Identify packet details

Select a packet and examine the following details:
- Source: Sender's address.
- Destination: Receiver's address.
- Protocol: Protocol used by the packet.
- Length: Packet size.
- Info: Brief information about the packet.

Step 6: Save the capture

In Wireshark, select File → Save As and save the capture as:
lab-capture.pcapng


4. Observation
1. Wireshark captures and displays network packets.
2. Different protocols can be identified using display filters.
3. Packet details include source, destination, protocol, length and information.
4. Captured network traffic can be saved in a .pcapng file.

5. Result
Network traffic was captured and analyzed using Wireshark. Common protocols were identified, display filters were applied and the packet capture was saved.
__________________________________________________________________________________________________________________________________________________________________________________________

Practical 6: Python Keylogger Practical

1. Aim
1. To understand how keyboard input can be captured by a program.
2. To demonstrate keyboard-input handling using Python.
3. To understand the security and privacy risks of keyloggers.

2. Requirements
- Windows Operating System
- Python 3
- Windows PowerShell
- Notepad or another code editor

3. Procedure
Step 1: Check Python installation

Open PowerShell and execute:
python --version


If it does not work, try:
py --version


Step 2: Create a Python demonstration program

Execute:
notepad "$HOME\keyboard_demo.py"


while True:
    text = input("Enter sample text (type exit to stop): ")

    if text.lower() == "exit":
        print("Demo stopped.")
        break

    print("Input received:", text)


Step 3: Execute the program
python "$HOME\keyboard_demo.py"

Alternatively:
py "$HOME\keyboard_demo.py"


Step 4: Enter sample text

Example output:

Enter sample text (type exit to stop): Hello
Input received: Hello

Enter sample text (type exit to stop): exit
Demo stopped.


Step 5: Observe the result

The program reads text entered into its own console and displays the received input. It is a keyboard-input demonstration, not a full system-wide keylogger.

Step 6: Understand the security risks

A malicious keylogger may capture passwords, messages and other sensitive information. Use trusted software, keep security tools updated and avoid running untrusted scripts.

4. Observation
1. Python can read keyboard input using the input() function.
2. The entered text is displayed by the program.
3. The program stops when the user enters exit.
4. A malicious keylogger can create privacy and security risks.

5. Result
Keyboard-input handling was demonstrated using Python, and the security and privacy risks associated with keyloggers were studied.
_________________________________________________________________________________________________________________________________________________________________________________

Practical 7: ARP Poisoning & Cain & Abel
1. Aim
1. To understand ARP and how local-network address resolution works.
2. To understand the concept and effects of ARP poisoning.
3. To identify suspicious ARP changes and understand defensive measures.

2. Requirements
- Windows Operating System
- Windows PowerShell
- Wireshark
- Isolated virtual lab, if available

3. Procedure
Step 1: Display the ARP cache

Open PowerShell and execute:
arp -a


This displays the IP-to-MAC address mappings stored on the computer.

Step 2: Display network neighbour entries
Get-NetNeighbor -AddressFamily IPv4


This displays IPv4 neighbour entries and their states.

Step 3: Check network configuration
Get-NetIPConfiguration


Identify the active network interface and default gateway.

Step 4: Generate normal network traffic

Ping your own default gateway using its actual IP address:
ping <your-default-gateway-IP>


Then display the ARP cache again:
arp -a


Compare the results before and after the ping. The gateway's ARP entry may appear or be refreshed.

Step 5: Inspect ARP packets in Wireshark
1. Open Wireshark.
2. Select the active network interface.
3. Start capturing packets.
4. Enter the display filter:
arp

5. Generate ordinary traffic to your own gateway.
6. Stop capturing and inspect the ARP requests and replies.
7. Look for unexpected changes in IP-to-MAC mappings.

Step 6: Study ARP poisoning and Cain & Abel

ARP poisoning, also called ARP spoofing, occurs when forged ARP messages cause a device to associate an IP address with an incorrect MAC address.

Cain & Abel is a legacy Windows security tool historically associated with password recovery and network-security demonstrations. Its availability and compatibility may vary.

Step 7: Apply defensive measures
- Monitor unexpected IP-to-MAC address changes.
- Use Dynamic ARP Inspection on supported managed switches.
- Enable appropriate switch-port security.
- Segment networks and secure network infrastructure.
- Use encrypted protocols such as HTTPS.

4. Observation
1. The arp -a command displays IP-to-MAC address mappings.
2. Wireshark displays ARP requests and replies.
3. Unexpected changes in IP-to-MAC mappings may indicate suspicious activity.
4. Dynamic ARP Inspection and network monitoring help defend against ARP poisoning.

5. Result
ARP address resolution, ARP poisoning, traffic analysis using Wireshark and defensive measures were studied. The purpose and historical role of Cain & Abel were also examined.

__________________________________________________________________________________________________________________________________________________________________________________________________
