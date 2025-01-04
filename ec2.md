---

### **What is a Server?**
A server is a powerful computer designed to process requests, store data, and provide services or resources to other computers, known as clients. Unlike personal computers, servers are optimized for reliability, scalability, and availability to handle multiple client connections simultaneously.

#### **Real-life Use Cases of Servers:**
1. **Web Hosting**: Websites and applications run on servers.
2. **Database Hosting**: Large databases are stored and accessed from servers.
3. **File Sharing**: Servers manage shared drives or folders in organizations.
4. **Gaming**: Multiplayer online games are hosted on dedicated servers.
5. **Email Services**: Emails are sent and received through mail servers.

---

### **EC2 Overview**
- **Elastic Compute Cloud (EC2)** is Amazon’s cloud-based virtual server offering.
- EC2 is a **region-specific service**, meaning instances are hosted in AWS regions close to your users or workloads.

#### **Server Components:**
- **CPU**: Processes computations.
- **Memory (RAM)**: Stores data for quick access.
- **Storage (HDD/SSD)**: Stores operating systems and applications.
- **Network Interface**: Facilitates communication with other systems.

#### **Instance Terminology**
- Instance = Server = Azure VM (Azure) = Compute Engine (Google Cloud).

#### **Server OS Types**
- **Client OS**: Windows 7, Windows 10, Ubuntu Desktop
- **Server OS**: RHEL, Ubuntu Server, Windows Server 2008 R2, 2012, 2016, 2019, 2022, 2025 and newer.

---

### **EC2 Pricing Models**

1. **On-Demand Instances**
   - Ideal for **unpredictable workloads** or short-term testing.
   - Charged **per second** (minimum 60 seconds).
   - **Free Tier Eligibility**: Available for limited usage (t2.micro instance).

2. **Reserved Instances**
   - Suitable for **predictable workloads** over longer durations (1 or 3 years).
   - **Types**:
     - **Standard RI**: No configuration changes allowed.
     - **Convertible RI**: Configurations can be modified (e.g., instance family or OS type).
     - **Scheduled RI**: For recurring workloads at specific times.
   - **Payment Options**:
     - **Full Upfront**: Pay 100% upfront.
     - **Partial Upfront**: Pay 30-50% upfront; remaining is paid monthly.
     - **No Upfront**: Pay entirely on a monthly basis.

3. **Spot Instances**
   - For **flexible workloads** with no critical data.
   - Bid your price against AWS pricing.
   - **Use Case**: Testing or temporary environments.
   - **Pricing Rules**:
     - If AWS price exceeds your bid, the instance is terminated.
     - If terminated by AWS, you are charged only for full hours used.
     - If terminated manually, you're charged for the full duration.

---

### **Launching a Windows EC2 Instance**

#### **Steps to Launch an EC2 Instance**
1. **Choose an AMI (Amazon Machine Image)**:
   - Select the OS for your instance (e.g., Windows Server 2016 Base).

2. **Choose an Instance Type**:
   - Example: `t2.micro` (1 vCPU, 1 GB RAM; Free Tier eligible).

   **Instance Categories**:
   - **General Purpose**: Balanced compute, memory, and networking (e.g., `t2`, `t3`, `m5`).
   - **Compute Optimized**: For CPU-intensive tasks (e.g., `c4`, `c5`).
   - **Memory Optimized**: For memory-intensive workloads (e.g., `r5`, `x1`).
   - **Storage Optimized**: For high IOPS workloads (e.g., `i3`, `d2`).
   - **GPU Optimized**: For machine learning or gaming (e.g., `p3`, `g4`).

3. **Configure Additional Settings**:
   - **Network**: Choose a VPC and subnet.
   - **IAM Roles**: Assign permissions if needed.
   - **User Data**: Add scripts to automate configurations.
   - **Instance Termination Protection**: Enable to prevent accidental termination.
   - **Shutdown Behavior**: Set to "Stop" to avoid accidental deletion.

4. **Add Storage**:
   - Root Volume: Minimum of 30 GB for Windows.
   - Additional Volumes: Optional based on workload.

5. **Add Tags**:
   - Tags help in categorizing and managing resources.
   - Example:
     - `Name`: MyInstance
     - `Project`: Demo
     - `Platform`: Windows/Linux

6. **Configure Security Groups**:
   - Acts as a firewall at the instance level.
   - Example Rules:
     - **RDP** (Windows): Port 3389.
     - **SSH** (Linux): Port 22.
     - **HTTP**: Port 80.
     - **HTTPS**: Port 443.
   - **Source**: Define who can connect.
     - **My IP**: Your current network IP.
     - **Custom**: Specify an IP range.
     - **Anywhere**: Open to all (not recommended).

7. **Review and Launch**:
   - Select a Key Pair (public-private key) to securely connect to the instance.

---

### **Connecting to a Windows Instance**

#### **From Windows**:
1. Open **Run** (Windows Key + R) → Type `mstsc` → Press Enter.
2. Enter the **Public IP** of the instance.
3. Username: `Administrator`.
4. Password: Retrieve using the private key.

#### **From Mac**:
1. Download **Microsoft Remote Desktop** from the App Store.
2. Enter the **Public IP**, Username (`Administrator`), and Password.

---

### **Instance Management**
- **Start/Stop**: Temporarily pause usage while retaining configuration.
- **Terminate**: Permanently delete the instance.

---

Let me know if further details are required!
