# 3 The Transport and Application Layers
## 3.1 The Transport Layer
**Introduction:**

- **Key Functions**:
  - **Multiplexing**: Directs traffic from multiple services to the correct receiving service on a network.
  - **Demultiplexing**: Receives traffic aimed at a node and directs it to the proper service.
  - **Connection Management**: Establishes long-running connections.
  - **Data Integrity**: Ensures data accuracy via error checking and verification.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-09%20at%2015.35.30.png" height="200">
</p>

- **Ports**:
  - **Definition**: A 16-bit number used to route traffic to specific services on a networked computer.
  - **Examples**:
    - **HTTP (Web Traffic)**: Typically uses port 80.
    - **FTP (File Transfer Protocol)**: Typically uses port 21.
  - **Socket Address**: Combines an IP address with a port (e.g., `10.1.1.100:80`).

- **Practical Application**:
  - **IT Support**: A single server might host various services (e.g., web, mail, file, print) using different ports.

- **Learning Outcomes**:
  - Understanding **multiplexing and demultiplexing**.
  - Identifying differences between **TCP** and **UDP**.
  - Explaining the **three-way handshake** in TCP connections.
  - Understanding how **TCP flags** are used.
  - Basics of **firewall** operations.

**TCP Segment Dissection:**

- **Overview**:
  - TCP segments are essential for managing data transmission in networks.
  - TCP establishes reliable connections for sending long chains of data segments.
  - A TCP segment consists of a **TCP header** and a **data section** (payload).
  - **Contrast with IP and Ethernet**: While IP and Ethernet send individual packets, TCP focuses on continuous data transfer.

- **Key Fields in TCP Header**:
  1. **Source Port**: High-numbered ephemeral port to distinguish outgoing connections.
  2. **Destination Port**: Port for the intended service (e.g., web server on port 80).
  3. **Sequence Number**: 32-bit number tracking the order of TCP segments.
  4. **Acknowledgment Number**: Indicates the next expected segment.
  5. **Data Offset**: 4-bit number specifying the length of the TCP header.
  6. **TCP Control Flags**: 6 bits reserved for controlling the state of the connection.
  7. **TCP Window**: 16-bit number defining the range of sequence numbers that can be sent before needing an acknowledgment.
  8. **Checksum**: 16-bit number used to verify data integrity.
  9. **Urgent Pointer**: Used with a TCP flag to highlight important segments (rarely used today).
  10. **Options Field**: Used for advanced flow control (also rarely used).
  11. **Padding**: Ensures the data payload begins at the correct location.
  
- **Flow Control**: TCP's reliance on sequence numbers, acknowledgments, and checksums ensures reliable data transmission.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-09%20at%2002.04.47.png" height="400">
</p>

**TCP Protocol and Control Flags:**
- **TCP Control Flags**:
  1. **URG (Urgent)**: Indicates that the segment is urgent (rarely used).
  2. **ACK (Acknowledgment)**: Confirms receipt of data; used in most segments.
  3. **PSH (Push)**: The transmitting device wants the receiving device to push currently-buffered data to the application on the receiving end as soon as possible.
  4. **RST (Reset)**: Resets the connection due to errors or lost segments.
  5. **SYN (Synchronize)**: Used to initiate a connection and synchronize sequence numbers.
  6. **FIN (Finish)**: Indicates that the sender has finished sending data and wants to close the connection.

- **TCP Connection Establishment**:
  - **Three-Way Handshake**:
    1. **SYN**: Computer A sends a SYN segment to start the connection.
    2. **SYN/ACK**: Computer B responds with SYN and ACK to acknowledge and agree.
    3. **ACK**: Computer A sends an ACK to confirm, establishing the connection.
  - **Full Duplex Mode**: After the handshake, both computers can send and receive data simultaneously, with each segment acknowledged by the other side.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-09%20at%2002.17.31.png" height="200">
</p>

- **TCP Connection Termination**:
  - **Four-Way Handshake**:
    1. **FIN**: One computer signals the end of data transmission.
    2. **ACK**: The other computer acknowledges the FIN.
    3. **FIN**: The second computer also signals the end.
    4. **ACK**: The first computer acknowledges, closing the connection.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-09%20at%2002.16.09.png" height="200">
