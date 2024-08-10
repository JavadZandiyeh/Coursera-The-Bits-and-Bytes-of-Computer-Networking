# 4 Network Services
## 4.1 Name Resolution
DNS (Domain Name System) is a system that translates human-readable domain names into IP addresses that computers use to identify each other. This process is known as name resolution.

- **Binary Communication**: Computers communicate using binary (1s and 0s), but humans find it easier to work with words rather than numbers.

- **DNS Introduction**: The Domain Name System (DNS) translates human-friendly domain names (like www.weather.com) into IP addresses (like 184.29.131.121).

- **Convenience of DNS**: DNS makes it easier for humans to remember and access websites without needing to memorize complex IP addresses. It also allows organizations to update IP addresses without disrupting user access.

- **Geographical Considerations**: DNS can route users to different IP addresses based on their location, optimizing web performance by directing users to geographically closer servers.

For a computer to function on a network we need the following:
1. IP Address
2. Subnet Mask
3. Gateway for Host
4. DNS Server

**DNS Server Configuration**: For a computer to function on a network, it needs to have certain configurations, including a DNS server, which is crucial for translating domain names into IP addresses.

**Types of DNS Servers**:
1. **Caching Name Servers**: Store domain name lookups temporarily to speed up future requests.
2. **Recursive Name Servers**: Perform full DNS resolution by querying multiple servers to find the correct IP address.
3. **Root Name Servers**: The starting point in DNS resolution, directing queries to the appropriate Top-Level Domain (TLD) name server.
4. **TLD Name Servers**: Responsible for the last part of a domain name (e.g., ".com") and direct queries to the authoritative name server.
5. **Authoritative Name Servers**: Provide the actual IP address of the domain.

**Name Resolution Process**:
- When a user types a domain name (e.g., www.facebook.com), the local name server checks if it has the IP cached. If not, it performs a full recursive resolution by contacting a root name server, which directs it to the appropriate TLD name server. The TLD server then directs the query to the authoritative name server, which provides the IP address.

  - If IP was cached:

  <p align="center">
    <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-10%20at%2011.24.37.png" height="300">
  </p>

  - else if the full recursive resolution is required:
   
  <p align="center">
    <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-10%20at%2011.25.43.png" height="300">
  </p>

**Caching and TTL**: 
- DNS servers cache the results of lookups to avoid repeating the entire resolution process for every request. This cache is stored for a duration defined by the domain's Time to Live (TTL) value. 

**Anycast and Global Distribution**:
- Root and TLD servers are distributed globally using Anycast, which routes queries to the nearest or best-performing server.

**Importance of Hierarchy**:
- The hierarchical structure of DNS ensures stability and security, preventing malicious entities from redirecting traffic to unauthorized IP addresses.

**Local DNS Cache**:
- To further reduce DNS lookups, individual devices like phones and computers also maintain their own temporary DNS caches.

DNS (Domain Name System) typically uses UDP (User Datagram Protocol) instead of TCP (Transmission Control Protocol) for several key reasons. The primary difference between the two protocols is that UDP is connectionless, meaning it doesn't require the setup or teardown of a connection, which results in less traffic and lower overhead.

**Why DNS Uses UDP:**
- **Efficiency**: A DNS request and its response can usually fit within a single UDP datagram, making it an ideal choice for a protocol that doesn’t need the reliability and connection management of TCP.
- **Traffic Volume**: DNS can generate a lot of traffic, especially when performing full resolutions. Using UDP minimizes the number of packets required, reducing network load.

**DNS Resolution with TCP:**

If DNS used TCP, the process would involve a three-way handshake (SYN, SYN-ACK, ACK) before even sending the DNS request, followed by additional handshakes for every step in the resolution process. For example, resolving a domain like "food.com" via TCP could require at least 44 packets due to the overhead of connection management, ACKs, and connection teardown. This would be inefficient given that DNS is just the precursor to actual data transmission.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-10%20at%2011.30.29.png" height="300">
</p>

**DNS Resolution with UDP:**

