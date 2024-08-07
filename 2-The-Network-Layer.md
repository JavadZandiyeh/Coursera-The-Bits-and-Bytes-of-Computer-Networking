
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

## 2.3 Routing
**Introduction:**
- The internet connects millions of individual networks, enabling near-instantaneous global data access.
- Routing is the process that facilitates communication across these networks.

**Key Concepts:**

1. **Routing Overview:**
   - **Simple yet Complex:** Basic routing is simple, but its underlying mechanisms are complex.
   - **Handled by ISPs and Large Companies:** Intensive routing issues are managed by Internet Service Providers (ISPs) and large companies.

2. **Basic Routing Steps:**
   1. **Packet Reception:** A router receives a data packet on one of its interfaces.
   2. **Destination IP Examination:** The router checks the packet's destination IP address.
   3. **Routing Table Lookup:** The router finds the destination network in its routing table.
   4. **Packet Forwarding:** The router forwards the packet to the interface closest to the remote network.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2023.12.53.png" height="300">
</p>

3. **Example 1: Two-Network Routing**
   - **Network A:** 192.168.1.0/24
   - **Network B:** 10.0.0.0/24
   - **Router Interfaces:** 
     - Network A: 192.168.1.1
     - Network B: 10.0.0.254
   - **Packet Flow:** 
     1. Computer on Network A (192.168.1.100) sends a packet to 10.0.0.10.
     2. Packet sent to the router (192.168.1.1) and forwarded to Network B (10.0.0.10).

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2023.14.55.png" height="300">
</p>

4. **Example 2: Three-Network Routing**
   - **Network A:** 192.168.1.0/24
   - **Network B:** 10.0.0.0/24
   - **Network C:** 172.16.1.0/23
   - **Router 1 Interfaces:** 
     - Network A: 192.168.1.1
     - Network B: 10.0.0.254
   - **Router 2 Interfaces:** 
     - Network B: 10.0.0.1
     - Network C: 172.16.1.1
   - **Packet Flow:** 
     1. Computer on Network A (192.168.1.100) sends a packet to 172.16.1.100.
     2. Packet sent to Router 1 (192.168.1.1), forwarded to Router 2 (10.0.0.1), and then to the final destination (172.16.1.100).

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2023.19.55.png" height="300">
</p>

**Routing on the Internet:**
- **Scale:** Internet routing involves more routers and networks.
- **Mesh Topology:** Core internet routers are interconnected in a mesh for redundancy and multiple paths.
- **Process:** 
  - Routers inspect the destination IP.
  - Look up the routing table for the best path.
  - Forward packets along the determined path.
 
**History and Basics of Routing Tables:**
1. **Early Routers:**
   - Early routers were regular computers with two network interfaces and a manually updated routing table.
   - Modern operating systems still use routing tables for data transmission.
   - You can build a router today with a computer, two network interfaces, and a manually updated routing table.

2. **Common Features:**
   - **Destination Network:** Defines each network the router knows about (network ID and netmask).
   - **Next Hop:** IP address of the next router for the destination network or indicates if the network is directly connected.
   - **Total Hops:** Number of hops to the destination network. Routers aim for the shortest path, which can change due to network conditions.
   - **Interface:** Specifies which router interface should forward the traffic for the destination network.

3. **Characteristics:**
   - Vary by router make and class.
   - Core Internet routers have millions of rows in their routing tables, which are consulted for every packet.
	- Four main columns: Destination Network, Next Hop, Total Hops, and Interface.
    - Catch-all entry for unknown IP addresses.
    - Routing tables update based on network changes (router failures, new links, congestion).
    - Critical for ensuring timely and efficient data delivery across networks.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2023.26.12.png" height="300">
</p>

**Routing Protocols Overview:**
- The real magic lies in how routing tables are continuously updated with new information.
- Routing protocols enable routers to communicate and share information.
- These protocols help routers determine the best path to destination networks.
- Two main categories: Interior Gateway Protocols (IGPs) and Exterior Gateway Protocols (EGPs).

**Interior Gateway Protocols (IGPs):**
1. **Purpose:** 
   - Used within a single autonomous system (AS).
   - Example: Large corporations or ISPs with national-scale networks.

2. **Types:**
   - **Link State Protocols**
   - **Distance Vector Protocols**

**Distance Vector Protocols:**
- **Method:**
  - Routers share their routing table (list of known networks and hop distances) with neighboring routers.
  - A list is referred to as a vector in computer science, hence the name.
- **Example:**
  - Router A and Router B influence each other’s routing tables by sharing hop distances.
  - Router A updates its table based on Router B’s information for quicker paths.
- **Limitations:**
  - Limited knowledge of the overall network state.
  - Slower reaction to distant network changes.
- **Protocols:**
  1. **RIP (Routing Information Protocol):**
	   - **Specification:** IETF RFC 2453
	2. **EIGRP (Enhanced Interior Gateway Routing Protocol):**
	   - **Documentation:** Cisco
<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2023.32.33.png" height="300">
</p>

**Link State Protocols:**
- **Method:**
  - Routers advertise the state of their links (interfaces) to all routers within the AS.
  - Each router knows the details of every other router and network in the AS.
- **Process:**
  - Uses more memory and processing power to run algorithms on this comprehensive data set.
  - Determines the best path to any destination network.
- **Advantages:**
  - Faster reaction to network changes.
  - More accurate and efficient routing decisions.
- **Evolution:**
  - Link state protocols have become dominant due to advancements in computer hardware.
- **Protocols:**
  - **OSPF (Open Shortest Path First):**
	  - **Specification:** IETF RFC 2328 
<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2023.33.40.png" height="300">
</p>

**Exterior Gateway Protocols (EGPs):**
- **Purpose:** 
  - Facilitate communication between routers at the edges of different autonomous systems (ASes).
  - Essential for data exchange across organizations and for the Internet's operation.
