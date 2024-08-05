# 1 Introduction to Networking
## 1.1 The TCP/IP Five-Layer Network Model
To grasp networking, it's essential to understand the components involved, from physical cables to communication protocols. This course focuses on a five-layer model:

1. **Physical Layer**: 
   - Represents physical devices interconnecting computers.
   - Includes networking cables, connectors, and signal transmission specifications.

2. **Data Link Layer**: 
   - Defines a way to interpret signals for device communication.
   - Common protocols: Ethernet, which specifies physical layer attributes and data delivery to nodes on the same network.

3. **Network Layer**: 
   - Allows different networks to communicate via routers.
   - Protocol: IP (Internet Protocol), essential for internet and small network communication.

4. **Transport Layer**: 
   - Ensures data is delivered to the correct applications on nodes.
   - Common protocols: TCP (Transmission Control Protocol) for reliable delivery, and UDP (User Datagram Protocol) for less reliable but faster delivery.

5. **Application Layer**: 
   - Contains application-specific protocols for activities like web browsing and email.
   - These protocols are often the most familiar to users.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-04%20at%2011.47.25.png" height="400">
</p>

**Analogy**: 
- **Physical Layer**: Delivery truck and roads.
- **Data Link Layer**: Moving from one intersection to another.
- **Network Layer**: Deciding which roads to take from address A to B.
- **Transport Layer**: Ensuring the delivery driver knocks on the right door.
- **Application Layer**: The contents of the delivered package.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-04%20at%2011.45.25.png">
</p>

## 1.2 The Basics of Networking Devices
Computer networks use various cables and devices to enable communication between computers.

**Cables:**
1. **Copper Cables:**
   - **Categories:** The most common types are Cat5, Cat5e, and Cat6.
   - **Function:** Copper cables transmit binary data through voltage changes.
   - **Differences:**
     - **Cat5:** Older, largely replaced by Cat5e.
     - **Cat5e:** Improved to reduce crosstalk, resulting in fewer data errors.
     - **Cat6:** Higher specifications, faster and more reliable but more expensive and shorter maximum distance at higher speeds.
   - **Crosstalk:** Unwanted signal interference between wires, leading to data errors.

2. **Fiber Optic Cables:**
   - **Construction:** Made of glass fibers that transmit data via light pulses.
   - **Advantages:** Faster data transmission, less susceptible to electromagnetic interference, and capable of longer distances compared to copper.
   - **Usage:** More common in data centers than in offices or homes due to higher cost and fragility.

While cables establish point-to-point connections between two devices, network devices enable communication among many computers.

**Hubs:**
- **Function:** A physical layer device that connects multiple computers.
- **Operation:** All connected devices receive data simultaneously and must determine if the data is relevant to them.
- **Issue:** Creates a collision domain where only one device can communicate at a time, leading to network slowdowns due to data collisions and retransmissions.
- **Status:** Mostly obsolete and considered a historical artifact.

**Switches:**
- **Function:** A more advanced device than hubs, connecting multiple devices for communication.
- **Operation:** As a data link layer device, a switch inspects Ethernet protocol data, identifies the intended recipient, and sends data only to that specific device.
- **Advantage:** Reduces or eliminates collision domains, resulting in fewer retransmissions and higher network throughput.

Hubs and switches connect computers within a single network, known as a LAN (Local Area Network). To send or receive data between different networks, routers are used.

**Routers:**
- **Function:** Forward data between independent networks.
- **Operation:** Unlike hubs (layer one) and switches (layer two), routers operate at layer three (network layer). They inspect IP data to determine routing.
- **Routing Tables:** Store information for routing traffic between various networks worldwide.
- **Types:**
  - **Home/Small Office Routers:** Simple routing tables, primarily forward traffic to the ISP (Internet Service Provider).
  - **Core Routers:** Handle large traffic volumes and complex routing decisions, forming the backbone of the internet.
- **Protocol:** Routers use the Border Gateway Protocol (BGP) to share data and learn optimal traffic paths.
- **Role:** Ensure efficient data transmission across the internet, with traffic often passing through numerous routers to reach its destination.

Network devices enable communication between computers, whether nearby or far apart. These devices, known as nodes, can function as servers or clients:

- **Server:** Provides data to a requesting entity (client).
- **Client:** Receives data from a server.
- **Dual Roles:** Nodes can be both servers and clients at different times, handling multiple tasks.
- **Primary Function:** Nodes are usually categorized based on their main role in the network. For example, an email server's primary role is to serve data to clients, even if it occasionally acts as a client itself.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-05%20at%2010.38.39.png" height="400">
</p>

## 1.3 The Physical Layer
The physical layer of the network stack focuses on transmitting binary data (ones and zeros) between devices. Though it involves complex mathematics, physics, and electrical engineering, IT support specialists need to understand its more accessible aspects for troubleshooting and setup. Key points include:

- **Bits:** The smallest units of data (ones and zeros) transmitted across the physical layer.
- **Modulation (Line Coding):** The process of varying electrical charges on a network cable to represent ones and zeros.
- **Transmission:** Modern networks can transmit billions of bits per second using standard copper network cables.
- **Role:** The physical layer enables all data transmission, from streaming music to using ATMs, by sending binary data through various network connections.

**Twisted pair cables** are the most common type used for connecting computing devices. They consist of pairs of copper wires twisted together to reduce electromagnetic interference and crosstalk. Key points include:

