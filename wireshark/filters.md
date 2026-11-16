# Wireshark — Network Traffic Analysis

## 1. What is Wireshark?

Wireshark is a network protocol analyzer used to capture and inspect network traffic.

It helps security analysts understand communication between devices and investigate network problems.

Main features:
- Capture network packets
- Analyze network protocols
- Inspect TCP and UDP traffic
- Identify connection problems
- Investigate suspicious network activity

## 2. Display Filters

Display filters help analysts find specific packets in a capture.

### IP Address Filters

Find packets from or to a specific IP:

```wireshark
ip.addr == 192.168.1.10
```

Find packets sent by a specific IP:

```wireshark
ip.src == 192.168.1.10
```

Find packets sent to a specific IP:

```wireshark
ip.dst == 192.168.1.10
```

### TCP Filters

Show all TCP traffic:

```wireshark
tcp
```

Show traffic using TCP port 80:

```wireshark
tcp.port == 80
```

Show traffic using TCP port 443:

```wireshark
tcp.port == 443
```

### TCP Handshake Filters

Find SYN packets:

```wireshark
tcp.flags.syn == 1
```

Find initial SYN packets:

```wireshark
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

Find SYN-ACK packets:

```wireshark
tcp.flags.syn == 1 && tcp.flags.ack == 1
```

Find TCP reset packets:

```wireshark
tcp.flags.reset == 1
```

Find TCP FIN packets:

```wireshark
tcp.flags.fin == 1
```

### TCP Retransmissions

Find TCP retransmissions:

```wireshark
tcp.analysis.retransmission
```

Retransmissions can indicate packet loss, congestion or other network problems.

## 3. TCP Stream Analysis

Wireshark assigns a stream index to each TCP conversation.

Example filter:

```wireshark
tcp.stream == 2
```

This displays packets belonging to TCP stream number 2.

To follow a TCP conversation:
1. Select a TCP packet.
2. Right-click the packet.
3. Select Follow → TCP Stream.
4. Inspect the communication between the client and server.

## 4. Important Wireshark Columns

| Column | Description |
|---|---|
| No. | Packet number |
| Time | Packet capture timestamp |
| Source | Source IP address |
| Destination | Destination IP address |
| Protocol | Network protocol |
| Length | Packet size in bytes |
| Info | Packet details and TCP flags |

## 5. Practical TCP Handshake Analysis

A normal TCP connection uses three steps:

1. SYN — client requests a connection.
2. SYN-ACK — server acknowledges the request.
3. ACK — client confirms the server response.

Example from my Wireshark capture:

| Packet | Source | Destination | TCP Flag |
|---|---|---|---|
| 77 | 192.168.3.29 | 8.6.112.0 | SYN |
| 78 | 8.6.112.0 | 192.168.3.29 | SYN-ACK |
| 79 | 192.168.3.29 | 8.6.112.0 | ACK |

Connection details:
- Client IP: 192.168.3.29
- Server IP: 8.6.112.0
- Client port: 55298
- Server port: 80

Result: The TCP three-way handshake was completed.

## 6. Wireshark in SOC Investigation

SOC analysts use Wireshark to investigate suspicious network activity.

Examples:

### SYN Flood Investigation
Possible indicators:
- High volume of SYN packets
- Many incomplete TCP handshakes
- Repeated connection attempts
- Multiple source IP addresses targeting one server

### Network Troubleshooting
Possible indicators:
- TCP retransmissions
- Repeated connection attempts
- TCP resets (RST)
- Missing expected responses

Important: These indicators do not automatically prove an attack. Additional investigation is required.

## 7. Key Takeaways

- Wireshark captures and analyzes network traffic.
- Display filters help find specific packets.
- TCP flags show connection states and control information.
- TCP streams help inspect individual conversations.
- Retransmissions can indicate network problems.
- Packet analysis is an important SOC investigation skill.
