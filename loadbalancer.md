
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

