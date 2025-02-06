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

## VPC and Subnet Configuration Documentation

### **Step 1: Create a VPC**

- **VPC Name:** CustomVPC/Dev-VPC/UAT-VPC/PRD-VPC 
- **VPC CIDR Block:** 192.168.0.0/22  
  - This CIDR block provides 1024 IP addresses (2^10), which are sufficient to allocate subnets for current and future needs.

---

### **Step 2: Create Subnets within CustomVPC**

Create separate subnets for public and private resources across different Availability Zones (AZs):

- **Public Subnets:**  
  - **Public-SN-1A:**  
    - **Availability Zone:** ap-south-1a  
    - **CIDR Block:** 192.168.0.0/24  
    - Provides up to 256 IP addresses (minus AWS-reserved IPs).  
  - **Public-SN-1B:**  
    - **Availability Zone:** ap-south-1b  
    - **CIDR Block:** 192.168.1.0/24

- **Private Subnets:**  
  - **Private-SN-1A:**  
    - **Availability Zone:** ap-south-1a  
    - **CIDR Block:** 192.168.2.0/25  
    - Provides up to 128 IP addresses (minus AWS-reserved IPs).  
  - **Private-SN-1B:**  
    - **Availability Zone:** ap-south-1b  
    - **CIDR Block:** 192.168.2.128/25

*Note: Reserving multiple subnets across different AZs increases availability and fault tolerance.*

---

### **Step 3: Create and Attach an Internet Gateway**

- **Internet Gateway (IGW):**  
  - Create one IGW and attach it to the CustomVPC.
  - An Internet Gateway allows resources in the public subnets to communicate with the internet.
  - One VPC Support only one IGW.

---

### **Step 4: Create Route Tables and Associate with Subnets**

#### **Public Route Table (PublicRoute)**
- **Association:**  
  - Associate with all public subnets (Public-SN-1A and Public-SN-1B).
- **Routing Rule:**  
  - Add a route for Internet traffic:  
    - Destination: 0.0.0.0/0  
    - Target: Internet Gateway (IGW)

#### **Private Route Table (PrivateRoute)**
- **Association:**  
  - Associate with private subnets (Private-SN-1A and Private-SN-1B).
- **Routing Rule:**  
  - For private subnets that do not require internet access, no default route via an Internet Gateway is added.
  - For private subnets that need internet access (for example, for patching, software updates, or accessing external endpoints), configure a NAT Gateway (see below) and add a default route via the NAT Gateway.

---

### **Step 5: Optional Public IP Assignment and DNS Settings**

- **Enable Auto-Assign Public IP:**  
  - Navigate to the Public Subnet settings in the VPC console, select "Modify auto-assign public IP settings," and enable the option. This ensures that resources launched in the public subnets receive a public IP automatically.
  
- **Enable DNS Hostnames:**  
  - In the VPC settings, choose "Edit VPC Settings" and enable DNS hostnames. This is particularly important for services like RDS Clusters that rely on DNS for endpoint resolution.

---

### **Bastion (Jump) Server**

- **Purpose:**  
  - A dedicated EC2 instance, typically placed in a public subnet, that acts as a secure gateway (bastion host) to connect to instances in private subnets.
- **Usage:**  
  - Administrators log into the bastion host via SSH or RDP and then connect to resources within the private subnets.

---

## NAT Gateway and Private Subnet Internet Access

### **Purpose of NAT Gateway:**
- **Network Address Translation (NAT) Gateway** allows EC2 instances in private subnets to access the internet (for updates, patching, outbound API calls, etc.) while preventing inbound connections from the internet.
- NAT Gateway is deployed in a public subnet and is assigned a static public IP via an Elastic IP (EIP).  

- **Note:** NAT Gateways are not available under the free tier and incur additional costs.

### **Configuration for Private Subnets with Internet Access:**

1. **Create a NAT Gateway:**  
   - Deploy the NAT Gateway in one of the public subnets.  
   - Associate an Elastic IP (EIP) with the NAT Gateway.

2. **Update Private Route Table (PrivateRoute):**  
   - Add a default route for private subnets that require internet access:  
     - Destination: 0.0.0.0/0  
     - Target: NAT Gateway ID

This configuration allows private subnet resources to initiate outbound traffic to the internet while remaining inaccessible from the internet directly.

---

## Summary of Network Architecture

- **CustomVPC (192.168.0.0/22):** Provides up to 1024 IPs.
- **Public Subnets:**  
  - Public-SN-1A (ap-south-1a): 192.168.0.0/24  
  - Public-SN-1B (ap-south-1b): 192.168.1.0/24  
- **Private Subnets:**  
  - Private-SN-1A (ap-south-1a): 192.168.2.0/25  
  - Private-SN-1B (ap-south-1b): 192.168.2.128/25  
- **Internet Gateway:** Attached to CustomVPC for public subnet internet access.
- **Route Tables:**  
  - PublicRoute: Associated with public subnets; route 0.0.0.0/0 via IGW.  
  - PrivateRoute: Associated with private subnets; route 0.0.0.0/0 via NAT Gateway for those requiring internet access.