- **Role in the Internet:**
  - Core Internet routers use EGPs to forward traffic between autonomous systems.
  - Key to managing the vast network of interconnected ASes.
- **BGP (Border Gateway Protocol):**
  - **Specification:** IETF RFC 4271
  - **Role:** Standard for Internet-wide information exchange.
  - BGP is the sole standard for external routing.

**Autonomous Systems (ASes):**
- **Definition:** 
  - Defined collections of networks under a single organization.
  - ASes are integral to Internet routing.
- **Core Router Goal:**
  - Route data efficiently to the edge router of the target AS.

**Internet Assigned Numbers Authority (IANA):**
- **Responsibilities:**
  - Manages IP address allocation and Autonomous System Number (ASN) allocation.
- **ASNs:**
  - 32-bit numbers assigned to individual ASes.
  - Unlike IP addresses, ASNs are presented as single decimal numbers.
  - Less frequently seen by users.
  - ASNs help identify entire ASes without needing to be split into segments like IP addresses.

 <p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-07%20at%2023.36.10.png" height="300">
</p>

### IPv4 Address Limitations and Non-Routable Address Space

**Historical Context:**
- **Problem:** By 1996, it was clear the Internet’s growth was outpacing the available IPv4 addresses.
  - **IPv4 Limitations:** IPv4 uses a 32-bit address system, providing 4,294,967,295 unique addresses.
  - **Current Usage:** As of 2017, with approximately 7.5 billion people and numerous data centers, IPv4 cannot support all users and devices.

**RFC 1918:**
- **Publication:** Introduced in 1996 to address the IPv4 address shortage.
- **Purpose:** Defined non-routable address space to manage internal network communications without affecting global routing.
  - **Non-Routable Address Space:** IP ranges that cannot be routed over the Internet but can be used internally within organizations.
  
**Defined Ranges:**
- **10.0.0.0/8**
- **172.16.0.0/12**
- **192.168.0.0/16**
  - **Usage:** These ranges are free for anyone to use internally and are not routable by core Internet routers.

**Routing Implications:**
- **Interior Gateway Protocols (IGPs):** Can route non-routable addresses within an autonomous system.
- **Exterior Gateway Protocols (EGPs):** Do not route non-routable addresses across the Internet.
- **Network Address Translation (NAT):** Will be discussed in a future module. NAT allows devices in non-routable address spaces to communicate with the Internet.

## 2.4 Glossary Terms
**Address class system:** A system which defines how the global IP address space is split up

**Address Resolution Protocol (ARP):** A protocol used to discover the hardware address of a node with a certain IP address

**ARP table:** A list of IP addresses and the MAC addresses associated with them

**ASN:** Autonomous System Number is a number assigned to an individual autonomous system

**Demarcate:** To set the boundaries of something

**Demarcation point:** Where one network or system ends and another one begins

**Destination network:** The column in a routing table that contains a row for each network that the router knows about

**DHCP:** A technology that assigns an IP address automatically to a new device. It is an application layer protocol that automates the configuration process of hosts on a network

**Dotted decimal notation:** A format of using dots to separate numbers in a string, such as in an IP address

**Dynamic IP address:** An IP address assigned automatically to a new device through a technology known as Dynamic Host Configuration Protocol

**Exterior gateway:** Protocols that are used for the exchange of information between independent autonomous systems

**Flag field:** It is used to indicate if a datagram is allowed to be fragmented, or to indicate that the datagram has already been fragmented

**Fragmentation:** The process of taking a single IP datagram and splitting it up into several smaller datagrams

**Fragmentation offset field:** It  contains values used by the receiving end to take all the parts of a fragmented packet and put them back together in the correct order

**Header checksum field:** A checksum of the contents of the entire IP datagram header

**Header length field:** A four bit field that declares how long the entire header is. It is almost always 20 bytes in length when dealing with IPv4

**IANA:** The Internet Assigned Numbers Authority, is a non-profit organization that helps manage things like IP address allocation

**Identification field:** It is a 16-bit number that's used to group messages together

**Interface:** For a router, the port where a router connects to a network. A router gives and receives data through its interfaces. These are also used as part of the routing table

**Interior gateway:** Interior gateway protocols are used by routers to share information within a single autonomous system

**IP datagram:** A highly structured series of fields that are strictly defined

**IP options field:** An optional field and is used to set special characteristics for datagrams primarily used for testing purposes

**Network Address Translation (NAT):** A mitigation tool that lets organizations use one public IP address and many private IP addresses within the network

**Next hop:** The IP address of the next router that should receive data intended for the destination networking question or this could just state the network is directly connected and that there aren't any additional hops needed. Defined as part of the routing table

**Non-routable address space:** They are ranges of IPs set aside for use by anyone that cannot be routed to

**Padding field:** A series of zeros used to ensure the header is the correct total size

**Protocol field:** A protocol field is an 8-bit field that contains data about what transport layer protocol is being used

**Routing protocols:** Special protocols the routers use to speak to each other in order to share what information they might have

**Service type field:** A eight bit field that can be used to specify details about quality of service or QoS technologies

**Static IP address:** An IP address that must be manually configured on a node

**Subnet mask:** 32-bit numbers that are normally written as four octets of decimal numbers

**Subnetting:** The process of taking a large network and splitting it up into many individual smaller sub networks or subnets

**Time-To-Live field (TTL):** An 8-bit field that indicates how many router hops a datagram can traverse before it's thrown away

**Total hops:** The total number of devices data passes through to get from its source to its destination. Routers try to choose the shortest path, so fewest hops possible. The routing table is used to keep track of this

**Total length field:** A 16-bit field that indicates the total length of the IP datagram it's attached to
