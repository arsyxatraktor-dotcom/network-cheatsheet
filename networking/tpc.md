
# TCP (Transmission Control Protocol)

## 1. What is TCP?

TCP is a connection-oriented transport layer protocol.
It provides reliable data transmission between devices.

Main features:
- Connection-oriented communication
- Reliable data delivery
- Packet sequencing
- Error detection
- Retransmission of lost segments
- Flow control

Default protocol: TCP
OSI layer: Layer 4 (Transport)

## 2. TCP Three-Way Handshake

TCP uses a three-step process to establish a connection.

### Step 1 — SYN
The client sends a SYN packet to the server.
It requests a new TCP connection.

### Step 2 — SYN-ACK
The server responds with SYN-ACK.
It acknowledges the client's request and sends its own SYN.

### Step 3 — ACK
The client sends ACK to the server.
The TCP connection is now established.

Sequence:

Client → Server: SYN
Server → Client: SYN-ACK
Client → Server: ACK

## 3. Important TCP Flags

| Flag | Meaning |
|---|---|
| SYN | Initiates a connection |
| ACK | Acknowledges received data |
| FIN | Gracefully terminates a connection |
| RST | Resets a connection immediately |
| PSH | Requests prompt delivery of data to the application |
| URG | Indicates urgent data |

## 4. TCP Connection Termination

TCP normally uses a four-step process to close a connection.

1. Client sends FIN.
2. Server responds with ACK.
3. Server sends FIN.
4. Client responds with ACK.

This is called the TCP Four-Way Handshake.

FIN = graceful connection termination.

RST = abrupt connection reset.

## 5. TCP SYN Flood Attack

A SYN flood is a type of Denial-of-Service (DoS) attack.

The attacker sends a large number of SYN packets to a target server.

The server responds with SYN-ACK, but the final ACK may never arrive.

This can cause:
- Many incomplete TCP connections
- Resource exhaustion
- Increased server load
- Service availability problems

### Possible Detection Indicators

- Unusually high SYN packet volume
- Many incomplete TCP handshakes
- Repeated SYN packets
- Large number of source IP addresses
- High number of half-open connections

### SOC Investigation

A SOC analyst should:
1. Identify the destination server.
2. Count incoming SYN packets.
3. Identify unique source IP addresses.
4. Check whether handshakes are completed.
5. Review firewall and server logs.
6. Check server resource usage.

Important: A high number of SYN packets does not automatically prove an attack. Legitimate traffic spikes and network problems must also be considered.

## 6. TCP in Wireshark

Useful display filters:

- Find SYN packets:
  tcp.flags.syn == 1

- Find initial SYN packets:
  tcp.flags.syn == 1 && tcp.flags.ack == 0

- Find SYN-ACK packets:
  tcp.flags.syn == 1 && tcp.flags.ack == 1

- Find TCP retransmissions:
  tcp.analysis.retransmission

- Find TCP resets:
  tcp.flags.reset == 1

## 7. Key Takeaways

- TCP is a reliable, connection-oriented protocol.
- TCP operates at OSI Layer 4.
- Three-Way Handshake establishes a connection.
- FIN is used for graceful termination.
- RST resets a connection.
- SYN flood targets TCP connection establishment.
- Wireshark helps analyze TCP traffic and detect suspicious behavior.
