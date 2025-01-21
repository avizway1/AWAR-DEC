
#### **Vertical Scaling**
- **Definition**: Increasing resources (CPU, memory, storage) of an instance by upgrading its instance type (e.g., from `t2.micro` to `t3.medium`).
- **Process in AWS**:
  1. Stop the EC2 instance.
  2. Modify the instance type in the AWS Management Console or CLI.
  3. Start the instance again.
- **Note**: Ensure compatibility of your application with the new instance type.

### Horizontal Scaling  
- **Definition**: Instead of upgrading a single instance (vertical scaling), horizontal scaling adds more instances to distribute the load.  
- **Key Features**:
  - No downtime: Instances can be added or removed without stopping existing ones.
  - Fault tolerance: If one instance fails, traffic is redistributed among the remaining instances.
  - Scalability: Applications can handle an increasing number of requests effectively.  
- **Implementation in AWS**:
  - Use **Auto Scaling Groups (ASG)** with **Load Balancers (ALB or NLB)** to dynamically add/remove instances based on predefined metrics (e.g., CPU utilization, request count).


---

### Comparison: Horizontal vs. Vertical Scaling
| Aspect                   | Horizontal Scaling                     | Vertical Scaling                     |
|--------------------------|-----------------------------------------|---------------------------------------|
| Resource Addition        | Adds more instances                    | Increases capacity of a single instance |
| Downtime                 | None                                   | Instance must be stopped and restarted |
| Scalability              | Unlimited (theoretically)              | Limited by hardware capacity          |
| Cost                     | Scales with number of instances        | Increased for high-capacity instances |
| Use Case                 | High availability, fault tolerance     | Quick upgrades for small applications |

---



#### **Security Group Best Practices**
- Avoid using the **same security group** for your EC2 instance and Load Balancer to minimize the risk of misconfigurations and ensure better isolation.

---

#### **User Data for Web Servers**
**First Web Server:**
```bash
#!/bin/bash
yum install httpd -y
service httpd start
chkconfig httpd on
echo "<h1>This is my first webserver</h1>" > /var/www/html/index.html
```

**Second Web Server:**
```bash
#!/bin/bash
yum install httpd -y
service httpd start
chkconfig httpd on
echo "<h1>This is my Second webserver</h1>" > /var/www/html/index.html
```

---
#### **Key Features by ELB Type**
| Feature                   | Application ELB     | Network ELB          | Gateway ELB         |
|---------------------------|---------------------|----------------------|---------------------|
| Protocols                 | HTTP, HTTPS         | TCP, UDP, TLS        | GENEVE              |
| IP Assignment             | No dedicated IP     | Supports dedicated IP| Not applicable      |
| Routing                   | Path and Host-based | Flow Hash Algorithm  | Security Appliances |
| Performance               | High but not for millions | Millions of requests/sec | -

---

#### **Elastic Load Balancer (ELB) Overview**
1. **Classic Load Balancer (CLB)**:
   - **Layer 4/7**: Supports TCP, UDP, HTTP, and HTTPS.
   - **Status**: Outdated and not recommended for new applications.

2. **Application Load Balancer (ALB)**:
   - **Layer 7**: Handles HTTP and HTTPS traffic.
   - **Use Case**: Ideal for modern applications with microservices or path-based routing.
   - **Supports**:
     - Path-based routing.
     - Host-based routing.
     - WebSocket.
     - Load balancing for containerized applications.
   - **DNS Endpoint**: Provided for connectivity (no dedicated IP).

3. **Network Load Balancer (NLB)**:
   - **Layer 4**: Handles TCP, UDP, and TLS traffic.
   - **Use Case**: Suitable for high-performance, low-latency workloads (e.g., millions of requests/second).
   - **Supports**:
     - Static IP addresses.
     - Flow Hash algorithm.
   - **Dedicated IP**: Can be assigned.

4. **Gateway Load Balancer (GLB)**:
   - **Protocol**: GENEVE.
   - **Use Case**: Designed for third-party virtual appliances (e.g., firewalls, intrusion detection systems).

---

#### **Target Groups**
- Define a group of targets (e.g., EC2 instances, Lambda functions) for an ELB to route requests.
- **Listener Rules**: Conditions based on hostnames, paths, or headers to forward traffic to the appropriate target group.

---

#### **Best Practices for ELB**
- **Availability**: Use **at least two subnets** in different Availability Zones (AZs) for higher availability.
- **Access Logs**: Enable ELB logging to track traffic details. Logs are stored in an S3 bucket.

