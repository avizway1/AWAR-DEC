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
   - If we have an application running inside an ec2 instance, that can be interrupted (or) if any interruption happens, it can be recovered without any organisational affects.
   - **Use Case**: Testing or temporary environments.
   - **Pricing Rules**:
     - If AWS price exceeds your bid, the instance is terminated.
     - If terminated by AWS, you are charged only for full hours used.
     - If terminated manually, you're charged for the full duration.

---
### **Understanding Free Tier**

The AWS Free Tier allows you to use up to **750 hours per month** for **t2.micro instances** (on-demand) for both **Windows** and **Linux** separately. Here's how it works:

1. **Single Instance Usage**  
   Running **1 instance** for **24 hours a day** in a 31-day month uses:  
   `1 instance x 24 hrs x 31 days = 744 hrs`  
   This is **within the 750-hour Free Tier limit**, so it's free.

2. **Multiple Instance Usage**  
   Running **2 instances** for **24 hours a day** for 16 days uses:  
   `2 instances x 24 hrs x 16 days = 768 hrs`  
   This **exceeds the 750-hour Free Tier limit** by 18 hours, so you'll be billed for those extra hours.

**Key Points:**
- The free tier applies to combined usage across instances (e.g., multiple instances sharing the 750-hour pool).
- Plan your usage carefully to stay within the limit and avoid charges.

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

---

						**Scenarios for Using Snapshots in AWS**

_**What is a Snapshot in AWS?**_
A snapshot in AWS is a point-in-time backup of an Amazon EBS (Elastic Block Store) volume. Snapshots are stored in Amazon S3, though not visible in your S3 bucket, and can be used to back up, restore, or replicate EBS volumes.

#### **1. Moving a Volume Between Instances in the Same Availability Zone (AZ)**  
- **Scenario:**  
  Instance 1 in `ap-south-1a` → Instance 2 in `ap-south-1a`.  
  - **Steps:**  
    - Detach the volume from **Instance 1**.  
    - Attach the volume to **Instance 2** within the same AZ.  
  - **Reason:**  
    Volumes can only be attached to instances within the same AZ.  

---

#### **2. Moving a Volume Between Instances in Different Availability Zones (AZs)**  
- **Scenario:**  
  Instance 1 in `ap-south-1a` → Instance 2 in `ap-south-1b`.  
  - **Steps:**  
    - Detach from **Instance 1** and attach to **Instance 2** is not directly possible due to AZ restrictions.  
    - **Solution:**  
      1. Choose the volume and take a **snapshot**.  
      2. Create a new volume from the snapshot and select `ap-south-1b` as the AZ during creation.  
      3. Attach the newly created volume to **Instance 2** in `ap-south-1b`.  

---

#### **3. Moving a Volume Between Instances in Different Regions**  
- **Scenario:**  
  Instance 1 in `Mumbai (ap-south-1a)` → Instance 2 in `N. Virginia (us-east-1a)`.  
  - **Steps:**  
    - Detach from **Instance 1** and attach to **Instance 2** is not directly possible due to region restrictions.  
    - **Solution:**  
      1. Take a **snapshot** of the volume.  
      2. Copy the snapshot to the desired region (`us-east-1`).  
      3. Create a volume from the copied snapshot, ensuring `us-east-1a` is selected as the AZ.  
      4. Attach the newly created volume to **Instance 2** in `N. Virginia (us-east-1a)`.  
    - **Note:** Data transfer between regions incurs costs.  

---

#### **4. Moving a Volume Between AWS Accounts in the Same Region**  
- **Scenario:**  
  Instance 1 in `AWS Account 1: Mumbai (ap-south-1a)` → Instance 2 in `AWS Account 2: Mumbai (ap-south-1a)`.  
  - **Steps:**  
    - Detach from **Instance 1** and attach to **Instance 2** is not directly possible as volumes cannot be shared across AWS accounts.  
    - **Solution:**  
      1. Take a **snapshot** of the volume in **AWS Account 1**.  
      2. Share the snapshot with **AWS Account 2**.  
      3. In **AWS Account 2**, create a volume from the shared snapshot, selecting `ap-south-1a` as the AZ.  
      4. Attach the new volume to **Instance 2**.  

---

#### **5. Sharing a Volume with Everyone (Public Access)**  
- **Scenario:**  
  Share a volume to make it accessible publicly.  
  - **Steps:**  
    - Take a **snapshot** of the volume.  
    - Mark the snapshot as **Public** in its permissions.  
    - Anyone can use this public snapshot to create their own volume.  
  - **Use Case:**  
    Sharing data, templates, or other resources broadly within the AWS community.  

---

### **AWS Snapshots Key Points**

1. **Point-in-Time Copies**  
   - Snapshots are **point-in-time copies** of EBS volumes, capturing the state and data of a volume at a specific moment.