In contrast, DNS using UDP only requires about eight packets for a full resolution, greatly reducing overhead. If the DNS request fails or doesn’t receive a response, the DNS resolver can simply send the request again, providing a basic form of error handling without the need for TCP’s extensive management features.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-10%20at%2011.32.40.png" height="300">
</p>

**DNS over TCP:**

Despite UDP's efficiency, DNS over TCP is used in situations where the response data is too large to fit in a single UDP datagram. In such cases, the server will prompt the client to switch to TCP for the resolution. This is increasingly common as the complexity of the web grows and responses become larger.

In summary, DNS primarily uses UDP for its efficiency and simplicity, but it can fall back on TCP when needed, especially for handling larger queries.

## 4.2 Name Resolution in Practice
Understanding DNS (Domain Name System) resource records is essential for troubleshooting networking issues, as they dictate how domain names are resolved to IP addresses or other useful data. Here's a breakdown of the most common and important DNS resource record types:

1. **A Record (Address Record)**
   - **Purpose**: Maps a domain name to an IPv4 address.
   - **Usage**: When a user enters a domain name, the DNS resolver queries the DNS server for the A record, which returns the associated IPv4 address. 
   - **Example**: If you look up "www.example.com", the A record might return "93.184.216.34".
   - **Multiple A Records**: A domain can have multiple A records, which can be used for load balancing via DNS round-robin. For instance, "www.microsoft.com" could resolve to multiple IP addresses (10.1.1.1, 10.1.1.2, etc.), distributing traffic among several servers.

2. **AAAA Record (Quad A Record)**
   - **Purpose**: Maps a domain name to an IPv6 address.
   - **Usage**: Similar to an A record, but it returns an IPv6 address instead of an IPv4 address, accommodating the newer addressing scheme.
   - **Example**: A lookup for "www.example.com" with an AAAA record might return "2606:2800:220:1:248:1893:25c8:1946".

3. **CNAME Record (Canonical Name Record)**
   - **Purpose**: Redirects one domain name to another domain name.
   - **Usage**: Allows for easier management of domain names by pointing multiple domain names to a single canonical domain name. This reduces the need to update multiple records if the IP address changes.
   - **Example**: "microsoft.com" could have a CNAME record that redirects to "www.microsoft.com", ensuring that both domain names resolve to the same site.

4. **MX Record (Mail Exchange Record)**
   - **Purpose**: Directs email to the appropriate mail server for a domain.
   - **Usage**: When an email is sent to someone@domain.com, the sending mail server queries the DNS for the MX record of "domain.com" to determine where to deliver the email.
   - **Example**: The MX record for "example.com" might point to "mail.example.com".

5. **SRV Record (Service Record)**
   - **Purpose**: Specifies the location of a specific service.
   - **Usage**: Used for defining the location (IP address and port) of servers for specific services, like VoIP or chat.
   - **Example**: An SRV record for a service like "ldap" could point to "ldap.example.com" with a specified port number.

6. **TXT Record (Text Record)**
   - **Purpose**: Holds free-form text, often used for various configuration purposes.
   - **Usage**: Initially intended for human-readable notes, TXT records are now commonly used for machine-readable data, like verifying domain ownership, SPF (Sender Policy Framework) records for email validation, and other service configurations.
   - **Example**: A TXT record for "example.com" might contain "v=spf1 include:_spf.example.com ~all" to define allowed email servers for SPF.

7. **NS Record (Name Server Record)**
   - **Purpose**: Specifies the authoritative DNS servers for a domain.
   - **Usage**: Determines which DNS servers are authoritative for a domain and should be queried for DNS resolution.
   - **Example**: The NS record for "example.com" might list "ns1.example.com" and "ns2.example.com" as the authoritative servers.

8. **SOA Record (Start of Authority Record)**
   - **Purpose**: Provides information about the domain, such as the primary name server and email of the domain administrator.
   - **Usage**: Contains administrative information about the zone, including the primary name server, contact email, and various timers related to zone transfers.
   - **Example**: The SOA record for "example.com" might specify "ns1.example.com" as the primary server and an email like "admin@example.com".