- **Bastion Host:** Located in public subnets to securely access instances in private subnets.
- **DNS and Public IP:** Ensure auto-assignment of public IPs in public subnets and enable DNS hostnames for seamless integration with AWS services.

---

## VPC Flow Logs

VPC Flow Logs enable you to capture information about the IP traffic going to and from network interfaces in your Virtual Private Cloud (VPC). Flow Logs can be created at different levels to suit your monitoring and auditing requirements:

- **VPC Level:** Capture traffic for all network interfaces in the VPC.
- **Subnet Level:** Capture traffic for all network interfaces within a specific subnet.
- **Instance Level:** Capture traffic for a specific network interface (attached to an instance).

### Flow Logs Destination Options

When creating Flow Logs, you can choose one of the following destinations:
1. **S3 Bucket:** Store logs in an S3 bucket for long-term archival and analysis.
2. **CloudWatch Logs Group:** Stream logs to CloudWatch for real-time monitoring and alerting.
3. **Kinesis Data Firehose:** Stream logs to Kinesis for further processing or integration with external systems.

### IAM Role and Policy for Flow Logs

Before enabling VPC Flow Logs, you must create an IAM role with a policy that grants the required permissions. Below is an example policy that allows CloudWatch Logs operations:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogStream",
                "logs:DescribeLogGroups",
                "logs:DescribeLogStreams",
                "logs:CreateLogGroup",
                "logs:PutLogEvents"
            ],
            "Resource": "*"
        }
    ]
}
```

**Steps to Create the Flow Logs Role:**

1. **Create an IAM Policy:**  
   - Create a new policy in IAM using the JSON above.
   
2. **Create an IAM Role:**  
   - When creating the role, set the trust relationship as follows to allow VPC Flow Logs to assume the role:
   
   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Principal": {
                   "Service": "vpc-flow-logs.amazonaws.com"
               },
               "Action": "sts:AssumeRole"
           }
       ]
   }
   ```
   
3. **Associate the Policy with the Role:**  
   - Attach the newly created policy to the role.

Once the role is in place, you can enable Flow Logs on your VPC, subnet, or network interface and choose the desired log destination.

---

## Network Access Control Lists (NACLs)

NACLs are a stateless firewall that operate at the subnet level, allowing you to control both inbound and outbound traffic for each subnet in your VPC.

### Key Characteristics of NACLs

- **Subnet Association:**  
  - A subnet can be associated with only one NACL at a time.
  
- **Default NACL:**  
  - Every VPC comes with a default NACL that allows all traffic. New custom NACLs, however, deny all traffic by default until you add explicit allow rules.
  
- **Rule Evaluation Order:**  
  - NACL rules are evaluated in order, starting from the lowest numbered rule. The first rule that matches the traffic is applied, making lower-numbered rules higher priority.
  
- **Ephemeral Ports:**  
  - In addition to defining rules for common ports, you must account for ephemeral (temporary) ports. AWS recommends allowing traffic on ports 1024 through 65535 as needed, especially for return traffic from clients.

### Comparison: Security Groups vs. NACLs

- **Security Groups:**  
  - Act as a stateful firewall at the instance level.
  
- **NACLs:**  
  - Operate at the subnet level as a stateless firewall.
  - You must explicitly allow both inbound and outbound traffic.

---

## Endpoints (Private Links)

Endpoints, also known as Private Links, enable private connectivity between your VPC and AWS services (such as S3 or DynamoDB) without routing traffic over the public internet.

### Types of Endpoints

1. **Gateway Endpoints:**  
   - Managed by AWS and used for services such as S3 and DynamoDB.
   - There is no hourly charge; you pay only for data transfer.
   
2. **Interface Endpoints:**  
   - Provisioned as elastic network interfaces (ENIs) in your VPC.
   - Provide private connectivity to a wide range of AWS services and third-party applications.
   - Incur an hourly charge per endpoint and data transfer fees.

### Use Cases for Endpoints

- **Enhanced Security:**  
  - Keep traffic between your VPC and AWS services private by avoiding the public internet.
  
- **Compliance:**  
  - Satisfy regulatory requirements by ensuring data remains within a private network.
  
- **Simplified Connectivity:**  
  - Easily connect to services like S3 and DynamoDB without configuring VPNs or NAT devices.

---
---

## VPC Peering

VPC Peering allows communication between multiple Virtual Private Clouds (VPCs) regardless of whether they are in the same region, different regions, or even different AWS accounts. This is useful for scenarios where resources in separate VPCs need to interact securely.

### Key Considerations for VPC Peering

- **Non-Overlapping CIDR Blocks:**  
  The requester VPC and the accepter VPC must have non-overlapping CIDR ranges. For example:
  - Requester VPC (Mumbai): CIDR 192.168.0.0/22  
  - Accepter VPC (Northern Virginia): CIDR 10.0.0.0/16