2. **Storage Platform**  
   - Snapshots are stored in the **S3 platform**, but **not in your S3 bucket**. They are managed by AWS and are not visible in the S3 console.

3. **Viewing Data Inside Snapshots**  
   - **Can we view the data inside a snapshot?**  
     **No**, snapshots do not provide a direct way to browse or access the data they contain. They are only meant for creating new volumes or restoring existing ones.

4. **Incremental Backup Mechanism**  
   - Snapshots use an **incremental backup mechanism**, meaning:  
     - The first snapshot is a full backup.  
     - Subsequent snapshots only store the changes (blocks) made since the previous snapshot, optimizing storage and costs.

5. **Encryption and Snapshots**  
   - **Encrypted Volumes and Snapshots**:  
     - If a volume is encrypted, any snapshot created from it is **automatically encrypted**.  
   - **Creating Volumes from Encrypted Snapshots**:  
     - Volumes created from encrypted snapshots are also **automatically encrypted** with the same encryption key.

6. **Sharing Snapshots**  
   - **Default AWS Master Key Encryption**:  
     - Snapshots encrypted with the default AWS-managed KMS key **cannot be shared** across accounts.  
   - **Custom Encryption Key**:  
     - Snapshots encrypted with a **customer-managed key** can be shared with other AWS accounts, but:  
       - You must grant permissions on the encryption key to the target account.  
       - Without key permissions, the target account cannot use the shared snapshot.

---

### **AWS Data Lifecycle Manager (DLM)**  

**1. What is AWS DLM?**  
   - **AWS Data Lifecycle Manager (DLM)** is a service that automates the **creation, retention, and deletion of EBS snapshots**.  
   - DLM helps manage backups efficiently, reducing the operational overhead of manual snapshot creation and retention.

---

**2. Why is it important to take backups?**  
   - **Data Protection**: Backups protect critical data from unexpected events such as system failures, accidental deletions, or data corruption.  
   - **Disaster Recovery**: Ensures quick recovery in case of disasters, minimizing downtime and data loss.  
   - **Compliance**: Many organizations have regulatory requirements to maintain backups for a specific duration.  
   - **Versioning**: Maintains historical versions of data, allowing restoration to a specific point in time.  

---
### **Benefits of Using AWS DLM**  
1. Backups are taken on a fixed schedule, ensuring no resources are missed.  
2. Automatically deletes outdated snapshots, reducing unnecessary storage costs.  
3. Minimal manual intervention is required—DLM handles the entire lifecycle of snapshots.  

---

**3. How does DLM automate backups?**  
   - **Tag-Based Filtering**:  
     - DLM policies use **tags** to identify resources (EBS volumes) for automated snapshot management.  
     - By applying consistent tags across environments, DLM can handle backups for multiple resources effortlessly.  

   - **Retention Policies**:  
     - DLM lets you define **retention periods** to ensure that old snapshots are deleted automatically, optimizing storage costs.  
     - Real-Time Scenarios:  
       - **Production (Prod)**: Retain snapshots for **7 days**.  
       - **Non-Production (Non-Prod)**: Retain snapshots for **3 days**.  

   - **Scheduled Backup Creation**:  
     - You can specify the **frequency** and **time of backup creation** for each policy to ensure backups align with your operational requirements.  

   - **Fast Snapshot Restore (FSR)**:  
     - FSR ensures that volumes created from DLM-managed snapshots are ready to deliver full performance immediately after creation, eliminating initialization delays.

---
### **What is a Custom AMI (Golden AMI) in AWS?**

A **Golden AMI** is a pre-configured, **customized Amazon Machine Image** that includes all required software, configurations, and settings. It allows organizations to standardize deployments, save time, and ensure consistency across EC2 instances.

---

### **Importance of a Golden AMI**

#### **Scenario**:  
You have **10 EC2 instances**, each requiring the following: Antivirus software, Microsoft Office, Custom WordPress setup, Custom OS users, Applications and IIS server  

**Option 1**:  
- Launch 10 EC2 instances individually.  
- Manually configure each instance (install software, customize OS, etc.).  
- **Result**: Time-consuming, error-prone, and inconsistent configurations.  

**Option 2**:  
- Launch **1 EC2 instance** and perform all configurations.  
- Create a **Golden AMI** from this configured instance.  
- Use the Golden AMI to launch 10 instances.  
- **Result**: Time-efficient, consistent, and scalable.  

---

### **Steps to Create a Golden AMI**

1. **Launch a Base EC2 Instance**:
   - Choose an Amazon-provided AMI (e.g., Amazon Linux, Windows Server).  
   - Configure the instance (e.g., instance type, security groups, etc.).  

2. **Customize the Instance**:
   - Install required software (e.g., antivirus, MS Office, custom applications).  
   - Create OS users and set permissions.  
   - Perform system hardening, such as applying **CIS Benchmarks** for security compliance.  
   - Configure application settings (e.g., IIS or WordPress).  

