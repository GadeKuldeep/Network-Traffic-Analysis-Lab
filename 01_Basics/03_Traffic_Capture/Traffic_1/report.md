# Wireshark Network Analysis: Wazuh Agent-Manager Communication Failure

## Executive Summary
Captured 3,019 packets revealing failed TCP handshakes between Wazuh agent (10.0.3.15:58081) and manager (192.168.1.16:1514). Analysis identified 44 unanswered SYN packets due to offline Wazuh server, demonstrating application-layer dependency on manager availability.

---

## Capture Overview

| Metric | Value |
|--------|-------|
| **Total Packets** | 3,019 |
| **TCP Packets** | 979 |
| **UDP Packets** | 2,017 |
| **ICMP Packets** | 14 |
| **TLS/TLSv1** | 356 |
| **SYN-only (no response)** | 44 |
| **Capture Filter** | `tcp and (ip.src==10.0.3.15 and ip.dst==192.168.1.16)` |

---

## Key Findings

### 1. **Wazuh Agent-Manager Communication Identification**
- **Agent IP:Port** → `10.0.3.15:58081`
- **Manager IP:Port** → `192.168.1.16:1514`
- **Protocol** → TCP (port 1514 is Wazuh's default agent-manager communication port)
- **Checksum Status** → Header checksum validation disabled (0xda50)

### 2. **Failed TCP Three-Way Handshake**
**Observed Behavior:**
```
[SYN] Agent → Manager (Seq=0, Win=64240)
[TCP Retransmission] Agent → Manager (multiple attempts)
[NO SYN-ACK RESPONSE]
```

**Evidence:**
- Stream packet count: 3 (SYN, SYN, SYN)
- Conversation completeness: Incomplete (37%)
- Flags present: RST, FIN absent
- Flags absent: SYN-ACK, ACK

### 3. **Root Cause: Offline Wazuh Manager**
The Wazuh manager (192.168.1.16) was **offline/unreachable**, preventing:
- SYN-ACK responses
- Proper TCP three-way handshake completion
- Agent registration and log forwarding

### 4. **TCP Retransmission Analysis**
- **Seq=0, Win=64240** (initial SYN)
- **Multiple retransmissions** detected at different timestamps
- **MSS=1460** (standard TCP maximum segment size)
- **No congestion control flags** (ECN not capable)

---

## Technical Details

### Packet Breakdown (Filtered Results)

**TCP Transmission Control Protocol Summary:**
- Source Port: 58081 (Wazuh agent ephemeral port)
- Destination Port: 1514 (Wazuh manager listening port)
- Header Length: 20 bytes (5 dwords)
- Flags: 0x2 (SYN)
- Window Size: 64240 bytes
- Identification: 0x9a13

**Stream Characteristics:**
- Stream Index: 0
- Packet Number: 3 total in failed stream
- Conversation Status: Incomplete (**37% completion rate**)
- Unidirectional communication (agent → manager only)

### Network Path Analysis
```
10.0.3.15 (Kali VM)
    ↓ [58081 → 1514]
192.168.1.16 (Offline Wazuh Manager)
    ↑ [NO RESPONSE]
```

---

## Forensic Indicators

| Indicator | Status | Interpretation |
|-----------|--------|-----------------|
| **TCP SYN Response** | ❌ Absent | Service unreachable |
| **ICMP Unreachable** | ❌ Absent | No active rejection |
| **TCP RST** | ❌ Absent | Graceful non-response |
| **Retransmissions** | ✅ Present | OS-level retry logic active |
| **Port 1514 Open** | ❌ No evidence | Manager offline or firewalled |

---

## Methodology

### Passive Analysis Approach
1. **Packet Capture** → tcpdump/Wireshark on Kali VM
2. **Filter Application** → Isolated agent-to-manager traffic
3. **Port Identification** → Correlated with Wazuh default ports
4. **Flag Analysis** → Examined TCP control flags and sequence numbers
5. **Timeline Reconstruction** → Mapped retransmission intervals

### Tools Used
- **Wireshark 3.x** (packet inspection & visualization)
- **Display Filter:** `tcp and (ip.src==10.0.3.15 and ip.dst==192.168.1.16)`
- **Manual Protocol Analysis** (TCP RFC 793)

---

## Impact Assessment

### Agent Perspective
- **Status:** Unable to register with manager
- **Consequence:** No log forwarding, security monitoring disabled
- **Recovery:** Requires manager restart on 192.168.1.16:1514

### Network Behavior
- **Bandwidth Impact:** Minimal (SYN retransmissions only)
- **OS Behavior:** Standard TCP backoff retry mechanism
- **Security Posture:** Monitoring capability degraded

---

## Resolution Steps

### Immediate (Operational Recovery)
```bash
# 1. On Wazuh Manager VM (192.168.1.16)
sudo systemctl start wazuh-manager

# 2. Verify listening on port 1514
sudo netstat -tulpn | grep 1514

# 3. On Kali Agent VM (10.0.3.15)
sudo systemctl restart wazuh-agent
```

### Verification
- **Expected:** TCP handshake completion (SYN → SYN-ACK → ACK)
- **Indicator:** Packets flowing bidirectionally on port 1514
- **Confirmation:** Wazuh manager dashboard shows agent status as "Active"

---

## Lab Insights & Lessons Learned

### 1. **Port Knowledge is Critical**
Identifying that port 1514 belonged to Wazuh (vs. random service) was key to diagnosis. Maintained port database accelerates incident triage.

### 2. **Incomplete Conversations Signal Application Issues**
A 37% stream completeness rate immediately suggests service-layer problems, not network problems.

### 3. **Absence of Rejection ≠ Absence of Problem**
No ICMP unreachable or TCP RST means the host likely isn't reachable at all (power off, firewall rules, process not running).

### 4. **Retransmissions Show Resilience & Persistence**
The OS-level retry logic confirms the agent is healthy; it's the manager that's the failure point.

### 5. **Passive Analysis Sufficiency**
Full TCP handshake analysis is possible from one-way packet captures—no active probing needed for diagnosis.

---

## MITRE ATT&CK Alignment

| Technique | ID | Applicability |
|-----------|----|----|
| **Lateral Movement - Internal Network Traffic Analysis** | T1040 | ✅ Applicable |
| **Discovery - Network Service Discovery** | T1046 | ✅ Port 1514 identified |
| **Defense Evasion - Disable or Modify Tools** | T1562 | ⚠️ Wazuh manager unavailable (unintentional) |

---

## Artifact Preservation

**Capture File Details:**
- Protocol Stack: IPv4 → TCP → Application (Wazuh)
- Packet Count: 3,019 total (979 TCP-only)
- Malformed Packets: 0
- Expert Info Severity: Note (retransmission flagged as suspected)

---

## Conclusion

This capture demonstrates real-world Wazuh deployment challenges and the diagnostic power of Wireshark for application-layer troubleshooting. The 44 SYN-only packets serve as a clear indicator of manager unavailability, guiding administrators toward root-cause resolution without false positives or network-layer confusion.

**Status:** Analyzed ✅ | **Severity:** Medium (security monitoring gap) | **Resolution:** Bring manager online

---

## References

- **Wazuh Official:** https://documentation.wazuh.com
- **TCP RFC:** RFC 793 - Transmission Control Protocol
- **Wireshark Filters:** https://wiki.wireshark.org/DisplayFilters
- **Lab Setup:** Red-Blue-Team-Lab-Setup (GitHub)

---

*Report Generated: Wazuh Lab Investigation*  
*Analyzer: Kuldeep Gade | Contact: gadekuldeep25@gmail.com*