# Wireshark Display Filters Cheat Sheet
## From Beginner to Advanced
### Complete Reference for Network Analysis, SOC, Malware Analysis, DFIR & Penetration Testing

---

# Table of Contents

1. Basics
2. Display Filter Syntax
3. Basic Packet Filters
4. IP Address Filters
5. MAC Address Filters
6. TCP Filters
7. UDP Filters
8. ICMP Filters
9. DNS Filters
10. HTTP Filters
11. HTTPS / TLS Filters
12. ARP Filters
13. DHCP Filters
14. FTP Filters
15. SSH Filters
16. SMB Filters
17. Email Filters
18. VoIP Filters
19. Packet Flag Filters
20. TCP Handshake Filters
21. TCP Retransmission Filters
22. Port Filters
23. Packet Size Filters
24. Time Filters
25. Error Filters
26. Malware Hunting Filters
27. SOC Investigation Filters
28. Incident Response Filters
29. Threat Hunting Filters
30. Performance Filters
31. Advanced Filters
32. Filter Operators
33. Useful Statistics
34. Display vs Capture Filters
35. Capture Filter Examples
36. Real-world Investigation Examples

---

# 1. Basics

Wireshark has two types of filters.

## Display Filter

Filters packets after capture.

Example

```wireshark
tcp
```

---

## Capture Filter

Filters packets before capture.

Example

```bash
tcp port 80
```

---

# 2. Display Filter Syntax

## Equal

```wireshark
ip.addr == 192.168.1.1
```

---

## Not Equal

```wireshark
ip.addr != 192.168.1.1
```

---

## Greater Than

```wireshark
frame.len > 100
```

---

## Less Than

```wireshark
frame.len < 500
```

---

## Greater or Equal

```wireshark
tcp.port >= 1024
```

---

## Less or Equal

```wireshark
tcp.port <= 1024
```

---

# 3. Basic Packet Filters

## Show TCP

```wireshark
tcp
```

---

## Show UDP

```wireshark
udp
```

---

## Show ICMP

```wireshark
icmp
```

---

## Show DNS

```wireshark
dns
```

---

## Show HTTP

```wireshark
http
```

---

## Show HTTPS

```wireshark
tls
```

---

## Show ARP

```wireshark
arp
```

---

# 4. IP Address Filters

## Specific IP

```wireshark
ip.addr == 192.168.1.10
```

---

## Source IP

```wireshark
ip.src == 192.168.1.10
```

---

## Destination IP

```wireshark
ip.dst == 192.168.1.20
```

---

## Communication Between Two Hosts

```wireshark
ip.src == 192.168.1.10 && ip.dst == 192.168.1.20
```

---

## Either Direction

```wireshark
ip.addr == 192.168.1.10 && ip.addr == 192.168.1.20
```

---

## Exclude Host

```wireshark
ip.addr != 192.168.1.10
```

---

# 5. MAC Address Filters

## Source MAC

```wireshark
eth.src == aa:bb:cc:dd:ee:ff
```

---

## Destination MAC

```wireshark
eth.dst == aa:bb:cc:dd:ee:ff
```

---

## MAC Address

```wireshark
eth.addr == aa:bb:cc:dd:ee:ff
```

---

# 6. TCP Filters

## All TCP

```wireshark
tcp
```

---

## TCP Port

```wireshark
tcp.port == 80
```

---

## Source Port

```wireshark
tcp.srcport == 443
```

---

## Destination Port

```wireshark
tcp.dstport == 80
```

---

## TCP Stream

```wireshark
tcp.stream == 0
```

---

## TCP Window Size

```wireshark
tcp.window_size > 0
```

---

## TCP Sequence Number

```wireshark
tcp.seq == 0
```

---

# 7. UDP Filters

## UDP Port

```wireshark
udp.port == 53
```

---

## Source Port

```wireshark
udp.srcport == 53
```

---

## Destination Port

```wireshark
udp.dstport == 53
```

---

# 8. ICMP Filters

## Echo Request

```wireshark
icmp.type == 8
```

---

## Echo Reply

```wireshark
icmp.type == 0
```

---

## Destination Unreachable

```wireshark
icmp.type == 3
```

---

## TTL Expired

```wireshark
icmp.type == 11
```

---

# 9. DNS Filters

## DNS Queries

```wireshark
dns.flags.response == 0
```

---

## DNS Responses

```wireshark
dns.flags.response == 1
```

---

## Specific Domain

```wireshark
dns.qry.name contains "google"
```