3. **Prepare for AMI Creation**:
   - Clean temporary data and logs to reduce AMI size.  
   - Stop services or processes that should not run on boot.  
   - Ensure the instance is **stopped** or in a stable state.  

4. **Create the AMI**:
   - In the EC2 console, select the instance.  
   - Choose **Actions → Image and Templates → Create Image**.  
   - Provide a name and description for the image.  
   - Optionally, customize volume settings (e.g., size, encryption).  

5. **Validate the AMI**:
   - Launch a test instance from the AMI.  
   - Verify that all configurations and software are intact.  

---

### **Golden AMI Use Cases**

1. **Launch Instances in the Same Region**:
   - Use the Golden AMI to spin up additional instances within the same AWS Region.  

2. **Cross-Region Deployment**:
   - Copy the Golden AMI to another region using the **"Copy AMI"** feature.  
   - Launch instances in the target region.  

3. **Cross-Account Sharing**:
   - Share the Golden AMI with another AWS account using 12 digit account ID.
   - Share Golden AMI across the Organisation (Multiple AWS accounts)
     
4. **Public Sharing**:
   - Share the Golden AMI publicly for open usage (e.g., community use cases).  

---

### **Golden AMI vs Snapshots**

| Feature             | Golden AMI                         | Snapshot                             |
|---------------------|------------------------------------|--------------------------------------|
| **Purpose**         | Full system (OS + Apps + Data)     | Point-in-time backup of an EBS volume |
| **Deployment**      | Launch EC2 instances               | Restore or create EBS volumes        |
| **Customization**   | Includes OS and customizations     | Limited to volume content            |

---


---

### **Elastic IP Address (EIP)**
- **What is EIP?**
  - A static, public IPv4 address in AWS that you can assign to an EC2 instance or other AWS services.
  - Unlike a regular public IP, it persists even after stopping/Starting the instance.

- **Features**:
  1. **Dedicated IP**: Useful for applications requiring a consistent public IP (e.g., hosting a website).
  2. **Cost Considerations**: **Not free tier eligible**. Charges apply if the EIP is not associated with a running resource.

- **Important Note**:
  - AWS charges for EIPs that are allocated but not used.
  - Avoid unnecessary EIP allocation to reduce costs.

---

### **What is a Security Group?**
- **Definition**:
  - A virtual firewall for your EC2 instance to control inbound and outbound traffic.
  - You can specify rules based on protocols, ports, and IP addresses.

- **Types of Rules**:
  1. **Inbound Rules**:
     - Define what type of incoming traffic is allowed (e.g., SSH, HTTP).
  2. **Outbound Rules**:
     - Define what type of outgoing traffic is allowed (e.g., access to the internet).

- **Common Ports**:

| **Port** | **Protocol**   | **Purpose**                                |
|----------|----------------|--------------------------------------------|
| 20       | FTP            | File Transfer Protocol - Data Transfer.   |
| 21       | FTP            | File Transfer Protocol - Control.         |
| 22       | SSH/SFTP       | Secure shell access and secure file transfer. |
| 53       | DNS            | Domain Name System (name resolution).     |
| 80       | HTTP           | Unsecured web traffic (regular web browsing). |
| 389      | LDAP           | Lightweight Directory Access Protocol (directory services). |
| 443      | HTTPS          | Secured web traffic (secure web browsing). |
| 636      | LDAPS          | Secure Lightweight Directory Access Protocol. |
| 3306     | MySQL/MariaDB  | Database connections for MySQL or MariaDB. |
| 3389     | RDP            | Remote Desktop Protocol (Windows remote access). |
| 5432     | PostgreSQL     | Database connections for PostgreSQL.       |
| 8080     | HTTP (Alt)     | Alternative HTTP port, often used for web proxies. |
| 1433     | MS SQL         | Microsoft SQL Server database connections. |


---

### **1. Security Group Overview**
A Security Group is like the main **security guard** for your house. It decides who can enter (inbound rules) and who can leave (outbound rules). Just like in a house, you can allow specific people in and out based on rules.

---

### **2. Port Numbers**
Think of port numbers as specific **doors or windows** of your house that serve different purposes. Each door (port) is meant for specific visitors or activities:
- **Port 22 (SSH):** The **front door key** used by administrators to enter securely.
- **Port 80 (HTTP):** The **main gate** for public visitors (web traffic).
- **Port 443 (HTTPS):** The **VIP gate** for encrypted, secure communication.

Just like you don’t want every door in your house to be open for everyone, in EC2, you open specific ports based on the type of traffic you expect.

---

### **3. Inbound Rules**
Inbound rules decide **who can come into your house** and through which door:
- **Example:** If you want your friend to come to your house through the main gate (Port 80), you give them permission by adding their **name** (or in EC2, their IP address) to the guest list.

