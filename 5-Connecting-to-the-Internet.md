# 5 Connecting to the Internet

## 5.1 POTS and Dial-up

The evolution of computer networks in the 20th century began with simple local connections and evolved into complex, long-distance data exchanges. Initially, networking technologies were limited to close physical proximity, but the need for long-distance data sharing spurred innovation. A key development was the use of the **Public Switched Telephone Network (PSTN)**, or **Plain Old Telephone Service (POTS)**, to transmit data over long distances.

**Origins of Long-Distance Networking**

- In the late 1970s, two graduate students at Duke University realized that the **PSTN**, originally designed for voice communication, could also connect computers and share data.
- Though the phone system was intended for voice transmission, this discovery led to the creation of **Usenet**, a precursor to dial-up networks.

**Dial-Up Connections**

- A **dial-up connection** is established via POTS and involves dialing a phone number to connect two computers.
- It enabled institutions like universities to share data through simple messages.
- **Modems** are used to:
  - **Modulate** (convert) digital data into sound waves for transmission over phone lines.
  - **Demodulate** these sound waves back into digital data on the receiving end.
  
- **Modem** stands for **modulator-demodulator** and allows digital data transmission over phone lines. 
- This process is similar to **line coding** in Ethernet cables, which converts binary data into electrical signals.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-09-28%20at%2015.50.10.png" height="300">
</p>

**Baud Rate**

- **Baud rate** measures how many bits can be transmitted per second (bps) over a phone line.
  - Early modems (1950s): **110 bps**.
  - By the 1970s (Usenet): **300 bps**.
  - 1990s (rise of dial-up internet): **14.4 kbps (kilobits per second)** and beyond.
  
- While dial-up speeds improved over time, they never matched modern broadband speeds.

**The Decline of Dial-Up and Rise of Broadband**

- Dial-up internet, popular in the 1990s and early 2000s, was eventually replaced by **broadband** technologies.
- **Broadband** offers an **always-on** connection, removing the need to choose between phone and internet use.
- Dial-up is still used in some rural areas due to limited broadband infrastructure.

## 5.2 Broadband Connections

**Broadband** refers to any non-dial-up internet technology, offering much faster speeds and **always-on** connectivity. Unlike dial-up, broadband connections are permanent and don't require reconnection with each use.

**Impact of Broadband**

- Broadband enabled the internet to reach its full potential for both businesses and home users.
- It allowed for faster data transfer, making activities like streaming and large file sharing possible.

**Early Adoption by Businesses**

- Businesses adopted broadband before home users, driven by the need for higher bandwidth.
- **T-carrier technologies** were commonly used, allowing businesses to transfer data faster than dial-up could handle.

**Transition to Home Use**

- As the internet evolved, home users required faster connections for increasingly complex content (e.g., images, videos).
- For instance, downloading a modern smartphone image (2MB) would take **~20 minutes** on a dial-up connection.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-09-28%20at%2016.17.52.png" height="300">
</p>

- Without broadband, the modern internet experience—such as streaming music or movies, sharing photos, or taking online courses—wouldn’t exist.

**T-Carrier Technologies**

**T-carrier technologies**, originally developed by AT&T, allowed multiple phone calls to travel across a single cable, starting with **Transmission System 1 (T1)**. This system was designed to transmit up to 24 simultaneous phone calls over twisted pair copper wires.
- This technology requires **dedicated lines**, making them more expensive, thus mainly used by businesses.

**Key Features of T1**

- **T1 specification**: Allowed up to 24 phone channels, each capable of transmitting at **64 kbps**, for a total throughput of **1.544 Mbps**.
- Over time, the term **T1** came to describe any twisted pair copper connection with speeds of 1.544 Mbps, even if it didn’t follow the original T1 specification.

**Adoption for Data Transfers**

- Originally, T1 was used only by telecom companies for interconnections.
- By the 1990s, businesses began using T1 lines for faster internet, taking advantage of its higher data transfer speeds.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-09-28%20at%2016.30.05.png" height="300">
</p>

**Improvements and Successors**

- **T3 lines**: Combined 28 T1 lines for a total throughput of **44.736 Mbps**.
- T-carrier technologies have been mostly replaced by cheaper and faster broadband options such as **cable broadband** and **fiber**.
- Today, **fiber technologies** have replaced older copper-based systems, especially for internal ISP communications.

**Digital Subscriber Line (DSL)**

