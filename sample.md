---

### **Task 1: EC2 Instance and Volume Management**  
1. Launch an EC2 instance in the **ap-south-1a** Availability Zone (AZ).  
2. Create a new **EBS volume** with a size of **1 GB** in the **ap-south-1a** AZ.  
3. Attach the volume to the EC2 instance and make it available at the operating system level.  
4. Write some data to the volume.  
5. Using the AWS Management Console, **increase the volume size to 2 GB**.  
6. Reflect the new size (2 GB) at the operating system level.  
7. Write additional data to confirm the changes.  

---

### **Task 2: Sharing EBS Volume Data Across Instances**  
1. Launch another EC2 instance in the **ap-south-2a** AZ.  
2. Transfer the data from the **2 GB volume** (attached to the instance in **ap-south-1a**) to the newly launched EC2 instance in **ap-south-2a**.  
3. Ensure the volume is made available and accessible from the **1b instance** in the new AZ.  

---

### **Task 3: Learn Amazon DLM Use Cases**  
1. Read the AWS blog article:  
   [Automating Amazon EBS Snapshot and AMI Management Using Amazon DLM](https://aws.amazon.com/blogs/storage/automating-amazon-ebs-snapshot-and-ami-management-using-amazon-dlm/).  
2. Understand the scenarios and use cases for **Amazon Data Lifecycle Manager (DLM)**.  

--- 
### AWS Task Questions Format  

---

#### **Task 1**: **Linux EC2 Instance Setup with Web Server and Custom Configuration**  
1. **Launch a Linux EC2 Instance**:  
   - Select the appropriate AMI and instance type.  
   - Configure security group rules to allow HTTP/HTTPS traffic.  
2. **Web Server Setup**:  
   - Install and configure a web server (e.g., Apache or Nginx).  
   - Add custom webpages and verify their accessibility via the public IP.  
3. **Volume Association**:  
   - Create a 2GB EBS volume.  
   - Attach the volume to the instance.  
   - Format, mount, and configure it for permanent mounting.  
4. **Golden AMI Creation**:  
   - Create an AMI of the configured instance.  
5. **Test Golden AMI**:  
   - Launch a new instance from the created AMI.  
   - Verify the web server and custom configurations are intact.  

---

#### **Task 2**: **Windows EC2 Instance Customization and Testing**  
1. **Launch a Windows EC2 Instance**:  
   - Select the appropriate AMI and instance type.  
   - Configure security group rules to allow RDP traffic.  
2. **Connect to the Instance**:  
   - Retrieve and decrypt the administrator password.  
   - Connect using an RDP client.  
3. **Perform Customizations**:  
   - Change the administrator password.  
   - Change the desktop wallpaper.  
   - Install PuTTY software.  
   - Install IIS and configure a custom webpage.  
4. **Golden AMI Creation**:  
   - Stop the instance and create an AMI.  
5. **Test Golden AMI**:  
   - Launch a new instance from the created AMI.  
   - Verify the customizations are preserved.  

---

#### **Task 3**: **Setup Password Authentication for EC2-User**  
1. Follow the steps in the provided [guide](https://comtechies.com/password-authentication-aws-ec2.html):  
   - Enable password authentication in the SSH configuration file.  
   - Restart the SSH service.  
   - Set a password for the `ec2-user`.  
2. Verify that password authentication works as expected.  

---