In EC2 terms:
- Allow **HTTP traffic (Port 80)** from **anyone** (0.0.0.0/0).
- Allow **SSH traffic (Port 22)** only from your **office network's IP address**.

**Real-world analogy:** A restaurant allowing customers through the front door but keeping the kitchen door locked, only accessible to staff.

---

### **4. Outbound Rules**
Outbound rules decide **who or what can leave your house**:
- **Example:** If you're ordering food online, you let your delivery request go out, but you don’t allow random spam emails from your computer.

In EC2 terms:
- By default, all outbound traffic is allowed, meaning your EC2 instance can communicate freely unless restricted.

**Real-world analogy:** A guest leaving your house after the party. You may allow them to leave through specific exits (e.g., the back gate).

---

### **5. Real-Life Scenarios**
Here are a few scenarios to simplify understanding:
- **Scenario 1: Hosting a Website**
  - You open **Port 80 (HTTP)** or **Port 443 (HTTPS)** to allow public users to access your website.
  - You may also open **Port 22 (SSH)** but restrict it to your own IP for maintenance.

- **Scenario 2: Secure Communication**
  - If you're running a private application, you allow **Port 3306** (MySQL) but restrict access to only the application server’s IP.

- **Scenario 3: Blocking Unwanted Visitors**
  - If you notice unusual traffic (like hackers), you update the rules to block their IP addresses, much like telling your security guard not to let specific people in.

---

### **What is Amazon CloudWatch?**
Amazon CloudWatch is a powerful monitoring and observability service in AWS. It provides actionable insights by collecting metrics, logs, and events for your AWS resources and applications.

- **Features**:
  - Monitors various AWS resources such as **EC2, S3, RDS, DynamoDB, Lambda**, and more.
  - Tracks metrics like **CPU usage, Disk I/O, and Network traffic** for EC2 instances.
  - Supports custom metrics for monitoring application-specific performance.
  - Enables **log analysis** using CloudWatch Logs.

- **Memory Monitoring**:
  - By default, CloudWatch does not monitor **Memory/RAM and OS level Disk Utilization**.
  - **Solution**: Install and configure the **CloudWatch Agent** on the EC2 instance to collect memory usage and other custom metrics. (Note: This incurs additional costs.)

---

### **Types of Monitoring in CloudWatch**
1. **Basic Monitoring**:
   - **Default**: Enabled automatically for supported resources.
   - **Interval**: Metrics are collected at **5-minute intervals**.
   - **Cost**: Free.

2. **Detailed Monitoring**:
   - **Optional**: Must be explicitly enabled.
   - **Interval**: Metrics are collected at **1-minute intervals**.
   - **Cost**: Additional charges apply.
   - **Use Case**: Required for time-sensitive or high-resolution metric monitoring.

---

### **What is a CloudWatch Alarm?**
A CloudWatch Alarm monitors specific metrics and triggers actions based on predefined thresholds. It integrates with other AWS services to notify you or take automated actions when an issue occurs.

- **How It Works**:
  1. Define a **metric** to monitor (e.g., CPU Utilization).
  2. Set a **threshold** (e.g., CPU exceeds 80%).
  3. Specify an **action** (e.g., send an email or auto-scale instances).

---

### **Common Use Cases for CloudWatch Alarms**
1. **Resource Monitoring**:
   - Notify when EC2 **CPU utilization** exceeds 80%.
   - Alert when **Memory usage** is high (requires CloudWatch Agent).
   - Trigger actions if an EBS volume is running out of space.

2. **Auto-Scaling**:
   - Automatically scale EC2 instances up or down based on traffic or workload.

3. **Application Performance**:
   - Trigger alarms if RDS database connections exceed a safe limit.
   - Monitor Lambda function invocations and error rates.

4. **Health Monitoring**:
   - Get alerts for unhealthy targets in an Application Load Balancer (ALB).
   - Monitor and respond to high error rates in APIs or application logs.

---

### **AWS EFS (Elastic File System) Overview**  
EFS is a **fully managed, scalable, and elastic file storage system** designed to provide shared access across multiple EC2 instances.

---

### **Key Features:**  
- **Protocol:**  
  - Works with **NFS v4.1/v4.0**, using port **2049** for communication.  
  - Supports **Linux-based operating systems only.**  
  - For Windows, AWS FSx (using SMB protocol) is recommended.  

- **Scalability:**  
  - No pre-provisioning required; storage grows and shrinks automatically.  
  - Can handle petabytes of data seamlessly.  

- **Performance Modes:**  
  1. **General Purpose (default)** – Suitable for most workloads.  
  2. **Max I/O** – Designed for high throughput and parallel operations.  

- **Throughput Modes:**  
  1. **Bursting (default):** Performance scales with the size of the file system.  
  2. **Provisioned:** Fixed throughput, useful for high-performance needs.  