---

### Application Load Balancing Algorithms

---

**1. Round Robin**  
   - **How it works**: Requests are distributed equally among all targets (e.g., EC2 instances) in a target group.  
   - **Best suited for**: Scenarios where all targets have equal capacity and performance. 

---

**2. Least Outstanding Requests**  
   - **How it works**: Requests are sent to the target with the fewest in-progress tasks or outstanding requests.  
   - **Best suited for**: Workloads with long-running requests, ensuring that no single target becomes overloaded.

---

### **3. Weighted Random**  
- **How it Works**: Distributes requests randomly across healthy targets based on assigned weights.  
  - **Weights**: Determine the proportion of traffic each target should receive.  
  - **Anomaly Detection**: Identifies issues with targets, and traffic is adjusted accordingly.  
  - **Anomaly Mitigation**: With **Automatic Target Weights (ATW)** enabled, target weights are automatically adjusted to handle anomalies.  

---

### **Comparison of Algorithms**

| **Algorithm**           | **Best For**                              | **Advantages**                          | **Limitations**                          |
|--------------------------|-------------------------------------------|------------------------------------------|------------------------------------------|
| **Round Robin**          | Uniform workloads                        | Simple and predictable                  | Not effective for variable workloads     |
| **Least Outstanding**    | Varying workload complexities            | Dynamic and responsive                  | Not compatible with Slow Start Duration  |
| **Weighted Random**      | Adaptive distribution for varying targets| Fault-tolerant, supports anomalies      | Requires additional configuration        |

---

### **AWS Network Load Balancer (NLB) Algorithm**

---

- **Flow Hash Algorithm**:  
  The NLB uses the **Flow Hash Algorithm** to determine how traffic is distributed across targets.  
  - It examines network attributes such as the **source IP address**, **destination IP address**, **protocol**, and **source/destination port numbers**.  
  - A hash is calculated based on these attributes, and traffic is routed consistently to the same target for a given connection (unless the target becomes unhealthy).
---

#### **Free Tier**
- ELB offers **750 hours/month** under the free tier.
  
---
### **What is Stickiness in AWS Load Balancers?**

Stickiness, also known as **session persistence**, ensures that a client’s requests are consistently routed to the same target (e.g., an EC2 instance) for the duration of a session. 

AWS Elastic Load Balancers (ELB) support stickiness for **Application Load Balancers (ALB)** using either cookies or custom configurations to track sessions.

---

### **How Stickiness Works**
1. **Cookie-Based Mechanism**:  
   - A cookie is issued to the client by the load balancer or application.  
   - This cookie tracks the session and ensures the client’s subsequent requests are routed to the same target.

2. **Duration Control**:  
   - Stickiness can be configured for a specific time duration.  
   - Once the duration expires, the client may be routed to a different target.

3. **Load Balancer Types**:  
   - **ALB**: Uses **application-controlled** cookies or **load-balancer-generated** cookies for stickiness.  

---

### **Use Cases of Stickiness**
1. **Session-Specific Applications**:  
   - **Example**: Online shopping carts or e-commerce sites.  
   - Ensures user-specific data, such as items in a cart, stays intact by routing all requests to the same backend server.

2. **Applications with In-Memory Data**:  
   - **Example**: Gaming or financial trading applications.  
   - Targets maintain session-specific data in memory, which avoids reloading from a database.

3. **User Authentication**:  
   - **Example**: Social media or enterprise web apps with user authentication.  
   - Keeps users authenticated without the need to share session data across multiple targets.

---

### **Advantages of Stickiness**
- Improves **user experience** by maintaining session continuity.
- Reduces **backend complexity** in handling session data.

---

### **Auto Scaling Group (ASG) Overview**
ASG helps automatically adjust the number of EC2 instances to maintain application availability and optimize costs. It works with different scaling policies to handle workload variations.

---

### **Steps to Set Up an ASG**

1. **Create a Golden AMI:**  
   - Launch an EC2 instance, install required software and configurations.  
   - Create an AMI (Amazon Machine Image) from the configured instance.  
   - This AMI will be used to launch multiple instances.

2. **Create an Elastic Load Balancer (ELB):**  
   - Create an **Application Load Balancer (ALB)** or **Network Load Balancer (NLB)**.  
   - Register target groups to distribute traffic across EC2 instances, that we launch in next steps.  
   - Ensure health checks are properly configured.

