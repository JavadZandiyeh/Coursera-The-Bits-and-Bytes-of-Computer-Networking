
# 2 The Network Layer
## 2.1 Introduction
- **Local Area Network (LAN) Communication**:
  - Nodes communicate through their physical MAC addresses.
  - Switches learn MAC addresses to route transmissions.

- **Limitations of MAC Addressing**:
  - MAC addressing doesn't scale well.
  - Every network interface has a unique MAC address.
  - No systematic ordering of MAC addresses.
  - Not ideal for long-distance communication.
  - MAC addresses are not location-specific.

- **Address Resolution Protocol (ARP)**:
  - ARP helps nodes learn each other's physical addresses.
  - ARP is limited to single network segments.

- **Need for Network Layer and IP**:
  - Network layer provides a scalable solution.
  - Introduction of Internet Protocol (IP) and IP addresses.

- **IP Address Structure**:
  - 32-bit numbers, divided into 4 octets.
  - Each octet ranges from 0 to 255.
  - Format: Dotted decimal notation (e.g., 12.34.56.78).
  - Invalid example: 123.456.789.100 (numbers exceed 255).

- **Hierarchical Distribution**:
  - IP addresses are distributed to organizations, not by hardware vendors.
  - Example: IBM owns IPs with "9" as the first octet.
  - Routers use this hierarchy to efficiently route packets (e.g., 9.0.0.1).

- **Network vs. Device IPs**:
  - IP addresses are associated with networks, not individual devices.
  - Device MAC addresses remain constant; IP addresses can change based on the network.
  - Example: A laptop's IP address changes when moving between networks (e.g., home vs. internet cafe).

- **IP Address Assignment**:
  - **Dynamic IP Address**:
    - Assigned automatically using Dynamic Host Configuration Protocol (DHCP).
  - **Static IP Address**:
    - Manually configured, typically for servers and network devices.
  - Dynamic IPs are usually for clients, but exceptions may exist.

- **IP Datagram**:
  - Packet at the network layer under the IP protocol.
  - **Sections**:
    - Header
    - Payload

- **IP Datagram Header Fields**:
  1. **Version** (4 bits):
     - Indicates the version of IP (e.g., IPv4 or IPv6).
  2. **Header Length** (4 bits):
     - Length of the IP header. Minimum length is 20 bytes for IPv4.
  3. **Service Type** (8 bits):
     - Specifies Quality of Service (QoS) for router prioritization.
  4. **Total Length** (16 bits):
     - Total length of the IP datagram (header + payload).
  5. **Identification** (16 bits):
     - Groups fragmented messages to reassemble them.
  6. **Flags**:
     - Indicates if the datagram can be fragmented or if it's already fragmented.
  7. **Fragmentation Offset**:
     - Used by receiving end to reassemble fragmented packets in the correct order.
  8. **Time to Live (TTL)** (8 bits):
     - Limits the number of router hops before the datagram is discarded. Prevents endless loops.
  9. **Protocol** (8 bits):
     - Specifies the transport layer protocol used (e.g., TCP or UDP).
  10. **Header Checksum**:
      - Checks the integrity of the IP header. Changes with TTL adjustments.
  11. **Source IP Address** (32 bits):
      - IP address of the sender.
  12. **Destination IP Address** (32 bits):
      - IP address of the receiver.
  13. **IP Options**:
      - Optional field for special features or testing.
  14. **Padding**:
      - Ensures the header is the correct total size, added after IP options if needed.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2014.29.23.png" height="400">
</p>

- **Encapsulation**:
  - IP datagrams are encapsulated as the payload within Ethernet frames.
  - IP datagram's payload typically contains a TCP or UDP packet.

- **Networking Layers**:
  - Each layer supports the layer above it, contributing to the overall networking functionality.
 
<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2014.43.19.png" height="400">
</p>

- **IP Address Structure**:
  - **Network ID**: Identifies the network.
  - **Host ID**: Identifies a specific device within the network.
  - Example: For IP address 9.100.100.100:
    - **Network ID**: First octet (9).
    - **Host ID**: Second, third, and fourth octets (100.100.100).

- **Address Classes**:
  - **Class A**:
    - **Network ID**: First octet.
    - **Host ID**: Last three octets.
    - **Range**: 0-127 in the first octet.
    - **Total Addresses**: 2^24 (16,777,216).
  - **Class B**:
    - **Network ID**: First two octets.
    - **Host ID**: Last two octets.
    - **Range**: 128-191 in the first octet.
    - **Total Addresses**: 2^16 (65,536).
  - **Class C**:
    - **Network ID**: First three octets.
    - **Host ID**: Last octet.
    - **Range**: 192-223 in the first octet.
    - **Total Addresses**: 2^8 (256).

- **Other Classes**:
  - **Class D**:
    - **Usage**: Multicasting.
    - **Range**: 224-239 in the first octet.
  - **Class E**:
    - **Usage**: Experimental, reserved for testing.
    - **Range**: 240-255 in the first octet.

- **CIDR (Classless Inter-Domain Routing)**:
  - Replaces the class system but understanding address classes is still useful for networking education.

- **Identification**:
  - **Class A**: First bit is 0 (Decimal range: 0-127).
  - **Class B**: First bits are 10 (Decimal range: 128-191).
  - **Class C**: First bits are 110 (Decimal range: 192-223).

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2014.56.43.png" height="300">
</p>
