# Network Protocol Cheat Sheet (OSI Model)

> A quick reference of common protocols from the **Physical Layer (Layer 1)** to the **Application Layer (Layer 7)**.

---

# Layer 1 - Physical Layer

| Protocol | Full Form | Use |
|----------|-----------|-----|
| Ethernet (PHY) | Ethernet Physical Layer | Physical transmission of electrical/optical signals. |
| RS-232 | Recommended Standard 232 | Serial communication between devices. |
| USB | Universal Serial Bus | Connects peripherals and transfers data/power. |
| DSL | Digital Subscriber Line | Internet over telephone lines. |
| SONET | Synchronous Optical Network | High-speed fiber optic communication. |
| ISDN | Integrated Services Digital Network | Digital voice and data communication. |
| Bluetooth (PHY) | Bluetooth Physical Layer | Wireless short-range communication. |
| IEEE 802.11 PHY | Wi-Fi Physical Layer | Wireless signal transmission. |

---

# Layer 2 - Data Link Layer

| Protocol | Full Form | Use |
|----------|-----------|-----|
| Ethernet | IEEE 802.3 | LAN communication using MAC addresses. |
| Wi-Fi | IEEE 802.11 | Wireless LAN communication. |
| PPP | Point-to-Point Protocol | Direct communication between two nodes. |
| HDLC | High-Level Data Link Control | WAN serial communication. |
| Frame Relay | Frame Relay | Packet-switched WAN technology. |
| ATM | Asynchronous Transfer Mode | High-speed voice, video, and data transfer. |
| ARP | Address Resolution Protocol | Resolves IPv4 addresses to MAC addresses. |
| RARP | Reverse Address Resolution Protocol | Resolves MAC to IP (obsolete). |
| VLAN | Virtual Local Area Network (802.1Q) | Network segmentation. |
| STP | Spanning Tree Protocol | Prevents Layer 2 loops. |
| LLDP | Link Layer Discovery Protocol | Discovers neighboring devices. |
| CDP | Cisco Discovery Protocol | Cisco device discovery. |

---

# Layer 3 - Network Layer

| Protocol | Full Form | Use |
|----------|-----------|-----|
| IPv4 | Internet Protocol Version 4 | Logical addressing and routing. |
| IPv6 | Internet Protocol Version 6 | Next-generation IP addressing. |
| ICMP | Internet Control Message Protocol | Error reporting and diagnostics (Ping). |
| IGMP | Internet Group Management Protocol | Multicast group management. |
| IPSec | Internet Protocol Security | Secure IP communication. |
| OSPF | Open Shortest Path First | Dynamic routing protocol. |
| RIP | Routing Information Protocol | Distance-vector routing. |
| EIGRP | Enhanced Interior Gateway Routing Protocol | Cisco routing protocol. |
| BGP | Border Gateway Protocol | Internet backbone routing. |
| GRE | Generic Routing Encapsulation | Creates VPN tunnels. |

---

# Layer 4 - Transport Layer

| Protocol | Full Form | Use |
|----------|-----------|-----|
| TCP | Transmission Control Protocol | Reliable, connection-oriented communication. |
| UDP | User Datagram Protocol | Fast, connectionless communication. |
| SCTP | Stream Control Transmission Protocol | Reliable transport with multi-streaming. |
| DCCP | Datagram Congestion Control Protocol | Congestion-controlled multimedia transport. |

---

# Layer 5 - Session Layer

| Protocol | Full Form | Use |
|----------|-----------|-----|
| NetBIOS | Network Basic Input/Output System | Session management on Windows networks. |
| RPC | Remote Procedure Call | Executes procedures on remote systems. |
| PPTP | Point-to-Point Tunneling Protocol | VPN session establishment. |
| SMB Session | Server Message Block Session | File sharing session management. |

---

# Layer 6 - Presentation Layer

| Protocol | Full Form | Use |
|----------|-----------|-----|
| SSL | Secure Sockets Layer | Encrypts communication (legacy). |
| TLS | Transport Layer Security | Secure encrypted communication. |
| MIME | Multipurpose Internet Mail Extensions | Defines email content formats. |
| ASCII | American Standard Code for Information Interchange | Character encoding. |
| Unicode | Unicode Standard | Universal character encoding. |
| JPEG | Joint Photographic Experts Group | Image compression format. |
| PNG | Portable Network Graphics | Lossless image format. |
| GIF | Graphics Interchange Format | Animated/static image format. |
| MPEG | Moving Picture Experts Group | Video compression standard. |

---

# Layer 7 - Application Layer

| Protocol | Full Form | Use |
|----------|-----------|-----|
| HTTP | HyperText Transfer Protocol | Web browsing. |
| HTTPS | HyperText Transfer Protocol Secure | Secure web browsing. |
| FTP | File Transfer Protocol | File transfer. |
| SFTP | SSH File Transfer Protocol | Secure file transfer. |
| TFTP | Trivial File Transfer Protocol | Simple file transfer. |
| SMTP | Simple Mail Transfer Protocol | Sending emails. |
| POP3 | Post Office Protocol Version 3 | Receiving emails. |
| IMAP | Internet Message Access Protocol | Email synchronization. |
| DNS | Domain Name System | Resolves domain names to IP addresses. |
| DHCP | Dynamic Host Configuration Protocol | Automatically assigns IP addresses. |
| SNMP | Simple Network Management Protocol | Network monitoring and management. |
| SSH | Secure Shell | Secure remote login. |
| Telnet | Telecommunication Network | Remote login (unencrypted). |
| LDAP | Lightweight Directory Access Protocol | Directory services. |
| NTP | Network Time Protocol | Time synchronization. |
| SIP | Session Initiation Protocol | VoIP call setup. |
| RTP | Real-time Transport Protocol | Audio/video streaming. |
| RTSP | Real Time Streaming Protocol | Controls media streaming. |
| SMB | Server Message Block | File and printer sharing. |
| NFS | Network File System | File sharing in Unix/Linux. |
| MQTT | Message Queuing Telemetry Transport | Lightweight IoT messaging. |
| AMQP | Advanced Message Queuing Protocol | Enterprise message queuing. |
| CoAP | Constrained Application Protocol | IoT communication. |
| WebSocket | WebSocket Protocol | Full-duplex web communication. |

---

# Quick Summary

| OSI Layer | Main Function | Common Protocols |
|-----------|---------------|------------------|
| Layer 7 | Application Services | HTTP, HTTPS, DNS, FTP, SSH, SMTP, DHCP |
| Layer 6 | Data Formatting & Encryption | TLS, SSL, MIME, JPEG, PNG |
| Layer 5 | Session Management | NetBIOS, RPC, PPTP |
| Layer 4 | End-to-End Communication | TCP, UDP, SCTP |
| Layer 3 | Routing & Logical Addressing | IPv4, IPv6, ICMP, OSPF, RIP, BGP |
| Layer 2 | MAC Addressing & Framing | Ethernet, Wi-Fi, ARP, VLAN, STP |
| Layer 1 | Signal Transmission | Ethernet PHY, USB, DSL, Bluetooth PHY |