---

## NXDOMAIN

```wireshark
dns.flags.rcode == 3
```

---

# 10. HTTP Filters

## GET Requests

```wireshark
http.request.method == "GET"
```

---

## POST Requests

```wireshark
http.request.method == "POST"
```

---

## User Agent

```wireshark
http.user_agent
```

---

## Host

```wireshark
http.host
```

---

## URI

```wireshark
http.request.uri
```

---

## Response Code

```wireshark
http.response.code == 200
```

---

## 404

```wireshark
http.response.code == 404
```

---

# 11. HTTPS / TLS

## TLS

```wireshark
tls
```

---

## TLS Handshake

```wireshark
tls.handshake
```

---

## Client Hello

```wireshark
tls.handshake.type == 1
```

---

## Server Hello

```wireshark
tls.handshake.type == 2
```

---

## Certificate

```wireshark
tls.handshake.certificate
```

---

# 12. ARP

```wireshark
arp
```

---

## ARP Request

```wireshark
arp.opcode == 1
```

---

## ARP Reply

```wireshark
arp.opcode == 2
```

---

# 13. DHCP

```wireshark
bootp
```

---

## Discover

```wireshark
bootp.option.dhcp == 1
```

---

## Offer

```wireshark
bootp.option.dhcp == 2
```

---

## Request

```wireshark
bootp.option.dhcp == 3
```

---

## ACK

```wireshark
bootp.option.dhcp == 5
```

---

# 14. FTP

```wireshark
ftp
```

---

## FTP Data

```wireshark
ftp-data
```

---

# 15. SSH

```wireshark
ssh
```

---

# 16. SMB

```wireshark
smb
```

---

## SMB2

```wireshark
smb2
```

---

# 17. Email

SMTP

```wireshark
smtp
```

POP3

```wireshark
pop
```

IMAP

```wireshark
imap
```

---

# 18. VoIP

SIP

```wireshark
sip
```

RTP

```wireshark
rtp
```

---

# 19. TCP Flags

## SYN

