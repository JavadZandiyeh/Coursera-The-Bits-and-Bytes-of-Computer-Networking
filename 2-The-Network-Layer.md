
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

How MAC and IP addresses relate through ARP:

- **Address Resolution Protocol (ARP)**:
  - **Purpose**: Discover the MAC address associated with a given IP address.
  - **Usage**: Required to encapsulate an IP datagram inside an Ethernet frame.

- **Process**:
  1. **Creating an Ethernet Frame**:
     - Need a destination MAC address to complete the frame header.
  2. **ARP Table**:
     - Stores mappings of IP addresses to MAC addresses on a local device.
  3. **Sending Data**:
     - **Case 1**: Destination MAC address is not in the ARP table.
       - **Action**: Send a broadcast ARP message to all devices on the local network (MAC Broadcast address: all Fs).
  4. **ARP Response**:
     - **Received by**: The device with the required IP address.
     - **Content**: MAC address of the responding device.
     - **Result**: The sending device can now add the correct MAC address to the Ethernet frame header.
  5. **Storing Information**:
     - The sending device updates its ARP table with the new IP-to-MAC mapping.
     - **Purpose**: Avoid future ARP broadcasts for this IP address.
  6. **ARP Table Expiry**:
     - Entries expire after a short time to accommodate network changes.

- **Benefit**:
  - Ensures efficient communication by mapping IP addresses to MAC addresses, reducing the need for repeated broadcasts.

## 2.2 Subnetting
Subnetting is the process of dividing a large network into smaller subnetworks (subnets extend the capabilities of network and host IDs).

- **Address Classes**:
  - Address classes (A, B, C) divide global IP space into discrete networks.
  - Example: IP address 9.100.100.100 belongs to the 9.0.0.0 Class A network.
  - **Routing**:
    - **Core Routers**: Route messages based on the network ID.
    - **Gateway Routers**: Serve as entry and exit points for specific networks and route data to the correct system using the host ID.

- **Need for Subnetting**:
  - Class A networks can have up to 16,777,216 IP addresses, which is too many for a single router to manage.
  - **Solution**: Subnets divide a large network into smaller, manageable segments.
  - Each subnet has its own gateway router for ingress and egress, improving network organization and performance.
 
<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2020.47.01.png" height="300">
</p>

**IP Address Structure**:
- **Network ID**: Identifies the network.
- **Subnet ID**: Further divides the network into subnets.
- **Host ID**: Identifies individual hosts within the network.

**Subnet Masks**:
- **Function**: Define the boundary between network, subnet, and host IDs.
- **Structure**: 32-bit numbers, often written as four octets in decimal (e.g., 255.255.255.0).
  - The mask part (all ones) indicates the subnet ID.
  - The remaining part (all zeros) indicates the host ID.

**Subnet Mask Example**:
- **255.255.255.0**: 
  - **Binary**: 24 ones followed by eight zeros.
  - **Usage**: Defines the last octet for host IDs.
  - **Host Range**: Provides 256 possible host addresses (0-255), but typically only 1-254 are usable (0 is reserved, 255 is for broadcast).

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2020.48.02.png" height="300">
</p>

**Advanced Subnet Mask**:
- **255.255.255.224**:
  - **Binary**: 27 ones followed by five zeros.
  - **Host Range**: 32 possible addresses.
  - **Shorthand Notation**: /27 (e.g., 9.100.100.100/27).

**Practical Application**:
- **Core Routers**: Route based on network ID.
- **Gateway Routers**: Use subnet ID for routing within the network and host ID for final delivery.
- **ARP**: Helps discover MAC addresses corresponding to IP addresses.

**Address Classes and Their Limitations**:
- **Initial Approach**: Address classes (A, B, C) were the first method to organize the global Internet IP space.
- **Limitations**:
  - Fixed network ID sizes: 8-bit for Class A, 16-bit for Class B, 24-bit for Class C.
  - Imbalanced network sizes: 
    - Only 254 Class A networks.
    - 2,097,152 potential Class C networks.
  - Inflexibility for business needs: 
    - Class C (254 hosts) often too small.
    - Class B (65,534 hosts) often too large.
  - Routing table congestion: Multiple Class C networks for the same destination.

**Introduction of CIDR (Classless Inter-Domain Routing)**:
- **Purpose**: Offers a more flexible and efficient way to manage IP addresses and routing.
- **Concept**: 
  - Abandons fixed address classes.
  - Uses subnet masks to define networks.
  - Combines network and subnet IDs into one.
  - Introduces CIDR notation (e.g., 9.100.100.100/24).

**Benefits of CIDR**:
- **Simplification**: 
  - Routers need fewer entries in routing tables.
  - More straightforward handling of IP addresses.
- **Flexible Network Sizes**:
  - Allows creation of networks of varying sizes (e.g., /23, /24).
  - Avoids rigid Class A, B, C limitations.
- **Efficient Address Allocation**:
  - A /23 network (512 potential hosts) vs. two /24 networks (508 hosts).
  - Maximizes usable IP addresses by reducing wasted space.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2021.12.46.png" height="300">
</p>

**Practical Example**:
- **Without CIDR**:
  - Company needs more than 254 addresses.
  - Requires multiple Class C networks.
  - Leads to multiple routing table entries.
- **With CIDR**:
  - Can use a single /23 network (255.255.254.0).
  - Reduces routing table entries.
  - Increases available hosts (510 usable IPs).