</p>

**TCP Socket Overview:**

- **What is a Socket?**:
  - A **socket** is the actual implementation of an endpoint in a TCP connection, created by a running program.
  - **Ports** are virtual descriptors, while sockets are active entities that respond when traffic is directed to a specific port.

- **Common TCP Socket States**:
  1. **LISTEN**: Socket is ready and waiting for incoming connections (server side only).
  2. **SYN_SENT**: A synchronization request has been sent, awaiting connection establishment (client side only).
  3. **SYN_RECEIVED**: Socket has received a SYN request and sent a SYN/ACK back, waiting for final ACK (server side only).
  4. **ESTABLISHED**: Connection is fully operational, and both sides can send/receive data.
  5. **FIN_WAIT**: FIN has been sent, but ACK hasn't been received yet.
  6. **CLOSE_WAIT**: Connection closed at the TCP layer, but the application hasn’t released the socket yet.
  7. **CLOSED**: Connection is fully terminated; no further communication possible.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/tcp_ladder_states.png" height="400">
</p>

- **Variability**:
  - Socket states and their names can vary across operating systems, unlike the universal TCP protocol. 
  - Check specific socket state definitions for the operating system you're working with during troubleshooting.

**TCP vs. UDP (Connection-Oriented vs. Connectionless Protocols):**

- **TCP (Connection-Oriented Protocol)**:
  - **Reliability**: Establishes a connection, ensures all data is transmitted correctly, and acknowledges each segment.
  - **Importance**: Vital for reliable communication, especially when data integrity is crucial, as the internet is prone to issues like congestion or errors.
  - **Mechanisms**:
    - **Acknowledgments**: Ensures data is received and retransmits if necessary.
    - **Sequence Numbers**: Keeps data in order, even if segments arrive out of sequence.
  - **Overhead**: Requires extra traffic for establishing, maintaining, and closing connections, which can be significant.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-09%20at%2015.09.31.png" height="400">
</p>

- **UDP (Connectionless Protocol)**:
  - **Speed**: Does not establish connections or send acknowledgments, making it faster with less overhead.
  - **Use Case**: Ideal for situations where speed is prioritized over reliability, like streaming video, where occasional data loss (e.g., a few video frames) is acceptable.
  - **Efficiency**: Saves bandwidth by eliminating the extra steps required by TCP, allowing for potentially higher data quality.

- **Comparison**:
  - **TCP** is necessary when data must arrive intact and in order, despite the higher overhead.
  - **UDP** is useful when speed and efficiency are more critical than perfect data transmission.

**TCP Ports and Sockets Summary:**

- **Ports in TCP/IP**: Used at the Transport Layer to establish connections and deliver data. A TCP "segment" activates ports for specific services, turning these ports into "sockets" that are ready to send and receive data.

- **Categories of Ports**:
  - **System Ports (1-1023)**: Reserved for common applications like FTP and Telnet.
  - **User Ports (1024-49151)**: Registered by vendors for specific server applications.
  - **Ephemeral Ports (49152-65535)**: Temporary ports used by clients for private data transfers.

- **Data Integrity in TCP**: TCP ensures data integrity through acknowledgments and checksum verification, confirming that received data matches what was sent.

- **Port Security**: Ports can be entry points for malware. Using firewalls and securing ports is essential to protect against malicious activities.

- **Firewalls** are devices or programs designed to block or allow network traffic based on specific criteria, playing a crucial role in network security.
  
- **Layer Operation**: Firewalls can operate at various layers of the network, including:
  1. **Application Layer**: Inspecting application-specific traffic.
  2. **Transport Layer**: Commonly used to block or allow traffic to specific ports.
  3. **IP Layer**: Blocking ranges of IP addresses.

- **Transport Layer Firewalls**:
  - These firewalls often control traffic by allowing access to certain ports and blocking others.
  - Example: In a small business, a firewall might allow traffic on port 80 for a web server while blocking access to other ports hosting confidential data.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-09%20at%2015.23.34.png" height="400">
</p>

- **Placement and Integration**:
  - Firewalls can be standalone devices, but they are often integrated with routers or even implemented as software on individual hosts.
  - All major operating systems come with built-in firewall capabilities, allowing traffic control at the host level.
