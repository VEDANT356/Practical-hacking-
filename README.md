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