```wireshark
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

---

## SYN ACK

```wireshark
tcp.flags.syn == 1 && tcp.flags.ack == 1
```

---

## ACK

```wireshark
tcp.flags.ack == 1
```

---

## FIN

```wireshark
tcp.flags.fin == 1
```

---

## RST

```wireshark
tcp.flags.reset == 1
```

---

## PSH

```wireshark
tcp.flags.push == 1
```

---

## URG

```wireshark
tcp.flags.urg == 1
```

---

# 20. TCP Handshake

First SYN

```wireshark
tcp.flags.syn==1 && tcp.flags.ack==0
```

Second Packet

```wireshark
tcp.flags.syn==1 && tcp.flags.ack==1
```

Third Packet

```wireshark
tcp.flags.ack==1 && tcp.len==0
```

---

# 21. TCP Problems

Retransmissions

```wireshark
tcp.analysis.retransmission
```

---

Fast Retransmission

```wireshark
tcp.analysis.fast_retransmission
```

---

Lost Segment

```wireshark
tcp.analysis.lost_segment
```

---

Duplicate ACK

```wireshark
tcp.analysis.duplicate_ack
```

---

Out of Order

```wireshark
tcp.analysis.out_of_order
```

---

Zero Window

```wireshark
tcp.analysis.zero_window
```

---

Window Full

```wireshark
tcp.analysis.window_full
```

---

Keep Alive

```wireshark
tcp.analysis.keep_alive
```

---

# 22. Port Filters

Port 80

```wireshark
tcp.port==80
```

Port 443

```wireshark
tcp.port==443
```

Port 22

```wireshark
tcp.port==22
```

Port 53

```wireshark
udp.port==53
```

Port 1514 (Wazuh)

```wireshark
tcp.port==1514
```

---

# 23. Packet Size

Greater than 1000 Bytes

```wireshark
frame.len>1000
```

Less than 64 Bytes

```wireshark
frame.len<64
```

---

# 24. Time

Packets after 10 Seconds

```wireshark
frame.time_relative>10
```

---

# 25. Error Filters

Checksum Errors

```wireshark
tcp.checksum_bad
```

Malformed

```wireshark
_malformed
```

---

# 26. Malware Hunting

Suspicious DNS

```wireshark
dns.flags.response==0
```

Large DNS

```wireshark
dns && frame.len>512
```

Beaconing

```wireshark
tcp.time_delta>60
```

Repeated Connections

```wireshark
tcp.analysis.retransmission
```

---

# 27. SOC Investigation

Failed Connections

```wireshark
tcp.flags.syn==1 && tcp.flags.ack==0
```

Internal Traffic

```wireshark
ip.src==10.0.0.0/8
```

RDP

```wireshark
tcp.port==3389
```

SSH

```wireshark
tcp.port==22
```

SMB

```wireshark
tcp.port==445
```

Wazuh

```wireshark
tcp.port==1514
```

---

# 28. Threat Hunting

Multiple SYN

```wireshark
tcp.flags.syn==1 && tcp.flags.ack==0
```

Possible Scan

```wireshark
tcp.flags.syn==1 && tcp.analysis.retransmission
```

DNS Tunneling

```wireshark
dns.qry.name.len>50
```

Large Uploads

```wireshark
tcp.len>1000
```

---

# 29. Performance

High Latency

```wireshark
tcp.analysis.ack_rtt
```

Window Issues

```wireshark
tcp.analysis.window_full
```

---

# 30. Advanced Filters

HTTP from One Host

```wireshark
http && ip.addr==192.168.1.10
```

---

TCP Between Two Hosts

```wireshark
tcp && ip.src==10.0.3.15 && ip.dst==192.168.1.16
```

---

Exclude DNS

```wireshark
!(dns)
```

---

HTTP OR HTTPS

```wireshark
http || tls
```

---

TCP NOT HTTP

```wireshark
tcp && !http
```

---

HTTP POST from One Host

```wireshark
http.request.method=="POST" && ip.src==192.168.1.5
```

---

# 31. Operators

AND

```wireshark
&&
```

OR

```wireshark
||
```

NOT

```wireshark
!
```

Equal

```wireshark
==
```

Not Equal

```wireshark
!=
```

Contains

```wireshark
contains
```

Matches Regex

```wireshark
matches
```

---

# 32. Display vs Capture Filters

| Display Filter | Capture Filter |
|---------------|---------------|
| tcp | tcp |
| udp | udp |
| ip.addr==192.168.1.1 | host 192.168.1.1 |
| tcp.port==80 | port 80 |
| tcp.port==443 | port 443 |
| arp | arp |
| icmp | icmp |
| dns | port 53 |
| http | tcp port 80 |
| tls | tcp port 443 |

---

# 33. Common Capture Filters

Capture HTTP

```bash
tcp port 80
```

Capture HTTPS

```bash
tcp port 443
```

Capture DNS

```bash
udp port 53
```

Capture SSH

```bash
tcp port 22
```

Capture ICMP

```bash
icmp
```

Capture Host

```bash
host 192.168.1.10
```

Capture Network

```bash
net 192.168.1.0/24
```

Capture TCP Only

```bash
tcp
```

Capture UDP Only

```bash
udp
```

---

# 34. Real-World Examples

## Find Failed TCP Connections

```wireshark
tcp.flags.syn==1 && tcp.flags.ack==0
```

---

## Investigate Wazuh Communication

```wireshark
tcp.port==1514
```

---

## Find SQL Injection

```wireshark
http.request.uri contains "union"
```

---

## Find Login Attempts

```wireshark
http.request.method=="POST"
```

---

## Detect Port Scan

```wireshark
tcp.flags.syn==1 && tcp.analysis.retransmission
```

---

## Detect Ping Sweep

```wireshark
icmp.type==8
```

---

## Detect DNS Tunneling

```wireshark
dns.qry.name.len>50
```

---

## Detect HTTP Downloads

```wireshark
http.content_length>100000
```

---

## Detect Large File Transfer

```wireshark
tcp.len>1400
```

---

# Pro Tips

- Use **Follow → TCP Stream** to reconstruct conversations.
- Colorize retransmissions for faster analysis.
- Apply **Statistics → Conversations** to identify top talkers.
- Use **Statistics → Endpoints** to map hosts.
- Use **Statistics → Protocol Hierarchy** to view protocol distribution.
- Use **Expert Information** to quickly identify anomalies.
- Combine filters with `&&`, `||`, and `!` for precise searches.
- Save frequently used filters as filter buttons for one-click access.
- Validate suspicious traffic with multiple indicators before drawing conclusions.

---
**Recommended Learning Order:** Ethernet → ARP → IP → ICMP → TCP/UDP → DNS → HTTP/HTTPS → TLS → TCP Analysis → Protocol Hierarchy → Conversations → Expert Information → Malware Traffic Analysis → SOC Investigations → Threat Hunting.