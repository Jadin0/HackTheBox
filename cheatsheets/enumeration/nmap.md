---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Nmap

Syntax

```bash
nmap [scan type] [options] [target]
```

| Option             | Description                                                           |
| ------------------ | --------------------------------------------------------------------- |
| 0.0.0.0/24         | Subnet scan via CIDR notation                                         |
| -sn                | Disables port scanning                                                |
| -Pn                | Disables ICMP Echo Requests                                           |
| -PE                | Performs the ping scan by using ICMI Echo Requests against the target |
| --packet-trade     | Shows all packets sent and received                                   |
| --reason           | Displays the reason for a specific output/result                      |
| --disable-arp-ping | Disables ARP Ping requests                                            |
| --top-ports \[num] | Scans the specified number of most frequently used ports              |
| -p-                | Scans all ports                                                       |
| -p\[num]-\[num]    | Scans all ports within the range provided                             |
| -p\[num],\[num]    | Scans only specified ports                                            |
| -F                 | Scans top 100 ports                                                   |
| -sS                | Performs TCP Syn-Ack Scan                                             |
| -sA                | Performs TCP Ack Scan                                                 |
| -sU                | Scans UDP ports                                                       |
| -sV                | Service version scan                                                  |
| -sC                | Script scan with default category scripts.                            |
| -O                 | OS Detection Scan                                                     |
| -A                 | OS Detection, Service Detection and tracert scans.                    |

