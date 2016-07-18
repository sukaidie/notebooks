## 02 Grundlagen

#### Information security

* **Datensicherheit** Data security
  * Mit Datensicherheit wird der Schutz von Daten hinsichtlich gegebener Anforderungen an deren **Vertraulichkeit, Verfügbarkeit und Integrität** bezeichnet.

* **Datenschutz** Data protection and privacy
  * Datenschutz soll den Einzelnen davor schützen, dass er durch den Umgang mit seinen personenbezogenen Daten in seinem Persönlichkeitsrecht beeinträchtigt wird.

#### Security of ICT Systems

* Part of Information security
* **ICT** information and communication technology
  * **Computer security** Secure storage and processing of data
  * **Network security** Secure exchange of data

#### Schutzziele

|                 | Confidentiality | Integrity | Availability |
| --------------- | --- | --- | --- |
| Threats         | Eavesdropping | Modification, Interception, fake Information Source | Failure of Systems, intentional damage and overloading of resources |
| How to Protect  | Encryption, Information Hiding | Cryptographic checksum, Authentication and Digital signature | Resource Redundancy |

## 03 Terms

* Cryptology
  * Cryptology
  * Cryptanalysis
* Information Hiding
  * Steganography
  * Watermarking

## 04 Classical Cryptography

* Symmetric crypto Systems
  * ke = kd
  * keys for n Partners : (n X (n - 1)) / 2
* Assymmetric crypto Systems
  * ke != kd
  * keys for n Partners : n

|                   | Substitution | Caesar      | Vigenère |
| ----------------- | ------------ | ----------- | -------- |
| Letter Frequency  | not changed  | not changed | changed  |
| (max) key length  | 1            | n           | n        |
| key sprace        | 25           | n!          | 26^n     |

* The basic Principles of Classical Cryptography
  * Substituion
    * Substituion
    * Monoalphabetic Substituion (e.g. Caesar)
    * Polyalphabetic Substituion (e.g. Vigenere)
  * Transposition
    * Columnar Transposition
* Information Theoretical Security
  * **Unconditional Security** *can not be broken with infinite computational resources*
    * Key length equal to Plantext
    * key stream is truely random
    * key stream is only used once
  * **Computational Security** *O(n) is very large and known*
  * **Relative Security**
* Strength of crypto Systems
  * **Diffusion** *by Transposition (permutaion)*
  * **Confusion** *by Substituion*

## 05 Symmetrical Cryptography

* Block cipher
  * Structure of block cipher
  * Iterative Block cipher
    * Use the same round transformation in all rounds **except of initial or final round**
  * Key-alternating block cipher
    * First round key is added before the first round
    * Last round key is added after the last round
  * Modes of Operation
    * Electronic codebook (ECB)
    * Cipher-Block chaing (CBC)
* Stram cipher
  * Less popuar than block cipher
  * Often used in mobole appliacation
  * Generally require fewer resources
  * Encrypt faster than block cipher
* Random Number Generator
  * True Random Number Generator
  * General Pseudo Random Number Generator
  * Cryptographically Secure Pseudo Random Number Generator
* LSFR
* DES
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/DES.svg)

* AES
  * Data Path
    * ![](https://dl.dropboxusercontent.com/u/55616012/note/AES.svg)
  * Key Expansion
    * ![](https://dl.dropboxusercontent.com/u/55616012/note/AES_key.svg)

## 07 Asymmetric Cryptography

* Kinds of Mathematical Functions
  * One-way function
  * Trapdoor function
* Diffie-Hellman Key Exchange
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/diffe.svg)
  * base on **discrete logarith problem**
  * Primitive root modulo p
    * if g^t for 0 ≤ t ≤ p-2 returns all values from 1 to p-1
* Station-to-Station Protocol
* RSA
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/RSA.svg)
  * base on **factorization problem**
  * multiplicative inverse
    * (e * d) mod n = 1
    * (m^e mod n)^d mod n = m^(e * d) mod n = m  
  * key generation
    1. select **n = p * q**
    2. generate **ϕ = (p - 1) * (q - 1)**
    3. select **(e, d)**, so that **(e * d) mod ϕ = 1**
  * Euclidean Algorithm
  * Extended Euclidean Algorithm
* EIGamal
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/EIGamal.svg)
  * base on Diffie-Hellman Key Exchange

## 08 Hybird Procedures
## 09 Hash Function