- **Non-Transitivity:**  
  VPC peering is non-transitive. This means if VPC A is peered with VPC B, and VPC B is peered with VPC C, VPC A cannot automatically communicate with VPC C. Separate peering connections are required.

- **Route Table Updates:**  
  Once a peering connection is established, update the route tables in both VPCs to direct traffic destined for the peer VPC’s CIDR block through the peering connection.

### Example VPC Peering Settings

| Field            | Requester VPC (Mumbai)       | Accepter VPC (Northern Virginia)   |
|------------------|------------------------------|------------------------------------|
| VPC CIDR         | 192.168.0.0/22               | 10.0.0.0/16                        |
| VPC ID           | vpc-08eb76bde20cef7          | vpc-0ba782a5b7a0a49                |
| Region           | ap-south-1                   | us-east-1                          |
| Account ID       | 123445678998                 | 123445678998                       |

---

## Site-to-Site VPN Configuration (Enterprise Level)

For enterprises with a dedicated firewall device, establishing a Site-to-Site VPN requires the following steps:

1. **Create a Virtual Private Gateway (VGW):**  
   Attach the Virtual Private Gateway to your VPC.

2. **Create a Customer Gateway (CGW):**  
   Provide the public IP address of your corporate office's firewall. This is the external endpoint that the VPN will connect to.

3. **Establish the VPN Connection:**  
   Using the Virtual Private Gateway and the Customer Gateway, configure the Site-to-Site VPN. Download the VPN configuration from the AWS console and share it with your firewall team for configuration on the on-premises device.

---

## Associating Multiple CIDRs with a VPC

AWS allows you to associate multiple CIDR blocks with a single VPC. This can help accommodate future growth or separate distinct workloads. When adding an additional CIDR block, ensure that:

- The new CIDR range does not conflict with any existing CIDR range in the VPC.
- Proper route tables and network ACLs are updated to reflect the new address space.

---

## NAT Gateway Alternatives for IPv6

NAT Gateways in AWS work only with IPv4 addresses. For VPCs configured with IPv6 addressing, use an "Egress-Only Internet Gateway" instead. The Egress-Only Internet Gateway provides IPv6 outbound communication for instances in a private subnet while preventing inbound IPv6 traffic from the internet.

---
## **AWS Transit Gateway**

### **What is AWS Transit Gateway?**  
AWS **Transit Gateway (TGW)** is a scalable and centralized networking hub that enables connectivity between multiple VPCs, on-premises networks, and AWS services. It simplifies network architecture by reducing the complexity of managing multiple VPC peering connections.

### **Key Benefits of Transit Gateway**
- **Scalability:** Connect thousands of VPCs and on-premises networks.
- **Simplified Management:** Eliminates the need for complex VPC peering.
- **High Performance:** Uses AWS backbone for optimized data routing.
- **Centralized Security:** Easily apply security policies across networks.

---

## **Steps to Create and Configure AWS Transit Gateway**
Follow these high-level steps to set up and configure an AWS Transit Gateway:

### **Step 1: Create a Transit Gateway**
1. Open the **AWS Management Console**.
2. Navigate to **VPC > Transit Gateway**.
3. Click **Create Transit Gateway**.
4. Provide a **Name** and **Description**.
5. Configure settings:
   - **Amazon side ASN:** (Auto-generated or custom ASN)
   - **DNS Support:** Enabled
   - **VPN ECMP Support:** Enabled/Disabled (based on requirement)
   - **Multicast Support:** Enabled/Disabled (for multicast traffic)
6. Click **Create Transit Gateway**.

---

### **Step 2: Create Transit Gateway Attachments**
You need to attach **VPCs**, **VPNs**, or **Direct Connect gateways** to the Transit Gateway.

#### **Attach a VPC**
1. Navigate to **Transit Gateway Attachments**.
2. Click **Create Attachment**.
3. Choose **VPC attachment**.
4. Select the **Transit Gateway ID**.
5. Choose the **VPC to attach** (Share TGW with RAM (Resource Access Manager), if you want to share with other region VPCs / Account VPC.
6. Select the **subnets** to associate.
7. Click **Create Attachment**.


---

### **Step 3: Update Route Tables**
Each VPC must have a **route table entry** directing traffic to the Transit Gateway.

1. Navigate to **VPC > Route Tables**.
2. Select the **VPC Route Table**.
3. Click **Edit Routes**.
4. Add a route:
   - **Destination:** CIDR of the peer VPC
   - **Target:** Transit Gateway ID
5. Click **Save Routes**.

---

### **Step 4: Validate Connectivity**
- **Use `ping` or `traceroute` commands** to check network reachability.
- **Enable VPC Flow Logs** to monitor traffic flow.
- **Use AWS Transit Gateway Route Tables** to verify routing.

---

### **Video Reference**  
For a detailed step-by-step tutorial, watch this **YouTube video:**  
🔗 **[AWS Transit Gateway Full Setup](https://www.youtube.com/watch?v=xyLlMBHy2wc)**  

---
