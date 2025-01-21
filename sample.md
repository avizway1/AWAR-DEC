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
### **Task: Application Load Balancer with Multiple Target Groups**  

#### **Objective:**  
Create an Application Load Balancer (ALB) to deliver multiple applications using separate target groups on port 80 and port 8080.  

#### **Requirements:**  
1. **Launch EC2 Instances:**  
   - Launch **two EC2 instances**, install and configure Apache web server to serve content on **port 80**, and register them to **Target Group A**.  
   - Launch **one EC2 instance**, configure it to serve content on **port 8080**, and register it to **Target Group B**.  

2. **Create an Application Load Balancer:**  
   - Configure the ALB to route traffic based on port numbers to the corresponding target groups.  
   - Ensure the ALB has appropriate security group rules to allow HTTP traffic on both ports.  

3. **Target Group Configuration:**  
   - Target Group A should listen on **port 80** and forward requests to the two Apache instances.  
   - Target Group B should listen on **port 8080** and forward requests to the single instance.  

4. **Testing:**  
   - Access the ALB DNS name via a web browser and confirm that both applications are accessible via:  
     - `http://<ALB-DNS>` → Should serve content from the instances in Target Group A.  
     - `http://<ALB-DNS>:8080` → Should serve content from the instance in Target Group B.  

---

**Expected Deliverables:**  
- EC2 instances running and serving content.  
- ALB properly configured to forward traffic to the appropriate target groups.  
- Validation screenshots showing application accessibility through the ALB.  

---

### **AWS Task Questions Format**  

---

#### **Task 1: Configure Pipeline Mechanism Between EC2 Instances and ELB**  

**Objective:**  
Set up a load balancer to serve traffic only through the ELB, ensuring direct instance access is restricted.  

**Requirements:**  
1. **Security Group Configuration:**  
   - Modify the EC2 instance security group to allow port 80 traffic only from the ELB security group.  

2. **Access Testing:**  
   - Verify that accessing the instance directly via its IP does **not** serve the webpage.  
   - Ensure that accessing the application via the ELB DNS name works correctly.  


---

#### **Task 2: Create an Auto Scaling Group (ASG) and Set Desired Count**  

**Objective:**  
Deploy an Auto Scaling Group with a defined desired count of instances and verify its functionality.  

**Requirements:**  
1. **Auto Scaling Group Setup:**  
   - Create an ASG and set the desired capacity to **2** instances.  

2. **Verification:**  
   - Confirm that two instances are launched and running as expected.  

3. **Cleanup:**  
   - Ensure the Auto Scaling Group is deleted after testing to avoid unnecessary costs.  


---

#### **Task 3: Create an ASG Using a V1 Launch Template with Scaling Policies**  

**Objective:**  
Create an Auto Scaling Group with a launch template and configure scaling policies.  

**Requirements:**  
1. **Launch Template Creation:**  
   - Create a V1 launch template.  
   - Set the desired capacity to **2** instances.  
   - Deploy and verify the instances.  

2. **Scaling Policies:**  
   - Configure an alarm to reduce desired capacity to **1** instance when CPU utilization is ≤10%.  

3. **Scheduled Scaling:**  
   - Configure a scheduled action to increase the desired capacity to **3** instances at a specified time.  

4. **Verification:**  
   - Monitor and confirm automatic scaling behavior based on conditions and schedules.  

**Expected Deliverables:**  
- Auto Scaling Group with applied scaling policies and scheduled actions.  
- Observations on scaling adjustments based on alarms and schedules.  

---

#### * Task: Load Testing with Stress Command**  

**Objective:**  
Simulate high CPU usage on EC2 instances to observe Auto Scaling behavior.  

**Steps:**  
1. Run the stress command (Check the number of CPU cores using "nproc" command): 
 
   ```bash
   stress --cpu 1 --timeout 900
   ``` 
   
3. Observe scaling behavior based on increased load.  

**Expected Deliverables:**  
- System metrics showing CPU utilization.  
- Observations on scaling responses under load.  

---