---

### **Mounting EFS on EC2 Instances**  

#### **Step 1: Create a mount directory**  
```bash
mkdir /server1
```

#### **Step 2: Mount the EFS file system**  
```bash
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-0b7b1937bf7ebbeb6.efs.ap-south-1.amazonaws.com:/ /server1
```

**Explanation of mount options:**  
- `-t nfs4` → Specifies the NFS version.  
- `nfsvers=4.1` → Specifies NFS version 4.1.  
- `rsize/wsize=1048576` → Read/write buffer size in bytes.  
- `hard` → Ensures operations retry indefinitely in case of failures.  
- `timeo=600` → Timeout in deciseconds before retrying an operation.  
- `retrans=2` → Number of retries before giving up.  
- `noresvport` → Uses a new dynamic source port for each connection.  

---

### **Persistent Mount Using `/etc/fstab`**  
To ensure the EFS mount persists after reboot, add the following entry in the `/etc/fstab` file:

```bash
fs-0b7b1937bf7ebbeb6.efs.ap-south-1.amazonaws.com:/ /server1 nfs4 nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 0 0
```

You can verify active mounts using:

```bash
cat /etc/mtab
```

---

### **Security Group Configuration for EFS**  
To allow EC2 instances to connect to EFS, create a security group with inbound rules allowing **NFS (port 2049)**. Options include:

1. **Open to the entire VPC CIDR block:**  
   - Allows any instance within the VPC to connect.  
   - Example: `10.0.0.0/16` (depends on your VPC CIDR).  

2. **Allow specific EC2 private IP addresses:**  
   - Use instance-specific private IPs in the rule to restrict access.  

3. **Reference EC2 security groups (recommended):**  
   - The most secure approach:  
   - Allow inbound traffic from EC2's security group instead of IP-based rules.  

---

### **Use Cases for AWS EFS**  
- Centralized storage for multiple EC2 instances (e.g., web servers).  
- Application data sharing across different environments.  
- Backup and archival purposes.  
- Scalable storage solution for containerized applications (ECS/EKS).  

---
### **AWS Placement Groups Overview**  
AWS **Placement Groups** are logical groupings of EC2 instances that influence how instances are placed on underlying hardware. They help optimize performance, reduce latency, or improve fault tolerance, depending on the workload requirements.

---

### **Types of Placement Groups:**  

#### **1. Cluster Placement Group**  
A **Cluster Placement Group (CPG)** places instances close together within a **single Availability Zone** to achieve **low-latency and high-throughput performance.**  

**Best suited for:**  
- Applications requiring **high network throughput** and **low latency.**  
- Big data applications (e.g., Hadoop clusters).  
- High-performance computing (HPC).  
- Distributed databases.

---

#### **2. Partition Placement Group**  
A **Partition Placement Group (PPG)** divides instances into **multiple isolated partitions** across multiple racks within an Availability Zone. Each partition is isolated from failures in other partitions.  

**Best suited for:**  
- Distributed and fault-tolerant applications (e.g., Hadoop, Kafka, Cassandra).  
- Large-scale distributed applications that need redundancy.  
- Workloads where failures should be isolated to specific partitions.


---

#### **3. Spread Placement Group**  
A **Spread Placement Group (SPG)** places instances across **distinct hardware racks**, ensuring that each instance is on a separate rack with its own power and network.  

**Best suited for:**  
- Applications requiring **high availability** and **minimal risk of simultaneous failure.**  
- Critical workloads such as financial applications, monitoring systems, or microservices.  
- Small deployments requiring fault tolerance (up to 7 instances per AZ).  

---

### **Choosing the Right Placement Group**  
1. **Choose Cluster Placement Group if:**  
   - You need low-latency, high-speed network connectivity.  
   - Your workload is tightly coupled and requires high throughput.  

2. **Choose Partition Placement Group if:**  
   - You need fault isolation within distributed applications.  
   - You are running big data clusters with failure resilience.  

3. **Choose Spread Placement Group if:**  
   - You need to minimize risk by placing instances on separate hardware.  
   - You have a smaller number of critical instances requiring isolation.  

---

### Standard Naming Formats we use in Organisation:

`[Environment]-[Platform]-[ServiceType]-[ComponentRole]-[ClientID]`  

---

### **Refined Component Breakdown:**  

#### **1. Platform (Unchanged)**  
- **WIN** → Windows  
- **LIN** → Linux  

#### **2. Environment (Unchanged)**  
- **P** → Production  
- **U** → UAT  
- **Q** → QA  
- **D** → Development  
- **T** → Training  

#### **3. Service Type (Broad functional category)**  
- **APP** → Application Server  
- **DBS** → Database Server  
- **WEB** → Web Server  
- **HDP** → Hadoop Platform  
- **DIR** → Directory Services (Active Directory, LDAP, etc.)  
- **FSR** → File Storage  

