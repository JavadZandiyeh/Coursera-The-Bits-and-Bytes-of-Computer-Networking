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
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-10%20at%2011.30.29.png" height="400">
</p>

**DNS Resolution with UDP:**

In contrast, DNS using UDP only requires about eight packets for a full resolution, greatly reducing overhead. If the DNS request fails or doesn’t receive a response, the DNS resolver can simply send the request again, providing a basic form of error handling without the need for TCP’s extensive management features.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-08-10%20at%2011.32.40.png" height="400">
</p>

**DNS over TCP:**

Despite UDP's efficiency, DNS over TCP is used in situations where the response data is too large to fit in a single UDP datagram. In such cases, the server will prompt the client to switch to TCP for the resolution. This is increasingly common as the complexity of the web grows and responses become larger.

In summary, DNS primarily uses UDP for its efficiency and simplicity, but it can fall back on TCP when needed, especially for handling larger queries.
