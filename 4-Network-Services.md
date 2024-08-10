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
