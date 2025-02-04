**Understanding IP Addressing and Network Classes**

### **Public and Private IP Addresses**

- **Public IP Address:** A public IP address is globally unique and assigned to a device for communication over the internet. It is provided by an **Internet Service Provider (ISP)** and can be accessed from anywhere in the world.
- **Private IP Address:** A private IP address is used within an internal network and is unique only within that specific network. It cannot be accessed directly over the internet and does not incur costs when used for internal communication.

### **IPv4 vs. IPv6**

- **IPv4:** Uses a 32-bit address space, supporting approximately **4.3 billion** unique addresses (2^32).
- **IPv6:** Uses a 128-bit address space, significantly expanding the number of possible addresses to **340 undecillion (2^128)**, ensuring long-term scalability for the internet.

### **Checking IP Addresses on Different Operating Systems**

To retrieve the private IP address of a device:
- **Windows:** Run `ipconfig /all` in the Command Prompt.
- **Linux/macOS:** Use `ifconfig` or `ip addr` in the terminal.

To determine the public IP of a network, visit websites such as:
- [https://whatismyipaddress.com/](https://whatismyipaddress.com/)
- [https://www.whatismyip.com/](https://www.whatismyip.com/)
- [https://iplocation.io/](https://iplocation.io/)

### **IPv4 Address Classes and Their Ranges**

IPv4 addresses are divided into five classes based on their leading bits and intended use:

| **Class** | **Address Range**         | **Network Bits** | **Host Bits** | **Usage**               |
|----------|--------------------------|----------------|--------------|----------------------|
| **A**    | 0.0.0.0 - 126.255.255.255 | N.H.H.H        | 16 million   | Large networks       |
| **B**    | 128.0.0.0 - 191.255.255.255 | N.N.H.H        | 65,000       | Medium-sized networks |
| **C**    | 192.0.0.0 - 223.255.255.255 | N.N.N.H        | 256          | Small networks       |
| **D**    | 224.0.0.0 - 239.255.255.255 | Multicast      | N/A          | Broadcasting/multicasting |
| **E**    | 240.0.0.0 - 255.255.255.255 | Reserved       | N/A          | Research and development |

- **Loopback Address:** The IP range **127.0.0.0/8** is reserved for loopback testing, with `127.0.0.1` commonly used to refer to the local system.

### **Private IP Address Ranges (RFC 1918)**

| **Class** | **Private IP Address Range**          |
|----------|--------------------------------------|
| **A**    | 10.0.0.0 - 10.255.255.255           |
| **B**    | 172.16.0.0 - 172.31.255.255         |
| **C**    | 192.168.0.0 - 192.168.255.255       |

Private IPs are used for internal communication within organizations, reducing the number of required public IPs and enhancing security.

### **Understanding Network and Host Segmentation**

IP addresses consist of two parts:
- **Network ID (N):** Identifies the network segment.
- **Host ID (H):** Identifies a specific device within the network.

The division of network and host portions depends on the class:
- **Class A:** N.H.H.H → Supports **127 networks**, each with **16 million hosts**.
- **Class B:** N.N.H.H → Supports **16,000 networks**, each with **65,000 hosts**.
- **Class C:** N.N.N.H → Supports **2 million networks**, each with **256 hosts**.

### **Subnetting and CIDR Notation**

- **Subnetting:** The process of dividing a larger network into smaller subnetworks to enhance performance and security.
- **CIDR (Classless Inter-Domain Routing):** Uses notation like `192.168.1.0/24` where `/24` indicates that the first 24 bits represent the network portion, leaving the remaining 8 bits for host addresses.

### **Internet Service Providers (ISP)**

ISPs allocate public IP addresses to customers for internet access. Some ISPs provide **dynamic IPs** (changing periodically) while others offer **static IPs** (fixed public IPs for business applications).

### **Example IP Allocation in a Private Network**

Consider a network using **Class C** addressing:
- **Network:** `192.168.0.0/24`
- **Usable IPs:** `192.168.0.1` to `192.168.0.254`
- **Broadcast Address:** `192.168.0.255` (used for network-wide communication)

In a home or office network, devices would be assigned private IPs such as:
- `192.168.0.1` → Router
- `192.168.0.2` → Laptop
- `192.168.0.3` → Printer
- `192.168.0.4` → Smartphone

---

### **IP Addressing in Traditional Networks vs. AWS Networking**  

In any network, certain IP addresses are reserved and cannot be assigned to hosts. These include:  
- **Network ID (First IP)** – Identifies the network itself.  
- **Broadcast Address (Last IP)** – Used for sending messages to all devices in the network.  

However, AWS further reserves additional IPs within each subnet for internal services, making a total of **five reserved IPs**:  
1. **Network ID (First IP)** – Identifies the subnet.  
2. **Broadcast IP (Last IP)** – Not used in AWS but still reserved.  
3. **AWS DNS Server** – The second IP address in the subnet.  
4. **AWS Reserved IP for Future Use** – Reserved by AWS for internal purposes.  
5. **AWS VPC Router** – The third IP address in the subnet for routing traffic within the VPC.  

### **Subnetting and IP Calculation in AWS**  

Subnetting allows breaking a large network into smaller subnetworks. AWS follows CIDR (Classless Inter-Domain Routing) notation for subnet creation.  

For a given CIDR block, the number of available IP addresses is calculated using:  
\[
\text{Total IPs} = 2^{(32 - \text{subnet mask})}
\]
Since AWS reserves 5 IP addresses per subnet, the usable IPs are:  
\[
\text{Usable IPs} = 2^{(32 - \text{subnet mask})} - 5
\]

#### **Subnet Size Ranges in AWS**  
AWS enforces a **minimum subnet size of /28** and a **maximum subnet size of /16**.  

| **Subnet Mask** | **Total IPs** | **Usable IPs (AWS)** |
|---------------|------------|----------------|
| **/32** | 1 | Not usable for subnets |
| **/31** | 2 | Not usable for subnets |
| **/30** | 4 | Not usable for subnets |
| **/29** | 8 | 3 |
| **/28** (Minimum in AWS) | 16 | 11 |
| **/27** | 32 | 27 |
| **/26** | 64 | 59 |
| **/25** | 128 | 123 |
| **/24** | 256 | 251 |
| **/20** | 4096 | 4091 |
| **/16** (Maximum in AWS) | 65536 | 65531 |

### **Example Calculation**  

For a **/24 subnet**:  
- **Total IPs**: \( 2^{(32 - 24)} = 256 \)  
- **Usable IPs**: \( 256 - 5 = 251 \)  

For a **/28 subnet** (smallest allowed by AWS):  
- **Total IPs**: \( 2^{(32 - 28)} = 16 \)  
- **Usable IPs**: \( 16 - 5 = 11 \)  

For a **/16 subnet** (largest allowed by AWS):  
- **Total IPs**: \( 2^{(32 - 16)} = 65536 \)  
- **Usable IPs**: \( 65536 - 5 = 65531 \)  

---

### VPC Pre-Checks and Design Considerations

#### 1. Overview of VPC
- **Virtual Private Cloud (VPC)** is an isolated, region-specific virtual network in AWS. It allows you to launch AWS resources in a virtual network that you define.
- VPCs provide complete control over your network configuration, including selection of IP address ranges, creation of subnets, configuration of route tables, and network gateways.

#### 2. CIDR Block and IP Planning
- **CIDR (Classless Inter-Domain Routing):**  
  This notation defines the size of the IP address space for your VPC. The CIDR block you select determines how many IP addresses are available within the VPC.
  
- **Determining the Size of Your VPC:**  
  Consider how many instances and resources you plan to launch. For example, a VPC CIDR of `192.168.0.0/22` provides:
  - Calculation: 32 – 22 = 10 bits for host addresses, which means 2^10 = 1024 IP addresses.
  - This size is appropriate if you need approximately 1000 IP addresses.

#### 3. Subnet Planning within the VPC
- **Public Subnets:**  
  These are subnets that are directly connected to the internet. They are typically used for resources such as Elastic Load Balancers (ELBs) and bastion (jump) hosts.
  
- **Private Subnets:**  
  These subnets are not directly accessible from the internet and are used for application servers, databases, and other backend resources.
  
- **Example Subnet Allocation:**  
  With a VPC CIDR of `192.168.0.0/22`, you might plan as follows:
  - **Public Subnets (2 required):**
    - Public Subnet in Availability Zone (AZ) ap-south-1a: `192.168.0.0/26`
    - Public Subnet in AZ ap-south-1b: `192.168.0.64/26`
  - **Private Subnets (2 required):**
    - Private Subnet in AZ ap-south-1a: `192.168.0.128/25`
    - Private Subnet in AZ ap-south-1b: `192.168.1.0/25`
  
- **Future Expansion:**  
  It is recommended to reserve additional IP space within your VPC for future subnets. For example, you might reserve:
  - `192.168.1.128/25`
  - `192.168.2.0/25`
  - `192.168.2.128/25`
  - `192.168.3.0/24`
  
  This planning allows flexibility for future resource growth or additional subnet creation.

#### 4. Example VPC and Subnet Layout
- **VPC CIDR:** `192.168.0.0/22` (1024 IP addresses)
  
- **Subnet Allocation:**
  - **Public Subnets:**  
    - Public Subnet 1 (ap-south-1a): `192.168.0.0/26`  
    - Public Subnet 2 (ap-south-1b): `192.168.0.64/26`
  - **Private Subnets:**  
    - Private Subnet 1 (ap-south-1a): `192.168.0.128/25`  
    - Private Subnet 2 (ap-south-1b): `192.168.1.0/25`
  - **Reserved for Future Use:**  
    - Additional subnets as needed, using the remaining IP space from the VPC CIDR block.

- **Application Segmentation:**
  - **Web/Public Layer:**  
    Place one public subnet in each AZ to host the ELB and bastion hosts.
  - **Application Layer:**  
    Allocate two subnets (one per AZ) for application servers.
  - **Database Layer:**  
    Allocate two subnets (one per AZ) for database servers.
  - **Lambda and Other Services:**  
    Consider additional subnets for services that require isolated network segments.

#### 5. Additional Considerations
- **Subnet Sizing:**  
  - AWS supports a minimum subnet mask of `/28` and a maximum of `/16`.
  - For example, a `/24` subnet provides 256 IP addresses. However, in AWS, five IP addresses are reserved by default in every subnet:
    - Two IPs are reserved by the standard networking conventions (Network ID and Broadcast Address).
    - Three additional IPs are reserved by AWS (typically for the VPC router, DNS servers, and future use).
  - In a `/24` subnet, usable IP addresses = 256 - 5 = 251.
  
- **VPC Design Best Practices:**  
  - Plan for scalability and future growth.
  - Ensure subnets are distributed across multiple Availability Zones for high availability.
  - Allocate public subnets for internet-facing resources and private subnets for backend resources.
  - Reserve sufficient IP space in your VPC to accommodate future expansion.
  
- **Routing and Security:**  
  - Use appropriate route tables and network ACLs to manage traffic between subnets.
  - Configure security groups to control access to resources in both public and private subnets.

---