* Types of Hash Functions
  * Keyless **Modification Detection (MDC)**
    * One Way Hash Function (OWHF)
      * Preimage Resistance
      * 2nd Preimage Resistance
    * Collosion Resistant Hash Function (CRHF)
      * Collosion Resistance
  * Key-Dependent **Message Authentication (MAC)**
* Requirements
  * Preimage resistance
  * 2nd Preimage Resistance
  * Collosion Resistance
  * Non-correlation
  * Near-collision resistance
  * Partial-preimage resistance
* MD4
  * 3 auxiliary functions

    ```javascript
    // If X = 1, return  Y, else return Z
    var f = function (x, y, z) {
      return ( x == 1 ) ? y : Z;
    };
    // If at least 2 bits are set to 1, G returns 1, else 0
    var g = function (x, y, z) {
      return ( (x + y + z) >= 2 ) ? 1 : 0;
    };
    // x XOR y XOR z
    var h = function (x, y, z) {
      return x ^ y ^ z;
    }
    ```

  * ![](https://dl.dropboxusercontent.com/u/55616012/note/MD4.svg)
  * "+" means here addition modulo 32 Bits

## 10 Network Security Basics

* Security Solutions
  * **Extra Functions** : Integration of security enhancing functions into existing protocols
  * **Protocol Stacks** : Specification of additional protocols to enhance the security  of protocol stacks
  * **Additional components** : Additional functions and network components  to improve network/communication security
* **X.800** OSI Security Services
  * X.800 extends **X.200** (OSI reference model) with **Security Services and related mechanisms** to cover secure communications between open systems
* Algorithms --> Security Mechanisms --> Security Services
* Security Goals
  * Authentication
  * Access Control
  * Data Confidentiality
  * Data Integrity
  * Non-Repudiation
* Examples for security mechanisms
  * Encryption
  * Digital Signature
  * Access control mechanisms
  * Data integrity mechanisms
  * Authentication exchange mechanism

![](https://dl.dropboxusercontent.com/u/55616012/note/Encryptions.svg)

* Asymmetrical cryptosystem
  * Solutions
    * Direct contact with communication partner
    * Certificates
  * Certificates - Distribution mechanisms
    * Direct distribution
    * Certifcate Server
    * Public Key Infrastructure (PKI)
  * Public Key Infrastructure
    * **End Entity** : (Server) requests a Certificate or (Client) verifies a Certificate
    * **CA (Certification Authority)** : issues Certificate
    * **CRL (Certificate Revocation List)** : maintains the Repository in the form of list
    * **RA (Registration Authority)** : handles requests and validates Information
    * **Repository** : store Certificate and CRLs
  * Types of Certificate
    * Root Certificate
    * CA Certificate
    * End Entity Certificate
  * Web of trust
    * different trust level : compete, marginal, untrusted
    * A Certificate is valid, when it is with one "compete" or two "marginal" assigned

## 11 Attack

* Glossar
  * Malware 恶意软件
  * Botnet 僵尸网络
  * Spamming 滥发电子讯息
  * Phishing 钓鱼式攻击
  * Pharming 网址重定向
  * Threats 威胁
  * Vulnerability 安全隐患，漏洞
  * Exploit 利用程序中的某些漏洞，来得到计算机的控制权
  * Countermeasure 反制措施
  * Hacker 黑客
  * Cracker 破解者
  * Script Kid 脚本小子
  * Spoofing 电子欺骗
  * Virus 病毒
  * Worm 蠕虫
  * Trojan Horse 木马
  * Wiretapping 电话窃听
  * Eavesdropping 窃听
  * Sniffing 嗅探
  * Interception 截取，拦截
  * IP-Spoofing IP欺骗
* Passive Attacks
  * Interception of the content of the communication
  * Collectiing and analyzing the traffic patterns
* Active Attacks
  * Attacks on the communication relationships
    * Man in the Middle
    * IP Spoofing
  * Attacks on the resources
    * DoS (Denial of Service), TCP-SYN flooding
* Attacks on different Layers

| Physical     | Date Link       | IP            | TCP/UDP        | Appliacation    |
| ------------ | --------------- | ------------- | -------------- | --------------- |
| Interception | ARP Spoofing    | ICMP Packets  | Portscan       | Buffer Overflow |
| DoS          | Man in Middle   | Ping of Death | Fingerprinting | DoS, Worms      |
|              | DoS (Swithes)   | IP Spoofing   | DoS            | Trojans         |
|              | Rediection      | DHCP Spoofing |                | Virus           |
|              | Packet Sniffing |               |                | Spam            |

* TCP / UDP

| TCP                                 | UDP                              |
| ----------------------------------- | -------------------------------- |
| Conection must be first established | Date is send with initialazition |
| Stream-based                        | Message-based                    |
| all data is acknowledged            | No acknowledgment                |
| Flow control                        | No Dataflow management           |
| Ordered                             | Not Ordered                      |

* TCP Header
  * Sequence Nummer
  * Acknowledgment Nummer
  * Data offset
  * TCP Flags
    * SYN(建立连接), RST(重置), FIN(关闭)
  * Windows Size
  * Checksum
  * Urgent Pointer
* TCP and UDP Port
  * Well-known Ports
  * Registered Ports
  * Dynamic / private Ports
* Portscan
  * **Connect Scan**
    * open : connect() completes the three-way handshake and then immediately sent a reset (RST) packet to close the connection
    * closed : recieves RST packet from Remote
  * **Syn Scan**
    * open : receives an acknowledgment to a SYN request, then sends an RST to reset the session, and the handshake is never completed.
    * closed : recieves RST packet from Remote
  * **Fin Scan**
    * open : no response
    * closed : recieves RST packet from Remote
* **Fingerprinting** : Each OS has unique feature at the implementation of communication protocol
* Denial of Service
  * Resources that could be attacked
    * Network bandwidth
    * System resources
    * Appliacation resources
  * Classical DoS Attacks
    * flooding Attacks
    * Smurf
    * Fraggle
    * Syn flooding
* Distributed Denial of Service (DDoS)
* Buffer Overflow

![](https://dl.dropboxusercontent.com/u/55616012/note/stackoverflow.svg)

* Social Engineering
  * Phishing, Viusal Spoofing, Pharming
* Host specific measures
  * turn on AutoUpdate
  * disable unused Services
  * secure necessary Services
  * disable Access to Telnet, FTP
  * check log
  * install attack Detection software

## 12 Intrusion Detection Systems

* Typical Steps of network based attack
  * Target searching *ICMP ping*
  * Target analyzing *TCP/UDP port scan*
  * Intrusion
* Security level
  * 1st. protection of internal network
  * 2nd. network based sensor System
  * 3rd. host based sensor System
* Intrusion prevention System (IPS)
  * part of firewall
  * analyze (recognize unusual traffic) and control (drop, block) appliacation layer traffic
* Intrusion response System (IRS)
  * automaic real-time reaction
  * patterns are asscociated with predefined response actions
  * measures
    * shutdown services and connections, session block, disable server, identification of attacker
* Intrusion Detection System (IDS)
  * Network IDS
    * Anomaly-based Detection
    * Signature/Pattern-based Detection
      * Signature : traffic patterns
      * Filter : Signature in a machine readable form
      * Filter search keys at **Protocol, Ports, Flags, Strings, Binary**
  * Host-based IDS
* Honeypot
* Honeynets

## 13 Firewall

* Definition : prevent unauthorized process or user from accessing a private Network
* Personal Firewall
  * Deny unauthorized remote access
  * Monitor outgoing activity
  * Organization puropose
  * Interactive mode
* Network Firewall
  * Layer 2 Firewall
  * Packet Filter
    * Static Packet Filter (stateless) : pass or reject Packet based on set of rules
      * source / destination IP
      * source / destination Ports
      * IP protocol field
      * Interface
    * Dynamic Packet Filter (stateful)
  * Appliacation Filter (Proxy)
    * Circuit level Gateway
    * Appliacation level Gateway
    * Bastion Host
* Firewall Location and Configuration
  * Screening router
  * Dual-homed Host
  * Screened basion host
  * Screened subnet
    * De-Militarized Zone (DMZ)
  * Network address Translation (NAT)
* Firewall Administration
  * Filter rules
    * chains : INPUT, FORWARD, OUTPUT
    * action : ACCEPT, DROP, REJECT
    * default Policies
      * Whitelisting (default = drop)
      * Blaklisting  (default = accept)
  * iptables in Linux
    * ``# iptables [-AI] [-io interface] [-p tcp|udp|icmp|all] [-s srcIP] [--sport range] [-d desIP] [--dport range] -j [ACCEPT|DROP|REJECT|LOG]``
    * -A : new rule at the end
    * -io : Interface (eth0, wlan0, etc)
    * -p : tcp, udp, icmp and all
    * -s : souce IP, 192.168.1.0/24
    * -d : destination IP
    * -j : actions, ACCEPT, DROP, REJECT, LOG

## 14 User Authentication

* Types of Authentication
  * Password Authentication
  * Token Authentication
  * Biometric Authentication
  * Remote User Authentication
    * Direct Authentication
    * Chanllenge response Authentication
    * ![](https://dl.dropboxusercontent.com/u/55616012/note/auth.svg)
* Two-Party Authentication
  * Extensible Authentication Protocol (EAP)
  * Remote Access Dial in user Service (RADIUS)
    * Network Access Server (NAS)
    * RADIUS Server
  * 802.1X Authentication
    * Supplicant
    * Authenticator (NAS, RADIUS Client)
    * Uncontrolled Port
    * Controlled Port
    * Authentication Server (RADIUS Server)
  * 802.11
    * open System
    * shared key Authentication
      * 路由器生产随机数字(Chanllenge)，填写共享密码，将哈希值(Chanllenge + Password)发给路由
      * Chanllenge response
      * WEP 有线等效加密
  * 802.11i
    * WPA
      * TKIP加密
      * PSK : preshared key Authentication 个人用户简化版
      * 企业版本 (EAP + RADIUS)
    * WPA2
      * TKIP, AES加密
* Trusted third-party Authentication
  * Kerberos
    * Key Distribution Center
      * **Authentication Server** generate TGT (Ticket Granting Ticket)
      * **Ticket Granting Server** generate SGT (Server Granting Ticket)
    * ![](https://dl.dropboxusercontent.com/u/55616012/note/kerberos.svg)

## 15-A IPSec

**Security Option**

| Appliacation | Transport | Network | Data Link |
| ------------ | --------- | ------- | --------- |
| PGP, HTTPS   | SSL/TLS   | IPSec   | WLAN, PPP |

* IP Security Architecture
  * Authentication Header (AH)
  * Encapsulating Security Payload (ESP)
  * Internet Security Association and key management protocol
  * Internet key Exchange  
* AH and ESP
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/ipsec.svg)
* Internet Key Exchange
  * provides dynamically negotiation of IPSec Security Associations
  * Modes
    * Main Mode Exchange
    * Aggressive Mode Exchange

## 15-B SSL/TLS and SSH

* SSL/TLS Architecture
  * Record Protocol
  * Handshake Protocol
  * Change Cipher Spec Protocol
  * Alert Protocol
* Record Protocol
  * content type
  * version
  * length
  * Protocol Message
    * Handshake Protocol
    * Change Cipher Spec Protocol
    * Alert Protocol
    * Appliacation Data (eg. Http Message)
  * MAC
* Handshake Protocol
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/ssl.svg)
* SSH
  * Transport Layer Protocol
    * key exchange
    * verify signature
  * User Authentication Protocol
  * Connection Protocol

## 16 VPN

* Glossar
  * VPN virtual private network
  * POP Point of presence
  * PPP Point-to-Point Protocol
  * PPTP Point-to-Point Tunneling Protocol
  * GRE Generic Routing Encapsulation
  * NAS Network access Server
  * MPLS  Multi-Protocol Label Switching
* **Tunneling** Encapsulation of a packet into an encrypted packet
  * End point
    * Authentication
    * Access Control
    * Nehotiation of security services
  * Encapsulation protocol
* VPN devices
  * VPN Gateway
  * VPN Client
* Security services
  * End-to-POP
  * End-to-LAN
  * End-to-End
  * POP-to-POP
  * LAN-To-POP
  * LAN-to-LAN
* VPN Architecture
  * Site-Site intranet VPN :  *LAN-to-LAN Mode*
  * Remote access VPN :  *End-to-LAN Mode*
  * Extranet VPN :  *combination*
* VPN Tunneling Protocol
  * Generic Routing Encapsulation
    * Encapsulation and Forwarding
    * GRE Header
      * Checksum : provide data integrity
      * Protocol Type :  indicate the Protocol type of Payload
  * Point-to-Point Tunneling Protocol (PPTP)
    * communication between **Access Control (PAC)** and **Netword server (PNS)**
    * Steps
      * Connecting to internet using PPP
      * establishing a control channel
        * PPP and GRE parameters via TCP Packet
      * PPTP tunnel is established
      * A PPP connection between PAC and PNS
      * send IP-Packet(使用局域网地址 with local address) inside PPP tunnel
    * ![](https://dl.dropboxusercontent.com/u/55616012/note/pptp.svg)