The **public telephone network** was a natural choice for early internet connectivity since its infrastructure was already widespread. Over time, faster internet access was desired, and research showed that the twisted pair copper wires used by modern phone lines could carry more data than needed for voice calls. This led to the development of **Digital Subscriber Line (DSL)**, which operates at a frequency range that doesn't interfere with normal phone calls, allowing for **simultaneous voice and data transmission**.

- **DSL**: Enables higher data transmission compared to dial-up, utilizing existing phone lines.
- **DSLAM (Digital Subscriber Line Access Multiplexers)**: Special modems used in DSL connections that establish long-running data connections.
  
**Types of DSL**

- **1. ADSL (Asymmetric Digital Subscriber Line)**:
  - Provides different speeds for upload and download, typically with faster download speeds.
  - Ideal for home users who download more data (e.g., web browsing) than they upload.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-09-28%20at%2016.39.23.png" height="300">
</p>

- **2. SDSL (Symmetric Digital Subscriber Line)**:
  - Offers equal upload and download speeds.
  - Primarily used by businesses that host servers, but has become more common for home use.
  - Similar speed to a **T1 line** with a cap of **1.544 Mbps**.

- **3. HDSL (High Bit-rate Digital Subscriber Line)**:
  - An advancement of SDSL, offering speeds higher than **1.544 Mbps**.

**Cable Broadband**

The evolution of communication technologies has moved from wired to wireless, but the story of **television** follows the opposite trajectory. Initially, **television broadcasts** were wireless, sent out by large towers, and received by antennas in people's homes. This worked much like today’s cellular phone systems, where users need to be within range of a cell tower.

- **1940s**: Cable TV technologies emerged to provide TV access to remote areas outside the range of broadcast towers.
- **1984**: The **Cable Communications Policy Act** in the U.S. deregulated the cable industry, leading to a significant growth in cable television adoption.
- **1990s**: Cable infrastructure in the U.S. reached the same scale as the public telephone system.

**Transition to Cable Internet**
- Cable providers noticed that **coaxial cables**, originally used for TV, could carry more data than needed for TV transmission.
- By using **non-interfering frequencies**, cable internet access technologies were developed to offer **high-speed internet** via the same cables used for TV.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-09-28%20at%2016.47.00.png" height="300">
</p>

**Shared Bandwidth Technology**
- Cable broadband operates on a **shared bandwidth model**, meaning that multiple users share the same bandwidth until reaching the ISP's core network.
- Unlike **DSL** or **dial-up**, which connect directly to a **central office (CO)** and can guarantee bandwidth, cable internet speeds can fluctuate, especially during **peak usage times**.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-09-28%20at%2016.47.57.png" height="300">
</p>

- Cable internet connections use a **cable modem** to connect the consumer’s network to the **Cable Modem Termination System (CMTS)**.
- The CMTS then links multiple cable connections to the ISP's core network.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-09-28%20at%2016.49.05.png" height="300">
</p>

**Fiber Internet**

Fiber optic connections have been at the core of the Internet for a long time, primarily due to their ability to transmit data at higher speeds and over longer distances without signal degradation. Unlike copper cables, which use electrical signals, **fiber connections** use **light** for data transmission, allowing data to travel much farther before requiring a repeater.

**Advantages of Fiber**
- **Electrical signals** in copper cables degrade after a few thousand feet and need repeaters.
- **Fiber signals** can travel **many miles** without degradation, making them ideal for core networks.

**FTTX (Fiber to the X)**

FTTX is a term used to describe how close **fiber technologies** get to the end-user. There are various types of FTTX implementations:

1. **FTTN (Fiber to the Neighborhood)**:
   - Fiber is run to a central cabinet serving a neighborhood.
   - **Twisted pair copper** or **coaxial cables** are used for the remaining distance to homes.

2. **FTTB (Fiber to the Building/Business/Basement)**:
   - Fiber reaches an individual building or business.
   - **Copper cables** connect individual users inside the building.

3. **FTTH (Fiber to the Home)**:
   - Fiber is run directly to each **individual residence**.
   - FTTH and FTTB are sometimes referred to as **FTTP (Fiber to the Premises)**.

<p align="center">
  <img src="https://github.com/JavadZandiyeh/Coursera-The-Bits-and-Bytes-of-Computer-Networking/blob/main/images/Screenshot%202024-09-28%20at%2016.57.04.png" height="300">
</p>

**Optical Network Terminator (ONT)**

- Instead of using a modem, fiber networks use an **ONT** as the **demarcation point**.
- The ONT converts fiber network protocols into those that **traditional copper networks** can understand, enabling compatibility with existing home or office setups.