These records are the backbone of how DNS functions, directing traffic, emails, and services to the correct servers, and enabling the efficient operation of the internet.

Let's break down the structure of a domain name using the example `www.google.com`, which consists of three primary parts: the **Top-Level Domain (TLD)**, the **Second-Level Domain (SLD)**, and the **Subdomain**.

1. **Top-Level Domain (TLD)**
   - **Definition**: The TLD is the last part of a domain name, appearing after the final dot. In the example `www.google.com`, the TLD is `.com`.
   - **Purpose**: TLDs categorize domains into groups, often based on geographical location, purpose, or industry. Some common TLDs include `.com`, `.net`, `.org`, `.edu`, and country-specific TLDs like `.de` for Germany or `.cn` for China.
   - **Management**: TLDs are managed by the Internet Corporation for Assigned Names and Numbers (ICANN), which oversees the assignment and administration of these domains globally.

2. **Second-Level Domain (SLD)**
   - **Definition**: The SLD is the part of the domain name that comes immediately before the TLD. In `www.google.com`, the SLD is `google`.
   - **Purpose**: The SLD is typically the most identifiable part of the domain name and is chosen by the entity or individual registering the domain. It represents the main name of the website or service and is often tied to a brand or organization.
   - **Registration**: This is the part of the domain that users can register through a domain registrar. The combination of the SLD and TLD must be unique within the DNS.

3. **Subdomain**
   - **Definition**: The subdomain precedes the SLD and is separated from it by a dot. In `www.google.com`, the subdomain is `www`.
   - **Purpose**: Subdomains are used to organize or differentiate sections of a website. For instance, `www` is the most common subdomain and traditionally stands for "World Wide Web." However, subdomains can be customized for specific purposes, like `blog.google.com` or `mail.google.com`.
   - **Control**: Subdomains can be freely created by the owner of the domain without the need for registration through ICANN. They allow for flexibility in structuring a website.

**Fully Qualified Domain Name (FQDN)**
   - **Definition**: An FQDN includes the subdomain, the SLD, and the TLD, fully specifying the location of a domain within the DNS hierarchy. In our example, `www.google.com` is the FQDN.
   - **Purpose**: The FQDN provides a complete and unambiguous reference to a specific location on the internet. It’s how a specific website or service is accessed.
   - **Structure Limitations**:
     - **Levels**: DNS supports up to 127 levels of domains (subdomains included) for an FQDN.
     - **Character Limits**: Each section of the domain name can be up to 63 characters long, and the entire FQDN can have a maximum length of 255 characters.

**Domain Registration**
   - **Process**: To use a domain name, you must register it through a domain registrar. The registrar, which has an agreement with ICANN, ensures that the domain name is unique and not already in use.
   - **Subdomains**: After registering a domain (like `google.com`), the owner can create subdomains (like `www.google.com`) without additional registration.

**ICANN and IANA**
   - **ICANN**: The Internet Corporation for Assigned Names and Numbers is responsible for managing TLDs and overseeing the global DNS structure. It ensures the stability and security of the internet’s naming system.
   - **IANA**: The Internet Assigned Numbers Authority, a part of ICANN, specifically manages the allocation of IP addresses and other internet protocol resources.

**Example Scenarios**
   - **Simple Domain**: `example.com` - where `example` is the SLD and `.com` is the TLD.
   - **With Subdomain**: `blog.example.com` - where `blog` is the subdomain.
   - **Complex FQDN**: `mail.server.east.co.example.com` - where `mail`, `server`, `east`, and `co` are subdomains, `example` is the SLD, and `.com` is the TLD.

**Understanding DNS Zones and Their Importance:**

DNS zones play a crucial role in managing the Domain Name System (DNS), allowing for better organization, delegation, and management of domain records. Let’s break down the concept of DNS zones, their hierarchical structure, and how they interact with authoritative name servers.

