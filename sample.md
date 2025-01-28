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

---

### **Task 1: Launch an EC2 Instance Using CLI**
**Objective:** Launch an EC2 instance with the following parameters using the AWS CLI:  
- AMI ID  
- Instance Type  
- Subnet ID  
- Security Group ID  
- Key Pair  
- Number of instances  

**Expected Steps:**  
1. Use the `aws ec2 run-instances` CLI command.  
2. Pass all required parameters (`--image-id`, `--instance-type`, `--subnet-id`, `--security-group-ids`, `--key-name`, `--count`).  
3. Verify the instance launch by checking its status using `describe-instances`.

---

### **Task 2: Automate Web Server Setup Using User Data and S3**
**Objective:** Set up an EC2 instance as a web server, download web content (index.html and status.html) from S3, and serve it using Apache.  

**Instructions:**  
1. **Create the S3 Bucket:**  
   - Upload `index.html` and `status.html` to the bucket.  

2. **Launch EC2 Instance:**  
   - Use the below userdata to pass the following script while launching the instance:  
     ```bash
     #!/bin/bash
     yum install httpd -y
     service httpd start
     chkconfig httpd on
     //Frame the command here as a task and try.
     ```

3. Verify the setup:  
   - Access the public IP or domain of the instance to check if the web server is running and serving the files.

---

### **Task 3: Create IAM Users and Test AWS CLI Profiles**
**Objective:** Create two IAM users with specific permissions and test them using the AWS CLI.  

1. **Create IAM Users:**  
   - `user1`: Grant **S3 Full Access**.  
   - `user2`: Grant **IAM Full Access**.  

2. **Generate Access Keys:**  
   - For each user, generate the **Access Key** and **Secret Key**.  

3. **Configure CLI Profiles on Your Laptop:**  
   - Use the `aws configure --profile <profile-name>` command to set up two profiles (`user1-profile` and `user2-profile`).  

4. **Test User Permissions:**  
   - Log in using each profile:  
     - **User1:** Try creating an S3 bucket (`aws s3 mb`).  
     - **User2:** Try creating an IAM user (`aws iam create-user`).  
   - Verify that each user has the expected permissions and no access beyond what is granted.  

---

### **Task 4: Use the `aws s3 sync` Command for Incremental Updates from S3 to EC2**

**Objective:** Test incremental synchronization of web content between an S3 bucket and an EC2 instance using the `aws s3 sync` command.

**Instructions:**  
1. **Prepare the S3 Bucket:**  
   - Add the initial set of files (e.g., `index.html` and `status.html`) to your S3 bucket.  

2. **Launch an EC2 Instance and configure Web Server Setup:**  
	- use Sync command and sync data from s3 bucket to /var/www/html/ path. 

3. **Test Incremental Updates:**  
   - Add a new file (e.g., `about.html`) or modify an existing file (e.g., `index.html`) in the S3 bucket.  
   - Use the `aws s3 sync` command on the EC2 instance to pull only the updated or new files to `/var/www/html/`.  
     ```bash
     aws s3 sync s3://<bucket-name>/ /var/www/html/
     ```

4. **Verify Updates:**  
   - Access the public IP or domain of the EC2 instance in your browser to confirm that the changes are reflected on the web server.

---


### **Task 5: Automate S3 to EC2 Synchronization Using a Cron Job**

**Objective:** Set up a cron job on an EC2 instance to automate regular synchronization of web content from an S3 bucket to the web server directory.

---

**Instructions:**  
1. **Launch an EC2 Instance and Configure Web Server:**  
   - Launch an EC2 instance and install Apache:  
   - Verify that the web server is running.

2. **Set Up the Initial Synchronization:**  
   - Manually run the `aws s3 sync` command to pull the initial content from the S3 bucket (you can use task 4 web content) to `/var/www/html/`:  
     ```bash
     aws s3 sync s3://<bucket-name>/ /var/www/html/
     ```

3. **Install `crontab`:**  
   - Ensure the `cron` package is installed and enabled on your EC2 instance:  
     ```bash
     yum install cronie -y
     service crond start
     chkconfig crond on
     ```

4. **Create a Cron Job for Regular Synchronization:**  
   - Open the crontab editor:  
     ```bash
     crontab -e
     ```
   - Add the following entry to synchronize every 2 minutes:  
     ```bash
     */2 * * * * aws s3 sync s3://<bucket-name>/ /var/www/html/
     ```

5. **Test the Automation:**  
   - Add or update files in the S3 bucket and wait for the cron job to trigger.  
   - Verify that the changes are reflected on the web server by accessing the instance's public IP or domain.

---