3. **Create an Auto Scaling Group (ASG):**  
   - **Step 1:** Create a **Launch Template** with:  
     - The Golden AMI.  
     - Instance type (e.g., `t2.micro`).  
     - Security Group.  
     - Key pair for SSH access.  
   - **Step 2:** Configure ASG:  
     - Attach ELB to distribute traffic.  
     - Set the desired, minimum, and maximum instance counts.  
     - Define scaling policies (manual, scheduled, or dynamic).

---

### **ASG Scaling Policies**

1. **Dynamic Scaling:** Automatically adjusts the number of instances based on real-time metrics.  
   - **Types:**  
     - **Step Scaling:** Adds/removes instances based on threshold values.  
     - **Simple Scaling:** Adds/removes instances based on a CloudWatch alarm trigger.  
     - **Target Tracking Scaling:** Maintains a specific metric target (e.g., CPU utilization at 50%).  

2. **Scheduled Scaling:** Adds/removes instances at specific times (e.g., scale up at 9 AM, scale down at 6 PM).  

3. **Manual Scaling:** Manually change the desired capacity at any time.  

---

### **Scale In vs. Scale Out**

- **Scale Out:** Adds instances to ASG when demand increases.  
- **Scale In:** Removes instances when demand decreases.  

---

### **ASG Termination Policy (How ASG Chooses Instances to Terminate)**

When a **Scale-In** action is triggered, ASG follows these policies in order:

1. **Default Termination Policy (Recommended)**  
   - Chooses instances from the oldest launch template/configuration.  
   - Then selects the instance closest to the next billing hour to reduce cost.  
   - Lastly, evenly distributes instances across Availability Zones (AZs).

2. **Specific Termination Policies (Can be set by the user):**  
   - **OldestInstance:** Terminates the oldest running instance.  
   - **NewestInstance:** Terminates the most recently launched instance.  
   - **OldestLaunchTemplate:** Removes instances created with older launch templates.  
   - **Availability Zone Rebalancing:** Terminates instances to maintain balance across AZs.  
   - **ClosestToBillingHour:** Selects instances that are about to reach a full billing hour.

---

### **Upgrading Instance Type with Zero Downtime (e.g., from `t2.micro` to `t2.nano`)**

#### Steps to perform instance upgrade:

1. **Create a New Launch Template:**  
   - Use the existing Golden AMI.  
   - Change the instance type from `t2.micro` to `t2.nano`.  

2. **Update ASG with New Launch Template:**  
   - Edit the ASG and associate the new launch template.  
   - Set the **desired capacity to 2** (to create new instances without downtime).

3. **Terminate the Old Instances Gradually:**  
   - ASG will automatically launch new instances with the updated settings.  
   - Once new instances are healthy, terminate the old ones manually or let ASG handle it.

---

### **Best Practices for ASG**
- Use **Target Tracking** for automated scaling based on metrics like CPU usage.  
- Distribute instances across multiple AZs for high availability.  
- Implement **termination policies** carefully to avoid unintended instance terminations.  
- Enable **ELB health checks** to ensure only healthy instances receive traffic.  
- Monitor ASG activities using **CloudWatch alarms** and logs.

---

### **What is the Cooldown Period in Auto Scaling Groups (ASG)?**  

The **cooldown period** in an Auto Scaling Group (ASG) is a waiting time after a scaling activity (scale in or scale out) to allow the system to stabilize before triggering another scaling action.  

During this period, ASG temporarily **pauses scaling actions** to prevent unnecessary scale-ins or scale-outs due to transient spikes in metrics like CPU utilization.  

---

### **How the Cooldown Period Works:**
1. The ASG triggers a scaling activity (e.g., adds an instance due to high CPU usage).  
2. The cooldown period starts (e.g., 300 seconds).  
3. During this period, ASG ignores further scaling triggers to allow the system to stabilize.  
4. Once the cooldown period expires, ASG resumes normal monitoring and responds to new scaling triggers.  

---

### **Example Scenario:**
Imagine an ASG scaling policy to scale out when CPU usage exceeds 70%.  
- ASG launches an additional instance.  
- A 300-second cooldown is applied.  
- During the cooldown, even if CPU crosses 70% again, no new instance will be launched.  
- After 300 seconds, ASG evaluates the CPU usage again and acts accordingly.  

---

### **Use Case for Cooldown Period**
- **Prevent rapid fluctuations (flapping):** Avoid launching and terminating instances too quickly due to metric spikes.  
- **Handling slow-start applications:** If your app takes time to boot up, a longer cooldown period allows it to stabilize before another action is taken.  
- **Optimizing cost:** Prevent unnecessary scaling actions that might increase costs.  