1. **What is a DNS Zone?**
   - **Definition**: A DNS zone is a distinct portion of the DNS namespace that is managed separately. It contains the mappings between domain names and IP addresses, as well as other types of DNS records. 
   - **Purpose**: Zones allow for the administrative control and delegation of DNS records for different parts of a domain. This segmentation is essential for large organizations that need to manage numerous DNS records efficiently.

2. **Hierarchical Structure of DNS Zones**
   - **Root Zone**: At the top of the DNS hierarchy is the root zone, managed by root name servers. The root zone contains pointers to the authoritative name servers for all the top-level domains (TLDs) like `.com`, `.net`, etc.
   - **TLD Zone**: Below the root zone are the TLD zones, each responsible for a specific TLD. For example, the `.com` TLD zone is managed by a set of authoritative name servers that direct queries to the appropriate domain-level name servers.
   - **Domain-Level Zones**: These are the zones managed by organizations or individuals who have registered domain names (e.g., `google.com`). These zones contain resource records for subdomains, email servers, and other services associated with the domain.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/dns-hierarchy.gif" height="300">
</p>

3. **DNS Zone Delegation**
   - **Delegation of Authority**: DNS zones do not overlap. Authority is delegated from the root zone to the TLD zones, and from TLD zones to individual domain zones. For instance, the `.com` zone does not manage `google.com` directly; instead, it delegates this responsibility to the authoritative name servers for `google.com`.
   - **Subdomains and Subzones**: Organizations can create subdomains within their domain (e.g., `la.largecompany.com`) and manage them as separate zones. Each subzone can have its own set of resource records and be controlled by different authoritative name servers.

4. **Zone Files and Their Contents**
   - **Zone Files**: These are text files that contain all the DNS records for a particular zone. The primary purpose of a zone file is to map domain names to IP addresses and define other important information about the zone.
   - **Start of Authority (SOA) Record**: Each zone file begins with an SOA record, which contains information about the zone, such as the primary name server, the administrator’s email, and the serial number of the zone file.
   - **Name Server (NS) Records**: These records indicate the name servers responsible for the zone. Multiple NS records are common to ensure redundancy and availability.
   - **Other Records**: Zone files include A records (for IPv4 addresses), AAAA records (for IPv6 addresses), CNAME records (aliases), MX records (mail servers), and TXT records (miscellaneous text information).

5. **Reverse Lookup Zones**
   - **Purpose**: Reverse lookup zones allow DNS resolvers to query an IP address to find the associated domain name (the reverse of a typical DNS lookup).
   - **PTR Records**: Reverse lookup zones primarily use PTR (Pointer) records, which map IP addresses back to domain names.
   - **Structure**: The structure of reverse lookup zones mirrors that of forward zones, but they are organized by IP addresses rather than domain names. For example, a reverse lookup for the IP `192.0.2.1` would use the PTR record in the reverse lookup zone file corresponding to the `192.0.2.x` range.

6. **Managing DNS Zones in Practice**
   - **Scalability**: By dividing a domain into multiple zones, large organizations can manage their DNS records more effectively. Each office or department can control its own zone, reducing the complexity of managing a single, massive zone file.
   - **Redundancy**: Using multiple authoritative name servers for each zone ensures that DNS queries can still be resolved even if one server fails.
   - **Updates and Maintenance**: Changes to DNS records are made in the zone files. The SOA record’s serial number is updated with each change, signaling other name servers to update their cached records.

**Example: LargeCompany.com**
   - **Scenario**: Imagine a company named LargeCompany with offices in Los Angeles, Paris, and Shanghai. Each office has its own DNS zone (`la.largecompany.com`, `pa.largecompany.com`, and `sh.largecompany.com`), and each is managed by its own authoritative name server.
   - **Benefits**: This setup allows each office to manage its own DNS records (e.g., `johns-pc.la.largecompany.com`) without interfering with the other offices. It also simplifies troubleshooting and updates since each zone is independent.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-10%20at%2015.01.48.png" height="300">
</p>

## 4.3 Dynamic Host Configuration Protocol
**Understanding DHCP and Its Importance in Network Management:**

