# Task 2: Network Security & Scanning

## Project Overview
This project demonstrates basic network reconnaissance, port scanning, service identification, packet capture, and firewall testing in an isolated cybersecurity lab.

## Objectives
- Discover a target host on a lab network.
- Identify open ports and running services.
- Detect service versions and estimate the target operating system.
- Capture and inspect network traffic using Wireshark.
- Attempt a firewall rule test.
- Document findings and security recommendations.

## Lab Environment
- **Attacker machine:** Kali Linux
- **Target machine:** Metasploitable 2
- **Target IP:** `192.168.56.101`
- **Tools:** Nmap, Wireshark, iptables

> All scanning and testing described here was performed in an isolated, authorized lab environment.

## Tools and Commands

### 1. Host Discovery
```bash
nmap -sn 192.168.56.101
```

### 2. TCP SYN Scan
```bash
sudo nmap -sS -T3 192.168.56.101 -oN ~/task2-network-security/reports/tcp-scan.txt
```

### 3. UDP Scan
```bash
sudo nmap -sU --top-ports 20 -T3 192.168.56.101 -oN ~/task2-network-security/reports/udp-scan.txt
```

### 4. Service and Version Detection
```bash
nmap -sV 192.168.56.101
```

### 5. Operating System Detection
```bash
sudo nmap -O -T3 192.168.56.101 -oN ~/task2-network-security/reports/os-detection.txt
```

### 6. Combined Scan
```bash
sudo nmap -sS -sV -O -T3 192.168.56.101 -oA ~/task2-network-security/reports/full-scan
```

## Key Findings
The combined Nmap scan identified **23 open TCP ports** on the target among the ports scanned.

Detected services included:
- FTP and SSH
- Telnet
- SMTP and DNS
- HTTP and Apache Tomcat
- SMB and RPC
- MySQL and PostgreSQL
- NFS, VNC, and IRC
- Legacy remote shell services

Nmap suggested that the target was running a Linux 2.6.x kernel.

These results indicate that the target exposes multiple services that should be reviewed. Service detection alone does not prove that every service is exploitable.

## Wireshark Packet Analysis
Wireshark was used to capture traffic between Kali Linux and Metasploitable 2.

- ICMP traffic was observed while pinging the target.
- The capture was saved as `capture.pcapng`.
- HTTP, FTP, and DNS traffic analysis was not confirmed as completed.

## Firewall Testing
A temporary `iptables` rule was attempted to block TCP port 80 on the target. The test result was not verified, so successful blocking is not claimed.

## Vulnerability Scanning Status
Greenbone/OpenVAS setup was attempted, but a completed vulnerability scan report was not obtained. Therefore, this repository does not claim verified vulnerability severity counts or a completed vulnerability assessment.

## Security Recommendations
1. Disable unnecessary network services.
2. Update outdated operating systems and applications.
3. Restrict database and file-sharing access to authorized hosts.
4. Replace insecure protocols such as Telnet with secure alternatives.
5. Use firewall rules to restrict exposed ports.
6. Run an authorized vulnerability scan and review its findings.
7. Save scan outputs and packet captures for future analysis.

## Repository Structure
```text
task2-network-security/
├── README.md
└── final-submission/
    ├── capture.pcapng
    ├── final-report.txt
    ├── full-scan.gnmap
    ├── full-scan.nmap
    ├── full-scan.xml
    ├── nmap-analysis.txt
    ├── os-detection.txt
    ├── tcp-scan.txt
    └── udp-scan.txt
```

## Conclusion
This lab provided practical experience with host discovery, TCP and UDP scanning, service identification, OS detection, packet capture, and an attempted firewall test. Further work is needed to complete vulnerability scanning and additional packet-analysis tasks.

## Disclaimer
This project is for educational purposes. Only scan or test systems for which you have explicit authorization.