- **Structure:** Standard Cat6 cables have eight wires (four twisted pairs) inside a single jacket.
- **Usage:** The number of pairs used depends on the transmission technology.
- **Duplex Communication:** Allows information to flow in both directions simultaneously using separate pairs for each direction.
  - **Full Duplex:** Both devices can communicate simultaneously.
  - **Half Duplex:** Only one device can communicate at a time if there's a connection issue.
- **Simplex Communication:** Information flows in only one direction.

The final steps of the physical layer involve how network connections are terminated and used at the endpoints. Here’s a summary:

**Twisted Pair Network Cables:**
- **Termination:** Twisted pair cables end with an RJ-45 plug, the most common type in networking.
- **Connection:** These plugs connect to RJ-45 network ports on devices like switches, servers, and desktops.

**Network Ports:**
- **LED Indicators:** Ports have two LEDs:
  - **Link Light:** Indicates a proper connection between two powered-on devices.
  - **Activity Light:** Flashes when data is transmitted. In modern networks, it indicates the presence of traffic.
- **Switch Ports:** Often use LEDs for multiple status indications, including link speed.

**Mounted Network Ports:**
- **Locations:** Can be found on walls or under desks.
- **Patch Panels:** Cables from these ports connect to a patch panel, which has many network ports but doesn’t process data. Additional cables run from the patch panel to switches or routers to complete the network connection.

## 1.4 The Data Link Layer
**Wireless vs. Cable Networks:**
- **Current Trends:** Wireless and cellular internet access are becoming common, but traditional cable networks remain dominant in workplaces and data centers.
- **Ethernet:** The primary protocol for sending data over individual links.

**Ethernet and the Data Link Layer:**
- **Function:** Allows higher-level software to send and receive data without concerning itself with the physical layer.
- **Abstraction:** Enables uniform operation of internet transport and application layers regardless of connection type.

**Key Learning Outcomes:**
- **MAC Addresses:** Understanding their role in identifying computers.
- **Ethernet Frames:** Components and structure.
- **Address Types:** Differentiating between Unicast, Multicast, and Broadcast addresses.
- **Cyclical Redundancy Checks (CRC):** Ensuring data integrity.

**Historical Context:**
- **Origins:** Ethernet was created in 1980 and standardized in 1983.
- **Evolution:** Few changes since inception, primarily to support increased bandwidth.
- **Early Networking:** Before switches, devices shared collision domains, leading to data collisions.

**Collision Domains and CSMA/CD:**
- **Definition:** A network segment where only one device can transmit at a time.
- **CSMA/CD (Carrier Sense Multiple Access with Collision Detection):** Protocol to manage data transmission and prevent collisions.
  - **Mechanism:** Nodes transmit if the channel is clear; collisions result in a pause and retry with random intervals.

**MAC Addresses:**
- **Uniqueness:** Globally unique identifiers for network interfaces.
- **Structure:** 48-bit number, split into Organizationally Unique Identifier (OUI) and device-specific section.
  - **OUI:** Assigned by IEEE to manufacturers.
  - **Device-Specific:** Ensures uniqueness within the manufacturer's range.
- **Representation:** Six groups of two hexadecimal digits.
- **Purpose:** Used by Ethernet to direct data to the correct recipient even within a shared collision domain.

**Types of Ethernet Transmissions:**

1. **Unicast:**
   - **Definition:** Transmission from one device to one specific device.
   - **Identification:** The least significant bit in the first octet of the destination MAC address is set to zero.
   - **Processing:** Sent to all devices on the collision domain, but only processed by the intended recipient.

2. **Multicast:**
   - **Definition:** Transmission to multiple devices, but not all.
   - **Identification:** The least significant bit in the first octet of the destination MAC address is set to one.
   - **Processing:** Sent to all devices on the local network segment and accepted or discarded based on device configurations.

3. **Broadcast:**
   - **Definition:** Transmission to all devices on a LAN.
   - **Identification:** Uses a special destination address of all F's (FF:FF:FF:FF:FF:FF).
   - **Purpose:** Allows devices to discover and communicate with each other.

**Ethernet Frame Overview:**

- **Definition:** An Ethernet frame is a structured data packet used in Ethernet networks, ensuring data is transmitted correctly from one device to another.
  
- **Frame Structure:**
  1. **Preamble:** 
     - **Length:** 8 bytes (64 bits)
     - **Contents:** First 7 bytes are alternating ones and zeros; last byte is the Start Frame Delimiter (SFD), signaling the start of the frame contents.
  
  2. **Destination MAC Address:** 
     - **Length:** 6 bytes
     - **Purpose:** Identifies the intended recipient of the frame.
  
  3. **Source MAC Address:** 
     - **Length:** 6 bytes
     - **Purpose:** Identifies the sender of the frame.
  
  4. **Ether-Type Field:**
     - **Length:** 2 bytes (16 bits)
     - **Purpose:** Indicates the protocol of the frame's payload (can also be a VLAN header if VLAN tagging is used).
  
  5. **Data Payload:**
     - **Length:** 46 to 1500 bytes
     - **Contents:** Contains the actual data from higher layers (IP, transport, application).
  
  6. **Frame Check Sequence (FCS):**
     - **Length:** 4 bytes (32 bits)
     - **Purpose:** Contains a checksum value generated by a Cyclic Redundancy Check (CRC) to verify data integrity. The receiving end performs its CRC check to ensure no corruption occurred during transmission.

**Key Points:**
- **VLANs:** Allow multiple logical LANs on the same physical network, useful for traffic segregation.
- **CRC:** A mathematical method used to detect errors in the transmitted data. If discrepancies are found, the data is discarded, and higher-layer protocols handle retransmission.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-05%20at%2011.44.22.png">
</p>
