# Network Security Traffic & Firewall Analysis

A hands-on network security project focused on analyzing network scanning techniques, TCP/IP traffic behavior, packet-level communication, and the impact of firewall filtering.

The project uses two Kali Linux virtual machines in a controlled environment. One system acts as the scanner using Nmap/Zenmap, while the second system acts as the target, running an Apache web service, capturing traffic with Wireshark, and applying UFW firewall rules.

## Project Objectives

The main objective of this project is to understand what actually happens at the packet level during network scanning and how firewall rules affect network communication.

The project focuses on:

- Performing and comparing different Nmap scanning techniques.
- Observing TCP/IP packet behavior using Wireshark.
- Understanding TCP flags and connection behavior.
- Identifying differences between open, closed, and filtered ports.
- Analyzing network behavior before and after firewall activation.
- Connecting network scanning results with the actual packets observed on the network.

## Environment

The project was implemented using a virtualized network environment with two Kali Linux systems:

```text
Kali Linux I
Nmap / Zenmap Scanner
        |
        |  Virtual Network
        |
        v
Kali Linux II
Apache Web Server
UFW Firewall
Wireshark Packet Capture
```

## Technologies & Tools

- Kali Linux
- Nmap
- Zenmap
- Wireshark
- UFW Firewall
- Apache Web Server
- TCP/IP
- Virtualization

## Network Scanning

Multiple Nmap scanning techniques were used to observe how different probes interact with the target system:

### TCP SYN Scan (-sS)
Used to analyze half-open TCP connection behavior without completing the full TCP handshake.

### TCP Connect Scan (-sT)
Used to establish a complete TCP connection and observe the full connection process.

### Xmas Scan (-sX)
Used to analyze responses to TCP packets containing FIN, PSH, and URG flags.

### ACK Scan (-sA)
Used to analyze firewall filtering behavior and determine whether traffic is being filtered.

### UDP Scan (-sU)
Used to examine UDP services and compare UDP scanning behavior with TCP-based scanning.

### Network Scanning Results

The following screenshots show representative Nmap/Zenmap scan results collected from the target system.

#### TCP SYN Scan (-sS)

![TCP SYN Scan](screenshots/02-network-scanning/Screenshot%202024-10-29%20020233.png)

The SYN scan identified TCP port 80 as open, demonstrating the behavior of a half-open TCP scan against the target.

#### TCP Connect Scan (-sT)

![TCP Connect Scan](screenshots/02-network-scanning/Screenshot%202024-10-29%20021509.png)

The TCP Connect scan completed the connection process and also identified TCP port 80 as open.

#### Xmas Scan (-sX)

![Xmas Scan](screenshots/02-network-scanning/Screenshot%202024-10-29%20021808.png)

The Xmas scan used FIN, PSH, and URG TCP flags, with port 80 reported as open|filtered.

#### ACK Scan (-sA)

![ACK Scan](screenshots/02-network-scanning/Screenshot%202024-10-29%20022158.png)

The ACK scan reported the tested ports as unfiltered, providing a baseline for later comparison with firewall filtering.

## Packet Analysis with Wireshark

Wireshark was used on the target system to capture and inspect traffic generated during the network scans.

The analysis included:

- TCP SYN packets
- SYN/ACK responses
- RST and RST/ACK packets
- TCP connection behavior
- Traffic on specific ports
- Differences in packet responses under different firewall conditions

Example Wireshark display filters used during the analysis:

```text
tcp.port == 20
tcp.port == 80
```

### Packet Analysis Results

The following Wireshark captures were used to inspect packet-level behavior generated during the network scans.

#### TCP Port Analysis

![TCP Port Analysis](screenshots/03-packet-analysis/Screenshot%202024-10-29%20023749(1)(1).png)

This capture shows TCP traffic involving port 20, including SYN probes and RST/ACK responses between the scanner and target.

#### TCP Response Analysis

![TCP Response Analysis](screenshots/03-packet-analysis/Screenshot%202024-10-29%20015204(3).png)

This capture provides additional visibility into TCP responses observed during the scanning process, including RST/ACK behavior.

#### UDP and ICMP Analysis

![UDP and ICMP Analysis](screenshots/03-packet-analysis/Screenshot%202024-10-29%20022623(2).png)

This capture shows UDP scan traffic together with ICMP Destination Unreachable responses, illustrating packet-level behavior associated with UDP port scanning.

## Firewall Testing

UFW was used to study how firewall rules affect network scanning and packet communication.

The testing process included:

1. Performing network scans with the firewall disabled.
2. Capturing the generated traffic using Wireshark.
3. Enabling UFW firewall protection.
4. Allowing HTTP traffic on TCP port 80.
5. Repeating the network scans.
6. Comparing scan results and packet behavior before and after firewall activation.

### Firewall Testing Results

The following screenshots document the firewall configuration and its impact on network scanning behavior.

#### UFW Configuration

![UFW Configuration](screenshots/04-firewall-testing/Screenshot%202024-10-29%20025047.png)

UFW was enabled on the target system and TCP port 80 was explicitly allowed to maintain access to the Apache web service.

#### Active Firewall Rules

![UFW Active Rules](screenshots/04-firewall-testing/Screenshot%202024-10-29%20025229.png)

The firewall status confirms that UFW is active and HTTP traffic on TCP port 80 is allowed.

#### Scan Behavior After Firewall Activation

![Nmap After Firewall](screenshots/04-firewall-testing/Screenshot%202024-10-29%20141056.png)

After firewall activation, the TCP Connect scan identified port 80 as open while 999 TCP ports were reported as filtered due to no response. This demonstrates the effect of firewall filtering on network reconnaissance.

## Key Observations

The project demonstrated how different scanning techniques generate different packet patterns and responses.

By comparing Nmap results with Wireshark captures, it was possible to observe how port states and firewall filtering are reflected directly in network traffic.

Firewall activation changed how the target responded to network probes, demonstrating the relationship between firewall policies, packet responses, and filtered port behavior.

## Key Takeaways

This project strengthened my practical understanding of:

- TCP/IP communication
- Network scanning and reconnaissance
- TCP flags and connection establishment
- Packet capture and traffic analysis
- Port states and service behavior
- Host-based firewall configuration
- Network security testing

It also helped connect these practical observations with networking concepts reinforced through my CCNA certification.

## Project Documentation

Additional project documentation and evidence are available in the repository:

- [Commands & Filters](commands.md)
- [Environment Setup](screenshots/01-environment-setup/)
- [Network Scanning](screenshots/02-network-scanning/)
- [Packet Analysis](screenshots/03-packet-analysis/)
- [Firewall Testing](screenshots/04-firewall-testing/)

> All network scanning and traffic analysis were performed in a controlled virtual environment for learning and testing purposes.




