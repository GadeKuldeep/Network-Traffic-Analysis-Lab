# Types of Switching in Computer Networks

Switching is the process of forwarding data from a source device to a destination device through intermediate networking devices (switches or routers). It determines how data travels across a network.

There are **three main types of switching**:

1. Circuit Switching
2. Packet Switching
3. Message Switching

---

# 1. Circuit Switching

## Definition

**Circuit Switching** establishes a **dedicated communication path** between the sender and receiver before any data is transmitted.

The entire path remains reserved until the communication ends.

This method is mainly used in traditional telephone networks.

---

## How It Works

### Step 1: Connection Setup

A dedicated path is established.

```
Sender
   |
Switch A
   |
Switch B
   |
Switch C
   |
Receiver
```

---

### Step 2: Data Transmission

Once the connection is established, all data follows the same path.

```
Sender
   |
======== Dedicated Path ========
   |
Receiver
```

---

### Step 3: Connection Termination

After communication ends, the dedicated path is released.

```
Dedicated Circuit Removed

Sender

Receiver
```

---

## Example

Traditional Telephone Call

```
You
 |
 |
Telephone Exchange
 |
 |
Friend
```

The entire communication channel remains reserved for both users.

---

## Characteristics

- Dedicated communication path
- Fixed bandwidth
- Continuous transmission
- No packet loss due to congestion
- Connection-oriented

---

## Advantages

- Guaranteed bandwidth
- Low delay after connection establishment
- No packet reordering
- Reliable communication

---

## Disadvantages

- Expensive
- Poor bandwidth utilization
- Connection setup takes time
- Resources remain reserved even when no data is sent

---

# 2. Packet Switching

## Definition

Packet Switching divides data into **small packets**. Each packet is transmitted independently and may take different paths to reach the destination.

This is the switching technique used on the Internet.

---

## How It Works

Original Data

```
This is a network packet.
```

Divided into packets

```
Packet 1
Packet 2
Packet 3
Packet 4
```

---

### Transmission

Each packet may travel through a different route.

```
               Router A
             /
Sender ---- Router B ---- Receiver
             \
               Router C
```

Example

```
Packet 1 → Router A

Packet 2 → Router C

Packet 3 → Router B

Packet 4 → Router A
```

At the destination

```
Packet 1
Packet 2
Packet 3
Packet 4

↓

Original Data Reconstructed
```

---

## Types of Packet Switching

### A. Datagram Packet Switching

Each packet travels independently.

Every packet contains the complete destination address.

Example

```
Packet 1 → Path A

Packet 2 → Path C

Packet 3 → Path B
```

Used by

- Internet Protocol (IP)

---

### B. Virtual Circuit Packet Switching

A logical path is established before transmission.

All packets follow the same logical route.

```
Sender
 |
Router A
 |
Router B
 |
Receiver
```

Used by

- Frame Relay
- ATM
- MPLS (logical paths)

---

## Example

Opening a website

```
Laptop

↓

ISP

↓

Internet Routers

↓

Google Server
```

Thousands of packets travel independently.

---

## Characteristics

- No dedicated path
- Efficient bandwidth utilization
- Dynamic routing
- High scalability

---

## Advantages

- Efficient bandwidth usage
- Faster network utilization
- Supports many users simultaneously
- Fault tolerant

---

## Disadvantages

- Variable delay
- Packet loss possible
- Packet reordering possible
- Congestion can occur

---

# 3. Message Switching

## Definition

In Message Switching, the **entire message** is transmitted as a single unit.

Each intermediate switch stores the complete message before forwarding it.

This technique is also called **Store-and-Forward Switching**.

---

## How It Works

```
Sender

↓

Switch A

(Store Complete Message)

↓

Switch B

(Store Complete Message)

↓

Receiver
```

Each switch waits until the entire message arrives before forwarding it.

---

## Example

Email Transmission

```
Sender

↓

Mail Server

↓

Internet

↓

Receiver Mail Server

↓

Receiver
```

The email is stored at each mail server before being forwarded.

---

## Characteristics

- No dedicated path
- Entire message stored
- Store-and-forward operation
- Large storage requirement

---

## Advantages

- No connection setup
- Better bandwidth utilization
- Can prioritize messages
- Reliable delivery

---

## Disadvantages

- High delay
- Large storage requirement
- Not suitable for real-time communication

---

# Switching Comparison

| Feature | Circuit Switching | Packet Switching | Message Switching |
|----------|------------------|------------------|------------------|
| Connection Required | Yes | No (Datagram) / Logical (Virtual Circuit) | No |
| Dedicated Path | Yes | No | No |
| Data Unit | Continuous Stream | Packets | Complete Message |
| Storage at Intermediate Nodes | No | Packet Buffer | Entire Message |
| Delay | Low after setup | Variable | High |
| Bandwidth Utilization | Poor | Excellent | Good |
| Fault Tolerance | Low | High | Medium |
| Suitable for Real-Time | Yes | Yes | No |

---

# Visual Comparison

## Circuit Switching

```
Sender
   |
======== Dedicated Circuit ========
   |
Receiver
```

---

## Packet Switching

```
          Router A
        /
Sender
        \
          Router B
             \
              Router C

↓

Receiver
```

Packets may take different routes.

---

## Message Switching

```
Sender

↓

Switch A
(Store)

↓

Switch B
(Store)

↓

Receiver
```

Each switch stores the complete message before forwarding it.

---

# Real-World Examples

## Circuit Switching

```
Traditional Telephone Network

Caller

↓

Telephone Exchange

↓

Receiver
```

---

## Packet Switching

```
Web Browser

↓

ISP

↓

Internet

↓

Web Server
```

Used for

- HTTP
- HTTPS
- FTP
- SSH
- Video Streaming
- Online Gaming

---

## Message Switching

```
User

↓

Mail Server

↓

Internet

↓

Recipient Mail Server

↓

Recipient
```

Used for

- Email Systems
- SMS Store-and-Forward Systems
- Message Queues

---

# Which Switching Technique is Used Today?

| Technology | Switching Method |
|------------|------------------|
| Telephone (PSTN) | Circuit Switching |
| Internet | Packet Switching |
| Email | Message Switching |
| VoIP | Packet Switching |
| Video Streaming | Packet Switching |
| Cloud Computing | Packet Switching |

---

# Key Points

- **Circuit Switching** establishes a dedicated communication path before data transmission, making it reliable but less efficient in bandwidth usage.
- **Packet Switching** divides data into packets that are routed independently (or through a logical path), providing efficient bandwidth utilization and scalability. It is the foundation of the modern Internet.
- **Message Switching** forwards the entire message using a store-and-forward mechanism, making it suitable for non-real-time applications such as email.
- Modern computer networks primarily rely on **Packet Switching** because it offers better resource utilization, flexibility, and fault tolerance.