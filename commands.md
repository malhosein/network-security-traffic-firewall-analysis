# Commands & Filters

This document contains the main network scanning options, firewall commands, and Wireshark display filters used throughout the project.

## Nmap / Zenmap Scanning

The following Nmap scan types were used to analyze different network and port behaviors.

### TCP SYN Scan

```bash
sudo nmap -sS <target-ip>
```

Performs a TCP SYN (half-open) scan without completing the full TCP three-way handshake.

### TCP Connect Scan

```bash
nmap -sT <target-ip>
```

Performs a full TCP connection using the operating system's connection mechanism.

### Xmas Scan

```bash
sudo nmap -sX <target-ip>
```

Sends TCP packets with the FIN, PSH, and URG flags set to analyze how the target responds.

### ACK Scan

```bash
sudo nmap -sA <target-ip>
```

Used to analyze firewall filtering behavior rather than directly determining whether a port is open.

### UDP Scan

```bash
sudo nmap -sU <target-ip>
```

Scans UDP ports and helps analyze services that do not use TCP connections.

---

## UFW Firewall

UFW was used on the target system to compare network behavior with and without firewall filtering.

### Disable the Firewall

```bash
sudo ufw disable
```

Used during the baseline testing phase before firewall filtering was applied.

### Enable the Firewall

```bash
sudo ufw enable
```

Activates UFW firewall protection.

### Allow HTTP Traffic

```bash
sudo ufw allow 80/tcp
```

Allows incoming TCP traffic to the Apache web service on port 80.

### Check Firewall Status

```bash
sudo ufw status
```

Displays the current UFW status and configured firewall rules.

---

## Wireshark Display Filters

Wireshark was used to inspect traffic generated during the network scans.

### TCP Port 20

```text
tcp.port == 20
```

Displays TCP packets where port 20 is either the source or destination port.

### TCP Port 80

```text
tcp.port == 80
```

Displays HTTP-related TCP traffic involving port 80.

---

## Testing Workflow

The general testing workflow used in the project was:

1. Prepare the scanner and target Kali Linux systems.
2. Disable UFW to establish baseline network behavior.
3. Run the different Nmap/Zenmap scans against the target.
4. Capture and inspect the generated traffic using Wireshark.
5. Enable UFW and configure the TCP port 80 rule.
6. Repeat the network scans.
7. Compare the scan results and packet behavior before and after firewall filtering.

> Replace `<target-ip>` with the IP address of the target system when reproducing the scans.


> 