Dynamic Host Configuration Protocol (DHCP) simplifies the process of configuring network settings for devices on a TCP/IP network.

1. **The Need for DHCP**
   - **Manual Configuration Challenges**: Without DHCP, network administrators would need to manually configure the IP address, subnet mask, gateway, and DNS server for each device. While the subnet mask, gateway, and DNS server are usually the same for all devices on a network, each device requires a unique IP address.
   - **Administrative Overhead**: Manually assigning IP addresses to hundreds or thousands of devices is time-consuming, prone to errors, and difficult to manage. DHCP automates this process, significantly reducing administrative overhead.

2. **What is DHCP?**
   - **Definition**: DHCP is an application layer protocol that automatically assigns IP addresses and other network configuration details to devices (hosts) on a network. When a device connects to a network, it sends a request to the DHCP server, which responds with the necessary configuration.
   - **Core Functions**: DHCP assigns IP addresses, subnet masks, default gateways, and DNS server addresses to devices on the network. It can also configure other settings like Network Time Protocol (NTP) servers.

3. **How DHCP Works**
   - **DHCP Process**: The DHCP process involves four main steps:
     1. **DHCP Discover**: When a device connects to the network, it broadcasts a DHCP Discover message to find available DHCP servers.
     2. **DHCP Offer**: The DHCP server responds with a DHCP Offer, proposing an IP address and other network settings.
     3. **DHCP Request**: The device accepts the offer by sending a DHCP Request message, indicating it wants to use the provided IP address.
     4. **DHCP Acknowledgement**: The DHCP server finalizes the process by sending a DHCP Acknowledgement, confirming that the device can use the IP address.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/dhcp-diag.epsi.gif" height="600">
</p>

4. **DHCP Allocation Methods**
   - **Dynamic Allocation**:
     - **Overview**: The most common method where the DHCP server assigns an IP address from a pool of available addresses. Each time a device requests an IP address, it might receive a different one.
     - **Use Case**: Ideal for client devices like desktops, laptops, and mobile devices, where the specific IP address is not critical.
   - **Automatic Allocation**:
     - **Overview**: Similar to dynamic allocation, but the DHCP server tries to assign the same IP address to the same device each time it connects, based on the device’s MAC address.
     - **Use Case**: Useful when it’s beneficial for a device to maintain the same IP address, without requiring manual configuration.
   - **Fixed Allocation** (Static DHCP):
     - **Overview**: The DHCP server assigns a specific IP address to a device based on its MAC address, as configured in a table. If the MAC address isn’t listed, the server may assign an IP dynamically or deny the request.
     - **Use Case**: Commonly used for devices that need a fixed IP, such as servers, printers, or network infrastructure devices.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-10%20at%2015.14.18.png" height="300">
</p>

5. **Additional DHCP Capabilities**
   - **Beyond Basic Configuration**: DHCP can also configure additional parameters such as:
     - **NTP Servers**: Ensures all devices on the network have synchronized time, which is crucial for logging, security, and network operations.
     - **Boot Parameters**: For devices that need to boot over the network, such as diskless workstations or thin clients.
     - **Custom Options**: Network administrators can define custom DHCP options to distribute other settings as needed.

6. **Security Considerations with DHCP**
   - **IP Address Management**: DHCP helps prevent IP conflicts and ensures efficient use of IP address space by dynamically managing IP assignments.
   - **Access Control**: In fixed allocation mode, DHCP can be used as a security measure, ensuring only devices with recognized MAC addresses can obtain an IP address and access the network.

7. **DHCP’s Role in Troubleshooting**
   - **Common Issues**: Problems like IP conflicts, devices failing to obtain an IP address, or incorrect network configurations often involve DHCP. Understanding DHCP helps IT support specialists diagnose and resolve these issues quickly.
   - **Network Health**: Monitoring DHCP logs and IP address allocation can provide insights into network health and help prevent problems before they impact users.

**In-Depth Look at DHCP Discovery and Configuration:**

