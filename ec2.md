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
- We can sell Instance in AWS MarketPlace, if we dont want to use it anymore.

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


#### **Step 1: Add Tags**  
- Tags help organize and identify resources.  
  Example:  
  ```
  Key: Name        Value: Windows-Server
  Key: Project     Value: AWSPractice
  Key: Platform    Value: Windows
  Key: CostCenter Value: AAZAA
  ```

#### **Step 2: Choose an AMI (Amazon Machine Image)**  

**Choose an AMI (Amazon Machine Image)**:
An AMI is a pre-configured template provided by AWS that contains the information needed to launch an EC2 instance. It includes:
Operating System: Linux, Windows, etc.
- Pre-installed software or tools.
- Security and settings required for the instance.

#### **Step 3: Choose an Instance Type**:
   - Example: `t2.micro` (1 vCPU, 1 GB RAM; Free Tier eligible).
   - We cannot customise configuration based on our requiremenet. we can use preavailable configs.

   **Instance Categories**:
   - **General Purpose**: Balanced compute, memory, and networking : Ideal for business critical applications, small and mid-sized databases, web tier applications(T & M (i.e; t3, t4g, m4, m5)).
   - **Compute Optimized**: For CPU-intensive tasks : Ideal for high performance computing, batch processing, video encoding, and more.(e.g., `c4`, `c5`).
   - **Memory Optimized**: For memory-intensive workloads : Ideal for high performance databases, distributed web scale in-memory caches, real time big data analytics (e.g., `R4`,`R5`,`R6`,`x1`,`Z1`).
   - **Storage Optimized**: For high IOPS workloads : Ideal for NoSQL databases, data warehousing, distributed file systems (e.g., `i3`, `d2`).
   - **GPU Optimized**: For machine learning or gaming : Ideal for machine learning, graphic intensive applications, gaming (e.g., `f1`,`p3`,`g4`).


#### **Step 4: Choose/Create akeyPair**  
- Choose an existing key pair or create a new one.  
  - **Key Pair**:  
    - **Public Key**: Stored by AWS in the EC2 instance.  
    - **Private Key (.pem)**: Downloaded and stored securely by the user.  
  - This private key is required to connect to the instance via SSH.  
  - Used for "Secure Authentication", "Encryption", "Ease of Management (Passwordless)"


#### **Step 5: Choose network Settings**  
  - For now, Please use "Default VPC" with "Default Subnet"
  - Enable "Auto Assign Public IP" as we want to connect to instance over internet.
  
  **Configure Security Group**  
  - **Security Group** acts as a firewall for the instance. Add the following rules:  
    - **SSH (22)**: Anywhere (Not recommended for production). For tighter security, restrict access to your specific IP.  
    - **HTTP (80)**: For web servers.  
    - **HTTPS (443)**: For secure web traffic.
	
   - **Source**: Define from what network we can connect .
     - **My IP**: Your current network IP.
     - **Custom**: Specify an IP range.
     - **Anywhere**: Open to all (not recommended).

  
#### **Step 6: Choose Storage**  
- **Root Volume**: The Minimum required size for Windows is 30 GB, which can be increased as required.
	- We can increase existing volume size and We can add new new volume also.

#### **Step 7: Configure Additional Settings**  
- **VPC**: Default VPC is usually sufficient for most cases.  
- **Roles**: Attach an IAM role if the instance needs to access other AWS services.  
- **User Data**: Add shell scripts here for tasks like software installation during instance initialization. 

- **Instance Termination Protection**:  
  - Enable this to prevent accidental termination.  
- **Shutdown Behavior**:  
  - Choose **STOP** so the instance halts instead of being terminated when shut down.

#### **Step 8: Review and Launch**  

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

### **Common error: Permissions are too open / Bad permisisons**
Please open command prompt from the location where keypair is present

Prevent the file from inheriting permissions:
```
icacls "<path-to-private-key-file>" /inheritance:r
```
Deny all access to the Everyone group:
```
icacls "<path-to-private-key-file>" /deny Everyone:F
```
Grant Read Permission Only to Your User:
```
icacls "<path-to-private-key-file>" /grant:r "%USERNAME%:R"
```

### **Instance Management**
- **Start/Stop**: Temporarily pause usage while retaining configuration.
- **Terminate**: Permanently delete the instance.

---

### **Linux OS on EC2 Instances**

Linux OS Examples:  
- **Amazon Linux 2 OS** (AWS-managed Linux distribution)
- **RHEL** (Red Hat Enterprise Linux)
- **Ubuntu** (Popular for development)
- **SUSE**
- **Kali** (For penetration testing and security)

**Note:**  
- **Amazon Linux 2** is optimized for AWS and is based on Red Hat/CentOS.  
- The process below focuses on launching and connecting to an Amazon Linux 2 instance.

