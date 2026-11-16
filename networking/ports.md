
# Ports and Network Protocols

## 1. What is a Network Port?

A network port is a logical identifier used by TCP and UDP to distinguish communication endpoints.

- IP address identifies a network interface.
- Port number identifies a communication endpoint.
- TCP and UDP have separate port spaces.
- Port numbers range from 0 to 65535.

Example:
192.168.3.29:55298 -> 8.6.112.0:80

Client IP: 192.168.3.29
Client port: 55298
Server IP: 8.6.112.0
Server port: 80 (HTTP)

## 2. Common Ports and Protocols

| Protocol | Port | Transport | Purpose |
|---|---|---|---|
| FTP | 21 | TCP | File transfer control |
| FTP data | 20* | TCP | Active-mode data |
| SSH | 22 | TCP | Secure remote access |
| SFTP | 22 | TCP | File transfer over SSH |
| Telnet | 23 | TCP | Unencrypted remote terminal |
| SMTP | 25 | TCP | Mail transfer |
| DNS | 53 | UDP/TCP | Name resolution |
| DHCP | 67/68 | UDP | IP configuration |
| HTTP | 80 | TCP | Web traffic |
| POP3 | 110 | TCP | Mail retrieval |
| NTP | 123 | UDP | Time synchronization |
| IMAP | 143 | TCP | Mail access |
| SNMP | 161 | UDP | Network monitoring |
| SNMP traps | 162 | UDP | Monitoring notifications |
| LDAP | 389 | TCP/UDP | Directory services |
| HTTPS | 443 | TCP | Encrypted web traffic |
| SMB | 445 | TCP | File and printer sharing |
| SMTP submission | 587 | TCP | Mail submission |
| LDAPS | 636 | TCP | LDAP over TLS |
| IMAPS | 993 | TCP | Secure IMAP |
| POP3S | 995 | TCP | Secure POP3 |
| SIP | 5060 | UDP/TCP | VoIP signaling |
| SIP over TLS | 5061 | TCP | Protected SIP signaling |
| RDP | 3389 | TCP/UDP | Remote desktop |

*FTP port 20 is associated with traditional active-mode data connections. Passive FTP uses a negotiated server port.

HTTPS using HTTP/3 typically runs over QUIC on UDP 443.

## 3. TCP vs UDP

### TCP
- Connection-oriented
- Reliable, ordered byte stream
- Uses acknowledgments
- Retransmits lost data
- Has a three-way handshake

Examples: SSH, HTTP/1.1, HTTPS over TCP.

### UDP
- Connectionless
- No built-in delivery guarantee
- No TCP-style handshake
- Lower protocol overhead

Examples: DHCP, NTP, traditional DNS queries.

Important: UDP applications can implement their own reliability mechanisms.

## 4. Important Protocol Differences

### FTP vs SFTP
FTP uses separate control and data connections.
Traditional FTP does not encrypt its traffic.

SFTP works over SSH and encrypts file operations.

SFTP is not the same as FTPS (FTP secured with TLS).

### SSH vs Telnet
SSH encrypts remote sessions.
Telnet does not provide transport encryption.

### HTTP vs HTTPS
HTTP transfers application messages.
HTTPS protects HTTP communication using TLS.

### DNS over UDP vs TCP
Traditional DNS commonly uses UDP 53.
TCP 53 is also supported and used when required.

### RDP
RDP provides graphical remote desktop access.

Default port: 3389.
Transport: TCP, with UDP support.

## 5. Security and SOC Monitoring

### SSH — TCP 22
Potential investigation signals:
- Repeated failed logins
- Successful login after many failures
- Unusual source IP addresses
- Unexpected privileged access

### RDP — TCP/UDP 3389
Potential investigation signals:
- Unusual remote login activity
- Unexpected external access
- Repeated failed authentication
- Connections outside normal patterns

### DNS — UDP/TCP 53
Potential investigation signals:
- Unusual query volume
- Unexpected domains
- Repeated failed resolutions
- Suspicious query patterns

### SMB — TCP 445
Potential investigation signals:
- Unusual file-share access
- Authentication failures
- Connections to many internal hosts

Important:
A suspicious network connection does not automatically prove an attack.

SOC analysts must correlate network observations with logs and system context.

## 6. Useful Wireshark Filters

SSH:
tcp.port == 22

DNS:
dns

HTTP:
http

RDP:
tcp.port == 3389 || udp.port == 3389

SMB:
tcp.port == 445

DHCP:
dhcp

TCP SYN:
tcp.flags.syn == 1 && tcp.flags.ack == 0

## 7. Troubleshooting Checklist

1. Is DNS resolution working?
2. Is the destination IP correct?
3. Is the destination port correct?
4. Is the service listening?
5. Is the network route valid?
6. Is a firewall blocking traffic?
7. Does the server respond?
8. What do the logs and packets show?

Remember:
An open port does not necessarily mean the application is functioning correctly.

## 8. Key Takeaways

- IP identifies the network endpoint.
- TCP/UDP port numbers distinguish services.
- Common ports are defaults, not guarantees.
- TCP and UDP behave differently.
- Encryption limits packet visibility.
- SOC analysts correlate traffic with system logs.
- Understanding protocols is more important than memorizing port numbers alone.