Dynamic Host Configuration Protocol (DHCP) operates at the application layer, but it relies heavily on underlying network protocols to function effectively. Here’s a deep dive into how DHCP works, focusing on the DHCP discovery process, encapsulation, and communication without initial network layer configuration.

**DHCP Discovery Process**

The DHCP discovery process involves four key steps, each leveraging different network layers to achieve network configuration:

1. **DHCP Discover**
   - **Objective**: A device (DHCP client) needs to find a DHCP server to obtain network configuration.
   - **Message Details**: The client sends a DHCP Discover message to locate DHCP servers on the network.
   - **Broadcast Mechanism**: Since the client lacks an IP address and does not know the server's IP, it uses a broadcast message.
   - **Encapsulation**:
     - **UDP Datagram**: The DHCP Discover message is sent from UDP port 68 (client) to UDP port 67 (server). 
     - **IP Datagram**: Encapsulated in an IP datagram with a destination IP of `255.255.255.255` (broadcast) and a source IP of `0.0.0.0` (unknown).
     - **Broadcast Nature**: This ensures that every node on the local network receives the message, including any available DHCP servers.

2. **DHCP Offer**
   - **Objective**: The DHCP server offers an IP address and configuration details to the client.
   - **Response Details**: The server replies with a DHCP Offer message.
   - **Broadcast Mechanism**: The DHCP Offer is sent to the broadcast IP `255.255.255.255` with the source IP being the server’s IP.
   - **Encapsulation**:
     - **UDP Datagram**: The DHCP Offer message is sent from UDP port 67 (server) to UDP port 68 (client).
     - **Identification**: The offer includes the MAC address of the client, allowing the client to identify that the message is for it.

3. **DHCP Request**
   - **Objective**: The client requests to use the IP address offered by the server.
   - **Message Details**: The client sends a DHCP Request message to indicate acceptance of the offer.
   - **Broadcast Mechanism**: Sent from IP `0.0.0.0` to the broadcast IP `255.255.255.255`.
   - **Encapsulation**:
     - **UDP Datagram**: The request is from UDP port 68 (client) to UDP port 67 (server).
     - **Server Acknowledgment**: This message helps the server confirm the client’s intention to use the offered IP address.

4. **DHCP Acknowledgement (DHCPACK)**
   - **Objective**: The server confirms the IP address assignment and provides the final configuration details.
   - **Message Details**: The server sends a DHCPACK message to acknowledge the request.
   - **Broadcast Mechanism**: Sent to the broadcast IP `255.255.255.255` with the source IP of the server.
   - **Encapsulation**:
     - **UDP Datagram**: Sent from UDP port 67 (server) to UDP port 68 (client).
     - **Client Confirmation**: The client recognizes this message as it contains its MAC address, completing the configuration process.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/dhcp-heirarchy.jpeg" height="600">
</p>

**Key Concepts and Configuration Details**

- **IP and MAC Address Communication**: DHCP operates without an initial IP configuration on the client, relying on MAC addresses and broadcasts for communication.
- **Lease Time**: The IP address assigned by DHCP comes with a lease time. The client must renew its lease before it expires or request a new IP address by repeating the discovery process.
- **Release of IP**: When a client disconnects from the network, it can send a DHCP Release message to return the IP address to the DHCP server’s pool of available addresses.

**DHCP and Network Layer Configuration**

- **Without Initial IP**: DHCP clients use broadcast communication (`255.255.255.255`) and their MAC addresses to discover and interact with DHCP servers, effectively operating without initial IP layer configuration.
- **UDP and IP Dependencies**: DHCP uses UDP as its transport protocol due to its connectionless nature, suitable for broadcasting and the quick exchange of configuration information.

**Encapsulation Recap**

- **UDP Datagram**:
  - **Source Port**: 68 (client) / 67 (server)
  - **Destination Port**: 67 (server) / 68 (client)
- **IP Datagram**:
  - **Source IP**: `0.0.0.0` (client) / Server's IP
  - **Destination IP**: `255.255.255.255` (broadcast)