#### **4. Component Role (Specific function within the service type)**  
- **SRV** → General Server (if role isn't tier-specific)  
- **FRNT** → Frontend Server (for web-facing roles)  
- **BACK** → Backend Server (for app roles)  
- **PROC** → Processing Server (for batch jobs, etc.)  
- **DC** → Domain Controller (for directory services)  
- **NS** → Name Server (for DNS-related roles)  

---

### **Example Naming Conventions:**  

**Production Windows Web Frontend Server for Client 1:**  
`P-WIN-WEB-FRNT-C1`  

**Development Linux Application Backend Server for Client 2:**  
`D-LIN-APP-BACK-C2`  

**UAT Windows Database Server for Client 3:**  
`U-WIN-DBS-SRV-C3`  

**Training Linux Hadoop Processing Server:**  
`T-LIN-HDP-PROC`  

---

---

### **AWS EventBridge Overview**  
AWS EventBridge is a **serverless event bus** that helps applications to respond to system changes in **real-time**. It allows event-driven architectures by routing events from AWS services and custom applications to various targets like Lambda, SQS, and SNS.  

---

### **Key Features of EventBridge:**  
1. **Event-Driven Processing:**  
   - Responds to AWS resource state changes (e.g., EC2 instance state change, S3 object creation).  

2. **Scheduled Processing:**  
   - Runs tasks on a defined schedule using **cron expressions** or rate-based rules.  

3. **Triggers Both Scheduled & Event-Driven Actions:**  
   - Combines event-driven and scheduled invocations in a single workflow.  

---

### **EventBridge Example Event Structure**  

#### **Sample EC2 Instance State-Change Event:**  
```json
{
  "version": "0",
  "id": "eec4eda2-6639-e7b3-150d-c6461f1f0686",
  "detail-type": "EC2 Instance State-change Notification",
  "source": "aws.ec2",
  "account": "501170964283",
  "time": "2022-04-08T02:59:33Z",
  "region": "ap-south-1",
  "resources": [
    "arn:aws:ec2:ap-south-1:501170964283:instance/i-00f56eba78b7b4e65"
  ],
  "detail": {
    "instance-id": "i-00f56eba78b7b4e65",
    "state": "stopped"
  }
}
```

#### **Input Path Mapping Example:**  
To extract specific fields from the event and pass them to the target.  
```json
{
  "instance-id": "$.detail.instance-id",
  "state": "$.detail.state",
  "time": "$.time",
  "region": "$.region",
  "account": "$.account"
}
```

#### **Input Template Example:**  
Defines how the event details should be formatted before sending to a target.  
```text
"At <time>, Status of your EC2 instance <instance-id> in the AWS Region <region> has changed to <state>."
```

---

### **EventBridge Rule Types**  

#### **1. Event-Driven Rules:**  
Triggers an event when a specific action occurs in AWS services (e.g., EC2 instance stops, S3 object upload).  
- Example use cases:  
  - Trigger a Lambda function when an EC2 instance state changes.  
  - Send an SNS notification when an S3 file is uploaded.  

#### **2. Scheduled Rules (Crontab Format):**  
Runs periodically based on a defined schedule using **cron expressions or rate-based rules**.

---

### **AWS EventBridge Crontab Format**  

EventBridge cron expressions follow this syntax:

```
cron(Minutes Hours Day-of-Month Month Day-of-Week Year)
```

| Field          | Values                    | Wildcards        |
|----------------|---------------------------|------------------|
| Minutes        | 0–59                        | , - * /          |
| Hours          | 0–23                        | , - * /          |
| Day of Month   | 1–31                        | , - * ? / L W     |
| Month          | 1–12 or JAN-DEC              | , - * /          |
| Day of Week    | 1–7 or SUN-SAT                | , - * ? / L #     |
| Year           | 1970–2199 (optional)         | , - * /          |

---

### **Examples of EventBridge Cron Expressions:**  

| Cron Expression          | Meaning                                              |
|-------------------------|------------------------------------------------------|
| `cron(0 12 * * ? *)`      | Every day at 12 PM UTC                               |
| `cron(0 18 ? * MON-FRI *)`| Every weekday (Monday-Friday) at 6 PM UTC            |
| `cron(0 9 1 * ? *)`       | On the 1st day of every month at 9 AM UTC            |
| `cron(0 0 * * ? *)`       | Every day at midnight UTC                            |
| `cron(*/10 * * * ? *)`    | Every 10 minutes                                     |
| `cron(0 22 L * ? *)`      | Last day of every month at 10 PM UTC                 |

**Special Characters Explanation:**  

- `*` → Any value  
- `?` → No specific value (used in Day of Month or Day of Week fields)  
- `-` → Range (e.g., 1-5 for Monday to Friday)  
- `/` → Step values (e.g., */5 in Minutes field means every 5 minutes)  
- `L` → Last day of month/week  
- `#` → nth day of the month (e.g., 3#2 means the second Wednesday of the month)  

**Useful links for cron expressions:**  
- [AWS Scheduled Events](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html)  
- [EventBridge Cron Expressions](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-create-rule-schedule.html#eb-cron-expressions)

---

### **Common EventBridge Use Cases:**  

1. **Automating EC2 Actions:**  
   - Start/stop EC2 instances at specific times using scheduled rules.  

2. **Monitoring and Notifications:**  
   - Send an SNS alert when an IAM policy is modified.  

3. **Pipeline Automation:**  
   - Trigger a CodePipeline build when a new code commit is pushed.  

4. **Security Compliance:**  
   - Detect security group changes and log them to CloudWatch Logs.  

---

### **How to Set Up an EventBridge Rule (Steps)**  

1. **Go to AWS EventBridge in the AWS Console.**  
2. **Create a new rule:**  
   - Name: `EC2-State-Change`  
   - Event Source: `AWS Services` → `EC2`  
   - Event Pattern: Define JSON pattern for EC2 state changes.  
3. **Select Target:**  
   - Choose AWS Lambda, SNS, or SQS to process the event.  
4. **Define Input Transformer (Optional):**  
   - Use an input path and template to customize event data.  
5. **Enable Rule and Save.**  

---

### **EventBridge vs CloudWatch Events**  
AWS EventBridge is an evolved version of CloudWatch Events with additional features such as:  

| Feature               | EventBridge                      | CloudWatch Events             |
|----------------------|---------------------------------|-------------------------------|
| Third-party Integrations | Supports SaaS apps (e.g., Zendesk) | Limited AWS integrations only  |
| Schema Registry      | Yes                             | No                            |
| Input Transformation | Yes                             | No                            |
| Pricing              | Based on event ingestion        | Based on rule invocations     |

---
### **AWS Elastic Beanstalk Overview**  

**AWS Elastic Beanstalk (EB)** is a **Platform-as-a-Service (PaaS)** offering that allows developers to **deploy, manage, and scale applications** without worrying about the underlying infrastructure. It provides a simple way to host web applications by automating the provisioning of AWS resources such as EC2, ELB, Auto Scaling, and RDS.

---

### **Why Do We Use AWS Elastic Beanstalk?**  

Elastic Beanstalk is primarily used for:  

1. **Quick Deployment:**  
   - Developers can focus on writing code while AWS handles deployment, scaling, and monitoring.  
   
2. **Managed Infrastructure:**  
   - AWS provisions and manages resources like EC2 instances, Elastic Load Balancers (ELB), and Auto Scaling Groups (ASG) automatically.  

3. **Support for Multiple Languages:**  
   - It provides preconfigured environments for popular programming languages, including:  
     - Python  
     - Java  
     - Go  
     - Ruby  
     - PHP  
     - .NET  

4. **Automatic Scaling:**  
   - Beanstalk automatically scales applications based on demand by adjusting EC2 instances using Auto Scaling.  

5. **Built-in Monitoring:**  
   - Provides built-in integration with **Amazon CloudWatch** for application and infrastructure monitoring.  

6. **Environment Management:**  
   - Supports different environments (development, staging, production) with easy rollbacks and updates.  

7. **Integration with AWS Services:**  
   - Easily integrates with **RDS, S3, DynamoDB, CloudWatch, and IAM**, making it a convenient choice for full-stack applications.  

8. **Zero Cost for Elastic Beanstalk Service:**  
   - You only pay for the underlying AWS resources (EC2, ELB, S3, etc.), while Beanstalk itself is free.  

---

### **How AWS Elastic Beanstalk Works**  

1. **Upload Code:**  
   - Developers upload their application code via the AWS Management Console, CLI, or CI/CD pipelines.  

2. **Environment Creation:**  
   - Beanstalk provisions necessary resources like EC2 instances, security groups, databases, and more.  

3. **Deployment & Scaling:**  
   - Automatically handles deployment and adjusts resources based on load.  

4. **Monitoring & Logging:**  
   - Provides health checks, logging, and monitoring to track performance and failures.  

5. **Application Updates:**  
   - Developers can easily push new code updates without downtime using rolling or immutable deployments.  

---

### **Limitations of AWS Elastic Beanstalk**  

1. **Limited OS-Level Customizations:**  
   - Elastic Beanstalk provides limited access to the underlying OS, making it challenging to install custom software or dependencies outside the predefined platform.  

2. **Single Application Per Environment:**  
   - Each Elastic Beanstalk environment supports only one application, which can be a limitation for microservices-based architectures.  

3. **Less Control Over Infrastructure:**  
   - Since AWS manages most of the infrastructure, it might not be suitable for applications requiring fine-grained infrastructure control.  

4. **Potential Vendor Lock-In:**  
   - Applications tightly coupled with AWS services may face migration challenges to other cloud platforms.  

---

### **When to Use AWS Elastic Beanstalk?**  

You should consider using AWS Elastic Beanstalk when:  

- You need a **fast and easy way to deploy web applications** without infrastructure management.  
- You prefer AWS to **handle resource provisioning and scaling automatically.**  
- Your application is **compatible with one of the supported programming languages.**  
- You want to focus more on development rather than infrastructure management.  
- You are running **monolithic applications** and don’t need advanced microservices architectures.  

---

### **Additional Key Points About Elastic Beanstalk**  

- **Environment Types:**  
  - **Web Server Environment:** Handles HTTP/S requests with ELB and Auto Scaling.  
  - **Worker Environment:** Asynchronous background processing using Amazon SQS.  

- **Infrastructure Customization via `.ebextensions`:**  
  - YAML/JSON-based configuration files allow customizing resources such as instance types, security groups, and environment variables.  

- **CI/CD Integration:**  
  - Elastic Beanstalk can be integrated with GitHub Actions, AWS CodePipeline, Jenkins, etc. for automated deployments.  

- **Multi-AZ Deployments:**  
  - Applications can be deployed across multiple AWS availability zones for high availability.  

---
**Instance Isolation in AWS**  

AWS provides different tenancy options to ensure instance isolation based on security, compliance, and performance needs. The two primary tenancy options are **Shared Tenancy** and **Dedicated Tenancy**, which further includes **Dedicated Instances** and **Dedicated Hosts.**  

---

### **1. Shared Tenancy (Default Option)**  
- **Definition:**  
  In shared tenancy, your EC2 instance runs on physical hardware that is shared with other AWS customers.  
- **Key Points:**  
  - Cost-effective as you pay only for your instance usage.  
  - AWS manages the physical hardware and ensures isolation using virtualization.  
  - Suitable for most workloads that do not have strict compliance or licensing requirements.  
- **Use Cases:**  
  - General-purpose applications.  
  - Web applications, test environments, and microservices that do not require dedicated resources.  

---

### **2. Dedicated Tenancy (Enhanced Isolation)**  

Dedicated tenancy ensures that your instances run on hardware dedicated only to your AWS account, enhancing security and compliance. It comes in two variants:  

#### **a. Dedicated Instances**  
- **Definition:**  
  AWS provides instances that run on dedicated physical servers, but you don't have control over the underlying hardware management.  
- **Key Points:**  
  - Isolation from other AWS customers.  
  - AWS manages hardware allocation.  
  - Billing is per instance, with an additional charge for dedicated tenancy.  
  - No visibility into physical resource details.  
- **Use Cases:**  
  - Applications requiring regulatory compliance (e.g., HIPAA, PCI-DSS).  
  - Enhanced security needs.  
  - Workloads where shared resources are not allowed.  

#### **b. Dedicated Hosts**  
- **Definition:**  
  Provides a physical EC2 server fully dedicated to your account, giving you complete control over instance placement and allowing software license optimization.  
- **Key Points:**  
  - Enables control over instance placement on the physical host.  
  - Helps meet strict licensing requirements (e.g., Oracle, Windows Server).  
  - Supports Bring Your Own License (BYOL) models.  
  - Visibility into hardware attributes such as host ID, sockets, and cores.  
- **Use Cases:**  
  - Applications with **strict compliance and licensing** needs.  
  - Software requiring **per-core or per-socket** licensing (e.g., SQL Server, SAP).  
  - Workloads needing high security and physical separation.  

---

### **Comparison of Shared Tenancy vs. Dedicated Instances vs. Dedicated Hosts**

| Feature             | Shared Tenancy             | Dedicated Instances          | Dedicated Hosts              |
|--------------------|---------------------------|------------------------------|------------------------------|
| Cost               | Lowest                     | Higher (instance-level pricing) | Highest (per host pricing)     |
| Isolation Level    | Virtualized Isolation      | Physical Isolation             | Complete Physical Isolation  |
| Hardware Control   | No                         | No                             | Yes                           |
| Licensing Options  | AWS-provided only          | Limited BYOL options           | Full BYOL support             |
| Use Case Example   | Web applications           | Regulated industries            | Specialized workloads         |
| Billing            | Per instance               | Per instance + dedicated charge | Per host (flat rate)          |

---

### **How to Choose the Right Tenancy Option?**  

Choose based on:  

- **Security and Compliance:** If strict compliance is needed, go for **Dedicated Hosts.**  
- **Cost Sensitivity:** Use **Shared Tenancy** for cost efficiency.  
- **Licensing Needs:** If running licensed software, prefer **Dedicated Hosts.**  
- **Performance Isolation:** Use **Dedicated Instances** for workloads that require isolated hardware.  

---
