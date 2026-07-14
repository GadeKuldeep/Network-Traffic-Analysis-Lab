# Types of Packet Transmission Methods

Packet transmission is the method by which packets travel from a sender to one or more receivers across a network. Depending on the destination and purpose, networks use different transmission methods.

---

# 1. Unicast

## Definition

**Unicast** is a one-to-one communication method where one sender transmits packets to one specific receiver.

This is the most common transmission method on the Internet.

### Example

- Opening a website
- Sending an email
- SSH connection
- FTP download
- HTTPS communication

### Diagram

```
           Unicast

+---------+
| Sender  |
+---------+
     |
     |
     V
+---------+
|Receiver |
+---------+
```

### Real Example

```
Laptop
192.168.1.10
      |
      |
      V
Web Server
142.250.183.78
```

The packet is delivered only to the destination IP.

---

## Packet Flow

```
Application
      |
TCP
      |
IP Header
      |
Ethernet Frame
      |
Router
      |
Destination
```

---

## Advantages

- Secure communication
- Reliable
- No unnecessary traffic
- Best for personal communication

## Disadvantages

- Multiple receivers require multiple copies
- Higher bandwidth usage

---

# 2. Broadcast

## Definition

Broadcast sends one packet to **every device** in the local network.

Every device receives the packet.

Only the intended device processes it.

Others simply discard it.

Broadcast does **not** cross routers.

---

### Example

ARP Request

```
Who has 192.168.1.20?
Tell 192.168.1.10
```

Every computer receives the request.

Only the owner replies.

---

### Diagram

```
                Broadcast

                +---------+
                | Sender  |
                +---------+
                     |
        -----------------------------
       |             |             |
       V             V             V
+---------+   +---------+   +---------+
|Device A |   |Device B |   |Device C |
+---------+   +---------+   +---------+
```

---

### Broadcast Address

IPv4

```
255.255.255.255
```

Example Network

```
Network:
192.168.1.0/24

Broadcast:
192.168.1.255
```

---

## Advantages

- Easy device discovery
- Fast network announcements
- Used by ARP and DHCP

## Disadvantages

- Consumes bandwidth
- Every device must process the packet
- Cannot cross routers

---

# 3. Multicast

## Definition

Multicast sends packets to a selected group of devices.

Only devices that joined the multicast group receive the packets.

---

### Example

- IPTV
- Video conferencing
- Live streaming
- Online classrooms
- Stock market feeds

---

### Diagram

```
                Multicast

                +---------+
                | Sender  |
                +---------+
                     |
        -----------------------------
       |             |             |
       V             X             V
+---------+     +---------+   +---------+
|Client A |     |Client B |   |Client C |
|(Joined) |     |Not Join |   |Joined   |
+---------+     +---------+   +---------+
```

Only A and C receive packets.

---

### Multicast IPv4 Range

```
224.0.0.0
     to
239.255.255.255
```

Example

```
239.1.1.1
```

---

## Advantages

- Saves bandwidth
- One transmission serves many receivers
- Efficient for streaming

## Disadvantages

- Complex routing
- Requires multicast-enabled routers
- Not supported everywhere

---

# 4. Anycast

## Definition

Anycast sends packets to the **nearest** or **best** server among multiple servers sharing the same IP address.

The network decides which server is closest.

---

### Example

- Google DNS
- Cloudflare DNS
- CDN (Content Delivery Networks)

---

### Diagram

```
                Anycast

               +---------+
               | Sender  |
               +---------+
                    |
        ----------------------------
       |            |             |
       V            V             V
+---------+   +---------+   +---------+
|Server A |   |Server B |   |Server C |
|Nearest  |   |Far Away |   |Far Away |
+---------+   +---------+   +---------+

Packet reaches Server A.
```

---

## Advantages

- Low latency
- High availability
- Automatic load balancing
- Fault tolerance

## Disadvantages

- Complex routing
- Difficult troubleshooting

---

# 5. Geocast

## Definition

Geocast delivers packets only to devices within a specific geographic region.

Mostly used in research, VANETs (Vehicle Ad Hoc Networks), and IoT.

---

### Example

Emergency alerts

```
Earthquake warning

Only devices inside Pune receive it.
```

---

### Diagram

```
            Internet

      ---------------------

      Mumbai      Pune      Delhi
         X          ✓         X

Only Pune receives packets.
```

---

## Advantages

- Saves bandwidth
- Location-specific delivery

## Disadvantages

- Rarely used on the public Internet
- Requires geographic routing

---

# Comparison

| Method | Communication | Internet Use | Example |
|---------|--------------|--------------|---------|
| Unicast | One → One | Yes | HTTP, HTTPS, SSH |
| Broadcast | One → All | Local Network Only | ARP, DHCP |
| Multicast | One → Many (Selected) | Limited | IPTV, Video Streaming |
| Anycast | One → Nearest | Yes | Google DNS, Cloudflare DNS |
| Geocast | One → Geographic Area | Limited | Emergency Alerts |

---

# OSI Layer Usage

```
+-----------------------------+
| Application                 |
+-----------------------------+
| TCP / UDP                   |
+-----------------------------+
| IPv4 / IPv6                 |
| Unicast                     |
| Broadcast                   |
| Multicast                   |
| Anycast                     |
+-----------------------------+
| Ethernet                    |
+-----------------------------+
| Physical Media              |
+-----------------------------+
```

---

# Real-World Examples

## Unicast

```
You
 |
 |
 V
youtube.com
```

Only your computer receives the video packets.

---

## Broadcast

```
Laptop

"Who owns 192.168.1.50?"

      |
----------------------------
|      |       |       |
PC1   PC2    PC3     PC4
```

Every device receives the ARP request.

---

## Multicast

```
Teacher

      |
--------------------------
|        |        |
Student1 Student2 Student3
```

Only students subscribed to the live class receive the stream.

---

## Anycast

```
User (India)
      |
      V
Nearest DNS Server (Mumbai)

Other DNS servers:

Singapore
London
New York

Ignored
```

---

## Geocast

```
Government Server

      |
      V

Only Maharashtra receives the emergency alert.

Other states ignore the transmission.
```

---

# Summary

| Method | Receivers | Bandwidth | Typical Use |
|---------|-----------|-----------|-------------|
| Unicast | 1 | Medium | Web browsing, Email |
| Broadcast | All | High | ARP, DHCP |
| Multicast | Group | Low | Live streaming, IPTV |
| Anycast | Nearest | Low | DNS, CDN |
| Geocast | Geographic Region | Low | Emergency alerts, IoT |

---

# Key Points

- **Unicast** is one-to-one communication and is the most common method used on the Internet.
- **Broadcast** sends packets to every device on the local network and is mainly used for discovery protocols such as ARP and DHCP.
- **Multicast** delivers packets only to devices that have joined a multicast group, making it efficient for streaming.
- **Anycast** routes packets to the closest available server, improving performance and availability for services like DNS and CDNs.
- **Geocast** targets devices within a specific geographic area and is primarily used in specialized applications such as emergency alert systems and IoT.