1. Identify Active Machines
	1. Ping Sweep
		1. Benefits
			1. Rapid to perform
			2. Sweep of IP address range
			3. Created to identify when a host is a alive
		2. Tools
			1. OS tool
				1. Ping
					1. One at a time
					2. `ping -c 1 X.X.X.X`
					3. Wring ping script to ping list
				4. fping
					1. Install in Linux
					2. `fping -c 1 iplist | tee outputlist`
			3. Nmap (network mapper)
				1. `nmap -PE X.X.X.1-254`
					1. Install in Linux
					2. Kali has by default
		3. Next Steps
			1. Save output, then do a reverse DNS lookup
				1. Is the host registered in the DNS with a fully qualified domain name (FQDN)?
				2. Can we figure out the services running based upon the name?
		3. If Ping Does Not Work
			1. ICMP (Echo Request/Echo Reply)
				1. Can be blocked at firewall
				2. Can be turned off on devices
			3. Different type of ICMP can be used
				1. Try to use timestamps
				2. At least 9 different types of ICMP can be used
				1. Tools
					1. OS Tool
						1. nping allows for different ICMP types
					2. Nmap
		3. If ICMP Does Not Work
			1. ARP, TCP, UDP traffic
		2. Ping Sweep Countermeasures
			1. Ping Sweeps are not just annoying
				1. Can be an indicator for an attack
				2. Loki2 used ICMP echo request/reply packet to covertly send data (~1997)
					1. Could be still used today
			2. Detection
				1. Using IDS such as Snort (Security Onion provides web frontend)
				2. Can set to alert for ping sweeps
				3. nmap scans too - so ARP, TCP scans of network
			4. Prevention
				1. Evaluate the need for types of ICMP traffic
				2. Do you need echo request/reply from the internet into your network
					1. Probably not
					2. Block ICMP messages at the external firewall
					3. Only allow into the DMZ
						1. Echo reply, host unreachable, time exceeded packet
					2. Maybe do access control list (ACL) to allow your ISP to send
						1. Echo request to check on connectivity to them
						2. But not all ping sweeps
3. Identify What Services are Running/Listening
	1. Port Scanning
		1. Want to determine the state of the port
			1. Probes each port on a system
			2. Looking for services to attack
			3. Trying to determine the OS
			4. TCP or UDP scan?
				1. TCP is more reliable
		2. Open ports usually return a service banner that can be interpreted
			1. Other actions possible
		3. Nmap Port States
			1. Open
				1. Accepting connections (avenue for attack)
			2. Closed
				1. Accessible, but nothing listening
			3. Filtered
				1. Packet doesn't reach port (think firewall)
			4. Unfiltered
				1. Accessible, but ?open or ?close (ACK scan)
			5. Open|Filtered
				1. Open port or filtered?, but won't respond (FIN, NULL, XMAS)
			6. Closed|Filtered
				1. Closed or filtered? (IP ID)
		4. TCP Port Scanning
			1. Flags
				1. Describes status of a packet and the communication that goes with it
				2. Bits set in packet header, describe a specific behavior
			3. TCP flags enable penetration testers or attackers to craft TCP packets designed to gain information about running applications or services
			4. Full Connection Scan
				1. `nmap -sT x.x.x.0/24`
				2. Does the full 3-way handshake
			3. Half Open Connection Scan
				1. `nmap -sS x.x.x.0/24`
				2. Just does SYN and SYN/ACK
			3. TCP FIN Scan / Inverse TCP Flag
				1. `nmap -sF x.x.x.x`
				2. Sends requests to close nonexistent connection
					1. Client sends FIN to target port
					2. RST/ACK comes back it's a closed port
				3. Sending a FIN packet to an open port
					1. RFC just specifies to not respond
			2. TCP Null Scan
				1. No flags set
					1. See what target responds with
					2. Use results to figure out OS
					3. RFC implem
			4. TCP XMAS Tree Scan
				1. `nmap -sX x.x.x.x`
				2. FIN, PSH, URG flags set
				3. This is illegal/illogical
				4. Result's monitored to see how system responds
				5. Closed ports should give RST
				6. Others that get this combination also send RST
				7. But some answer open|filtered (some Linux)
			8. TCK ACK Scan
			9. TCP Windows Scan
				1. `nmap -sW x.x.x.x`
			2. UDP Scan
				1. May want to only scan known ports
		5. Stack Fingerprinting
			1. Nuances between one vendor's IP stack implementation and another's
		2. Port Scanning Countermeasures
			1. Port scanning is effective
			2. Detection
				1. Intrusion detection of port scanning activity
					1. Real time alerts (email / text message)
					2. Early warning that you might see an attack
				3. Firewalls usually can also detect port scanning
			4. Prevention
				1. Can't completely prevent
				2. Disable unnecessary services
				3. Block all traffic to all ports unless traffic is explicitly approved
			4. Extra Notes:
				1. Just having firewalls to filter/block traffic and IDS to log activity doesn't solve the problem
					1. Make sure the above tools are tested
				2. Scan your own networks
					1. Use the same tools an attacker would use
					2. See what the attacker would see
				3. Be careful using Intrusion Prevention Systems
					1. Could accidently block yourself
		2. Service and Version Detection
			1. Port scanning just reveals open ports and the common services running on the port
				1. May not be the actual service running on that port (e.g., running ssh on port 80)
		2. OS Detection
			1. Determines OS based on response behavior