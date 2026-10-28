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

Viva Questions — abhi yaad karne ke liye
Q1. What is Nmap?

Nmap stands for Network Mapper. It is a tool used for network discovery and security auditing.

Q2. What is Zenmap?

Zenmap is the graphical user interface (GUI) for Nmap.

Q3. What is port scanning?

Port scanning is the process of checking ports on a host to identify their states.

Q4. What is a SYN scan?

A SYN scan is a half-open TCP scan that checks port responses without completing the full TCP connection.

Q5. What is the use of -sV?

The -sV option detects the services and their versions running on open ports.

Q6. What is an ACK scan?

An ACK scan helps determine whether ports are filtered by a firewall. It does not directly identify open ports.

Q7. What is a filtered port?

A filtered port is a port whose state cannot be determined because a firewall or network filter blocks or affects the scan responses.
