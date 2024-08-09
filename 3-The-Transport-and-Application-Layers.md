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

## 3.2 The Application Layer
- **Application Layer**: This layer handles the communication between actual applications, allowing them to send and receive data.

- **Previous Layers Recap**:
  1. **Physical Layer**: Processes electrical or optical signals for communication across cables.
  2. **Data Link Layer**: Uses Ethernet to address and send data between individual computers.
  3. **Network Layer**: Uses IP to facilitate communication between different networks.
  4. **Transport Layer**: Ensures data is correctly sent and received by the appropriate applications.

- **Application Layer Protocols**:
  - The **data** sent at this layer is the entire content that applications exchange, such as web pages, streaming video, or documents.
  - Unlike lower layers with fewer protocols (e.g., Ethernet at the Data Link Layer, IP at the Network Layer, TCP/UDP at the Transport Layer), the Application Layer has a **wide variety** of protocols tailored to specific application types.

- **Web Traffic Example**:
  - **Web Browsers and Servers**: Despite the variety of web browsers (Chrome, Safari, etc.) and servers (Microsoft IIS, Apache, NGINX), they must all communicate using the **HTTP protocol** to ensure compatibility.
  - **Interoperability**: Regardless of the browser or server used, they must adhere to the same application layer protocol (e.g., HTTP for web traffic) to ensure they can communicate effectively.

- **Standardization**:
  - Application protocols like **FTP** work similarly, where all clients must communicate using the standardized FTP protocol, ensuring interoperability across different software options.

- **Network Layer Models**: Different models exist, with variations in how layers are grouped. The five-layer model we've used is common, but others, like the four-layer model, combine some layers.

- **OSI Model Overview**:
  - The **OSI (Open Systems Interconnection) model** is a seven-layer model and is the most rigorously defined, often used in academic settings and for network certifications.
  - The OSI model adds two additional layers between the **Transport Layer** and **Application Layer**: 
    1. **Session Layer (5th Layer)**: Manages communication between applications and the transport layer, handling the transfer of data from the application layer.
    2. **Presentation Layer (6th Layer)**: Ensures that data is in a usable format for applications, handling tasks like encryption and compression.

- **Comparison with the Five-Layer Model**:
  - The five-layer model combines the functions of the **Session** and **Presentation Layers** into the **Application Layer** for simplicity.
  - The five-layer model is seen as more practical for everyday networking tasks, while the seven-layer OSI model provides a more detailed and structured approach, especially useful in educational contexts.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-09%20at%2016.16.36.png" height="400">
</p>

**All the Networking Layers Working Unison:**

https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/All-the-Networking-Layers-Working-in-Unison.mp4

## 3.3 Glossary Terms

**ACK flag:** One of the TCP control flags. ACK is short for acknowledge. A value of one in this field means that the acknowledgment number field should be examined

**Acknowledgement number:** The number of the next expected segment in a TCP sequence

**Application layer:** The layer that allows network applications to communicate in a way they understand

**Application layer payload:** The entire contents of whatever data applications want to send to each other

**CLOSE:** A connection state that indicates that the connection has been fully terminated, and that no further communication is possible

**CLOSE_WAIT:** A connection state that indicates that the connection has been closed at the TCP layer, but that the application that opened the socket hasn't released its hold on the socket yet

**Connection-oriented protocol:** A data-transmission protocol that establishes a connection at the transport layer, and uses this to ensure that all data has been properly transmitted

**Connectionless protocol:** A data-transmission protocol that allows data to be exchanged without an established connection at the transport layer. The most common of these is known as UDP, or User Datagram Protocol

**Data offset field:** The number of the next expected segment in a TCP packet/datagram

**Demultiplexing:** Taking traffic that's all aimed at the same node and delivering it to the proper receiving service

**Destination port:** The port of the service the TCP packet is intended for

**ESTABLISHED:** Status indicating that the TCP connection is in working order, and both sides are free to send each other data

**FIN:** One of the TCP control flags. FIN is short for finish. When this flag is set to one, it means the transmitting computer doesn't have any more data to send and the connection can be closed

**FIN_WAIT:** A TCP socket state indicating that a FIN has been sent, but the corresponding ACK from the other end hasn't been received yet

**Firewall:** It is a device that blocks or allows traffic based on established rules

**FTP:** An older method used for transferring files from one computer to another, but you still see it in use today

**Handshake:** A way for two devices to ensure that they're speaking the same protocol and will be able to understand each other

**Instantiation:** The actual implementation of something defined elsewhere

**Listen:** It means that a TCP socket is ready and listening for incoming connections

**Multiplexing:** It means that nodes on the network have the ability to direct traffic toward many different receiving services

**Options field:** It is sometimes used for more complicated flow control protocols

**Port:** It is a 16-bit number that's used to direct traffic to specific services running on a networked computer

**Presentation layer:** It is responsible for making sure that the unencapsulated application layer data is actually able to be understood by the application in question

**PSH flag:** One of the TCP control flags. PSH is short for push. This flag means that the transmitting device wants the receiving device to push currently- buffered data to the application on the receiving end as soon as possible

**RST flag:** One of the TCP control flags. RST is short for reset. This flag means that one of the sides in a TCP connection hasn't been able to properly recover from a series of missing or malformed segments

**Sequence number:** A 32-bit number that's used to keep track of where in a sequence of TCP segments this one is expected to be

**Server or Service:** A program running on a computer waiting to be asked for data

**Session layer:** The network layer responsible for facilitating the communication between actual applications and the transport layer

**Socket:** The instantiation of an endpoint in a potential TCP connection

**Source port:** A high numbered port chosen from a special section of ports known as ephemeral ports

**SYN flag:** One of the TCP flags. SYN stands for synchronize. This flag is used when first establishing a TCP connection and make sure the receiving end knows to examine the sequence number field

**SYN_RECEIVED:** A TCP socket state that means that a socket previously in a listener state, has received a synchronization request and sent a SYN_ACK back

**SYN_SENT:** A TCP socket state that means that a synchronization request has been sent, but the connection hasn't been established yet

**TCP checksum:** A mechanism that makes sure that no data is lost or corrupted during a transfer

**TCP segment:** A payload section of an IP datagram made up of a TCP header and a data section

**TCP window:** The range of sequence numbers that might be sent before an acknowledgement is required

**URG flag:** One of the TCP control flags. URG is short for urgent. A value of one here indicates that the segment is considered urgent and that the urgent pointer field has more data about this

**Urgent pointer field:** A field used in conjunction with one of the TCP control flags to point out particular segments that might be more important than others
