# Packets and How They Work

## What is a Packet?

A **packet** is the smallest unit of data sent over a network.

When you send a message, download a file, or open a website, the data is **broken into smaller packets**. Each packet travels independently through the network and is reassembled at the destination.

Example:

Original Message:
```
Hello World
```

Packets:
```
Packet 1 -> Hello
Packet 2 -> World
```

---

# How Packets Travel Over the Internet

```
Application
     |
Transport Layer (TCP/UDP)
     |
Internet Layer (IP)
     |
Data Link Layer (Ethernet/Wi-Fi)
     |
Physical Layer (Cable/Fiber/Wireless)
```

Example:

```
Your PC
   |
Home Router
   |
ISP
   |
Internet Routers
   |
Destination Server
```

Every router checks the destination IP address and forwards the packet to the next router until it reaches the destination.

---

# Packet Encapsulation

Each layer adds its own header.

```
+----------------------+
| Ethernet Header      |
+----------------------+
| IP Header            |
+----------------------+
| TCP/UDP Header       |
+----------------------+
| Data (Payload)       |
+----------------------+
```

At the destination, these headers are removed in reverse order.

---

# General Packet Structure

```
+-------------------------------+
| Header                        |
+-------------------------------+
| Payload (Actual Data)          |
+-------------------------------+
| Trailer (Optional)             |
+-------------------------------+
```

Header contains routing information.

Payload contains user data.

Trailer is mainly used by Ethernet for error detection.

---

# Ethernet Frame Structure

```
+---------+---------+----------+----------+--------+
|Dst MAC  |Src MAC  |Type      |Payload   |CRC     |
|6 Bytes  |6 Bytes  |2 Bytes   |46-1500 B |4 Bytes |
+---------+---------+----------+----------+--------+
```

Fields

- Destination MAC Address
- Source MAC Address
- EtherType
- Payload
- Frame Check Sequence (CRC)

---

# IPv4 Packet Header

Minimum Size: **20 Bytes**

```
0                   15                  31
+----+----+-----------------------------+
|Ver |IHL | Type of Service             |
+---------------------------------------+
| Total Length                          |
+---------------------------------------+
| Identification                        |
+---------------------------------------+
| Flags | Fragment Offset               |
+---------------------------------------+
| TTL   | Protocol | Header Checksum    |
+---------------------------------------+
| Source IP Address                     |
+---------------------------------------+
| Destination IP Address                |
+---------------------------------------+
| Options (Optional)                    |
+---------------------------------------+
```

## IPv4 Header Fields

| Field | Size |
|--------|------|
| Version | 4 bits |
| IHL | 4 bits |
| DSCP/ToS | 8 bits |
| Total Length | 16 bits |
| Identification | 16 bits |
| Flags | 3 bits |
| Fragment Offset | 13 bits |
| TTL | 8 bits |
| Protocol | 8 bits |
| Header Checksum | 16 bits |
| Source IP | 32 bits |
| Destination IP | 32 bits |
| Options | Variable |

Protocols

- TCP = 6
- UDP = 17
- ICMP = 1

---

# IPv6 Packet Header

Fixed Size: **40 Bytes**

```
+---------------------------------------+
| Version | Traffic Class | Flow Label  |
+---------------------------------------+
| Payload Length                        |
+---------------------------------------+
| Next Header | Hop Limit               |
+---------------------------------------+
| Source Address (128 bits)             |
+---------------------------------------+
| Destination Address (128 bits)        |
+---------------------------------------+
```

## IPv6 Header Fields

| Field | Size |
|--------|------|
| Version | 4 bits |
| Traffic Class | 8 bits |
| Flow Label | 20 bits |
| Payload Length | 16 bits |
| Next Header | 8 bits |
| Hop Limit | 8 bits |
| Source Address | 128 bits |
| Destination Address | 128 bits |

IPv6 does **not** contain

- Header Checksum
- Fragmentation Fields

These are handled differently compared to IPv4.

---

# TCP Packet Header

Minimum Size: **20 Bytes**

```
+-------------------------------+
| Source Port                   |
+-------------------------------+
| Destination Port              |
+-------------------------------+
| Sequence Number               |
+-------------------------------+
| Acknowledgement Number        |
+-------------------------------+
| Data Offset | Flags           |
+-------------------------------+
| Window Size                  |
+-------------------------------+
| Checksum                     |
+-------------------------------+
| Urgent Pointer               |
+-------------------------------+
| Options (Optional)           |
+-------------------------------+
```

## TCP Header Fields

| Field | Size |
|--------|------|
| Source Port | 16 bits |
| Destination Port | 16 bits |
| Sequence Number | 32 bits |
| Acknowledgement Number | 32 bits |
| Data Offset | 4 bits |
| Reserved | 3 bits |
| Flags | 9 bits |
| Window Size | 16 bits |
| Checksum | 16 bits |
| Urgent Pointer | 16 bits |
| Options | Variable |

Common TCP Flags

- SYN
- ACK
- FIN
- RST
- PSH
- URG

---

# UDP Header

Size: **8 Bytes**

```
+----------------------+
| Source Port          |
+----------------------+
| Destination Port     |
+----------------------+
| Length               |
+----------------------+
| Checksum             |
+----------------------+
```

Fields

| Field | Size |
|--------|------|
| Source Port |16 bits|
| Destination Port |16 bits|
| Length |16 bits|
| Checksum |16 bits|

UDP is faster because it has fewer header fields than TCP.

---

# ICMP Packet Header

```
+-------------------------+
| Type                    |
+-------------------------+
| Code                    |
+-------------------------+
| Checksum                |
+-------------------------+
| Rest of Header          |
+-------------------------+
| Data                    |
+-------------------------+
```

Used for

- Ping
- Network diagnostics
- Error reporting

---

# Packet Journey Example

```
User types:
www.google.com

↓

DNS resolves domain to IP

↓

TCP Handshake

↓

HTTP Request

↓

Request divided into packets

↓

Router 1

↓

Router 2

↓

Router 3

↓

Google Server

↓

Packets reassembled

↓

HTTP Response returned
```

---

# OSI Layer vs Packet

| OSI Layer | Protocol | Data Unit |
|------------|----------|-----------|
| Application | HTTP, FTP | Data |
| Transport | TCP, UDP | Segment / Datagram |
| Network | IP | Packet |
| Data Link | Ethernet | Frame |
| Physical | Cable/Wi-Fi | Bits |

---

# Packet Summary

| Protocol | Header Size | Purpose |
|-----------|-------------|---------|
| Ethernet | 14 Bytes | Local Network Communication |
| IPv4 | 20–60 Bytes | Routing |
| IPv6 | 40 Bytes | Routing |
| TCP | 20–60 Bytes | Reliable Communication |
| UDP | 8 Bytes | Fast Communication |
| ICMP | Variable | Diagnostics |

---

# Key Points

- A packet is a small unit of data transmitted over a network.
- Large files are divided into multiple packets before transmission.
- Each packet contains a header and a payload.
- Routers use the IP header to forward packets to the correct destination.
- IPv4 uses 32-bit addresses, while IPv6 uses 128-bit addresses.
- TCP provides reliable communication, whereas UDP prioritizes speed.
- Ethernet frames encapsulate IP packets for transmission over local networks.
```