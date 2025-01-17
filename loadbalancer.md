
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
   - **Algorithms**:
     - Round robin.
     - Least outstanding requests.
     - IP hash method.
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

---

### Load Balancing Algorithms (Application and Network ELBs)
**1. Round Robin**  
   - **How it works**: Requests are distributed equally among all targets (e.g., EC2 instances) in a target group.  
   - **Best suited for**: Scenarios where all targets have equal capacity and performance.

**2. Least Outstanding Requests**  
   - **How it works**: Requests are sent to the target with the fewest outstanding requests.  
   - **Best suited for**: Workloads with long-running requests, ensuring that no single target becomes overloaded.

**3. IP Hash Method**  
   - **How it works**: Requests from the same client IP are consistently routed to the same target.  
   - **Best suited for**: Applications that require session persistence (e.g., shopping carts, login sessions).

**4. Flow Hash (Network ELB)**  
   - **How it works**: Uses a combination of source IP, destination IP, source port, and destination port to route traffic.  
   - **Best suited for**: Optimizing traffic distribution across highly dynamic environments.


---

#### **Free Tier**
- ELB offers **750 hours/month** under the free tier.