---

### **Steps to Launch a Linux Instance**

#### **Step 1: Add Tags**  
- Tags help organize and identify resources.  
  Example:  
  ```
  Key: Name        Value: LinuxServer
  Key: Project     Value: AWSPractice
  Key: Platform    Value: Linux
  Key: Cost Center Value: AAZAA
  ```


#### **Step 2: Choose an AMI (Amazon Machine Image)**  
- Select the **Operating System**. For this example, choose **Amazon Linux 2 (Free Tier eligible)**.

#### **Step 3: Choose an Instance Type**  
- For beginners, select **t2.micro** (Free Tier eligible).  
  - It offers 1 vCPU and 1 GB RAM, suitable for basic workloads like learning or development.  

#### **Step 4: Choose/Create akeyPair**  
- Choose an existing key pair or create a new one.  
  - **Key Pair**:  
    - **Public Key**: Stored by AWS in the EC2 instance.  
    - **Private Key (.pem)**: Downloaded and stored securely by the user.  
  - This private key is required to connect to the instance via SSH.  
  - Used for "Secure Authentication", "Encryption", "Ease of Management (Passwordless)"

#### **Step 5: Choose network Settings**  
  - For now, Please use "Default VPC" with "Default Subnet"
  - Enable "Auto Assign Public IP" as we want to connect to instance over internet.
  
  **Configure Security Group**  
  - **Security Group** acts as a firewall for the instance. Add the following rules:  
    - **SSH (22)**: Anywhere (Not recommended for production). For tighter security, restrict access to your specific IP.  
    - **HTTP (80)**: For web servers.  
    - **HTTPS (443)**: For secure web traffic.
  
#### **Step 6: Choose Storage**  
- **Root Volume**: The default size for Amazon Linux is 8 GB, which can be increased as required.

#### **Step 7: Configure Additional Settings**  
- **VPC**: Default VPC is usually sufficient for most cases.  
- **Roles**: Attach an IAM role if the instance needs to access other AWS services.  
- **User Data**: Add shell scripts here for tasks like software installation during instance initialization. 

- **Instance Termination Protection**:  
  - Enable this to prevent accidental termination.  
- **Shutdown Behavior**:  
  - Choose **STOP** so the instance halts instead of being terminated when shut down.

#### **Step 8: Review and Launch**  

---

### **How to Connect to a Linux Instance**

#### **Option 1: EC2 Instance Connect (Browser-Based)**  
1. Go to the **EC2 Dashboard**.  
2. Select the instance and click **Connect**.  
3. Choose **EC2 Instance Connect**.  
4. Use the default username **ec2-user**.  
5. Click **Connect**.  

> **Note:** This method is often used for quick testing but not in real-time production environments.

---

#### **Option 2: Using Windows Command Prompt or PowerShell**  
1. Install **OpenSSH Client** on your Windows laptop if not already installed.  
   - Go to **Settings** → **Apps & Features** → **Optional Features** → Enable or Install **OpenSSH Client**.  
   - [Microsoft Docs for OpenSSH Setup](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse).  
2. Open Command Prompt or PowerShell.  
3. Use the command:  
   ```
   ssh -i "keypair.pem" ec2-user@<Public-IP/DNS>
   Example: ssh -i "linuxkp.pem" ec2-user@ec2-3-108-53-198.ap-south-1.compute.amazonaws.com
   ```

---

#### **Option 3: Using PuTTY (Windows)**  
1. **Convert the .pem file to .ppk** format using **PuTTYgen**:  
   - Open PuTTYgen.  
   - Load the .pem file and save it as a .ppk file.  
2. Download and install **PuTTY** from [PuTTY official website](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).  
3. Open PuTTY and configure:  
   - **Host Name**: Public IP or DNS of the instance.  
   - **Port**: 22.  
   - **Connection Type**: SSH.  
   - **Auth**: Browse and upload the .ppk file.  
4. Click **Open** to connect.  

---

#### **Option 4: Using Git Bash (Windows)**  
1. Install **Git for Windows** from [Git-SCM](https://git-scm.com/download/win).  
2. Open Git Bash in the directory where your key pair (.pem) is stored.  
3. Use the command:  
   ```
   chmod 400 keypair.pem
   ssh -i "keypair.pem" ec2-user@<Public-IP/DNS>
   ```

---

#### **Common Error: Unprotected Private Key File**  
- If you see an error like **Bad Permissions**, set appropriate permissions for the .pem file:  
  ```
  chmod 400 keypair.pem
  ```
  This works for Git Bash or other Linux-compatible terminals.

---

### **Linux Instance Default Usernames**  
- **Amazon Linux**: `ec2-user`  
- **RHEL**: `ec2-user` or `root`  
- **Ubuntu**: `ubuntu`  
---

