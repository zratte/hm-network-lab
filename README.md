# hm-network-lab
This repo will be used for my technical assessment submission for Human Managed.

Over 2.5 days, using GitHub Codespaces and Containerlab, I developed a site-to-site VPN solution to securely route simulated log traffic across a simulated insecure network. 
The primary objective for this project was to provide a means to securely transmit log traffic (syslog, UDP) from Site A, via the simulated insecure network, to a log collector located in Site B. 

Technologies Implemented: 
Infrastructure as Code: Containerlab, Docker, YAML
Networking & Security: WireGuard VPN, Static Routing, UDP Syslog (nc)
Development Environment: GitHub Codespaces (2-core) 


Ground Rules and Assumptions: 
IP Addressing: For internal segments, I used subnets 10.10.x.x and 10.20.x.x. To ensure a clear and defined 'unsecure' network segment, I reserved the RFC 5737 documented IP block 192.0.2.0/24. 

Assumptions (Day 1, Email also sent to Ma'am Grace): 
1. Given the choice between WireGuard and strongSwan, I'll go with WireGuard. The latter is older and, while solid, requires additional modules to function in the kernel. With WireGuard, most Linux kernels include the support by default. 
2. I’m assuming the client will have their systems configured to push logs to the log collector via UDP port 514 (Syslog standard).
3. The unsecure path will allow UDP packets between Site A and Site B to permit tunnel establishment between Site A and Site B using WireGuard on port 51820. 
4. I’ll go with lightweight Linux OS distributions (Alpine or Ubuntu) for firewall and rsyslog containers, as I want to keep the resource overhead low. 

Syslog assumptions:
For the Syslog component, I’ll assume standard UDP port 514 is the way to go. To generate traffic to test log routing, I will rely on nc (Netcat). 
- I am operating on the assumption that a typical GitHub Codespace of 2-cores would support 4 docker nodes in the network.


Resource Used: 
Containerlab Documentation: Used to figure out the topology.yml structure.
Draw.io: used to make the topology diagram
Youtube: watched tutorials on how to configure a YML file correctly.
AI Assistant (GeminiPro): I used an AI assistant to help troubleshoot a 100% packet loss issue during the WireGuard peering phase. It taught me how to use the wg show wg0 public-key command to verify cryptographic keys directly on the hardware instead of relying on standard ping errors.


How to use:

If you want to use it yourself:
1. Clone this repository into a Linux environment or Github Codespace.
2. Ensure Containerlab is installed.
3. Run the following command to deploy the topology:
   - sudo clab deploy -t topology.yml
  

To see my daily progress, troubleshooting steps, and screenshots of the project, check out LEARNING.md file.
