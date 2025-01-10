#### **Package Management**

---

### **1. RPM (RedHat Package Manager):**
- **Purpose:** Manages installation, updates, and removal of software packages on RedHat-based systems.
- **Features:**
  - Does not resolve dependencies automatically.
  - Requires downloading and managing dependencies manually.
  
- **Commands:**
  - Install a package:  
    ```bash
    rpm -ivh package.rpm
    ```
  - Update a package:  
    ```bash
    rpm -Uvh package.rpm
    ```
  - Remove a package:  
    ```bash
    rpm -e package_name
    ```

---

### **2. YUM (Yellowdog Updater Modified):**
- **Purpose:** A wrapper around RPM that automatically resolves dependencies and retrieves packages from repositories.

- **Features:**
  - Resolves dependencies.
  - Retrieves packages from local/global repositories.
  - Enables automatic updates.
   
- **Commands:**
  - Update all packages:  
    ```bash
    yum update
    ```
  - Install a package:  
    ```bash
    yum install package_name
    ```
  - Search for a package:  
    ```bash
    yum search keyword
    ```
  - Remove a package:  
    ```bash
    yum remove package_name
    ```

---

### **3. DNF (Dandified YUM):**
- **Purpose:** The modern package manager that replaces `YUM` in newer Linux distributions, including **Amazon Linux 2023**. 

- **Features:**
  - Faster dependency resolution than YUM.
  - Plugin-based architecture.
  - Supports rollback of transactions.
  - Enhanced handling of large data sets.
  - Secure and efficient.
  
- **Commands:**
  - Install a package:  
    ```bash
    dnf install package_name
    ```
  - Update all packages:  
    ```bash
    dnf update
    ```
  - Remove a package:  
    ```bash
    dnf remove package_name
    ```
  - Search for a package:  
    ```bash
    dnf search keyword
    ```
  - View installed packages:  
    ```bash
    dnf list installed
    ```
  - Enable a repository:  
    ```bash
    dnf config-manager --set-enabled repository_name
    ```

---

- **Repository Configuration:**  
  - Files located in `/etc/yum.repos.d/` or `/etc/dnf/dnf.conf` contain information about enabled repositories.

#### **1. Repository Location:**
-  /etc/yum.repos.d/*.repo` Contains `.repo` configuration files.

---

### **Package Installation Examples**

#### **Apache Installation:**
1. Search for Apache:  
   ```bash
   dnf search httpd
   ```
2. Get information about Apache:  
   ```bash
   dnf info httpd
   ```
3. Install Apache:  
   ```bash
   dnf install httpd
   ```
4. Start and enable Apache:  
   ```bash
   systemctl start httpd  (0r) Service httpd start
   systemctl enable httpd (or) chkconfig httpd on
   ```

---

## **Process Management**

### Identifying and Managing Process IDs (PIDs) in Linux

#### **What is a PID?**
- A PID (Process ID) is a unique identifier assigned by the operating system to each running process.

---

#### **Commands to Identify PIDs and Manage Processes**

1. **View Background and Suspended Jobs:**
   - `jobs`: Displays all background and suspended processes in the current shell.

2. **View the Process Tree:**
   - `pstree`: Shows the process tree in a hierarchical structure.
   - `pstree | less`: Use with `less` to view the process tree page by page.

3. **List Running Processes:**
   - `ps`: Displays processes running in the current terminal.
   - `ps aux`: Lists all running processes across the system in a detailed format.
   - `ps faux`: Displays the process tree along with detailed process information.

4. **Real-Time Process Monitoring:**
   - `top`: Displays a continuously updating list of running processes, their CPU, memory usage, etc. Press `z` for a colorized view.

5. **Quit from any Continuous Process View:**
   - Press `q` to exit from commands like `top`.

---

#### **System and Memory Information**

1. **Check System Uptime:**
   - `uptime`: Provides the time since the system was last booted, along with load averages.

2. **Check Free Memory:**
   - `free`: Displays memory usage statistics.
   - `free -h`: Displays memory usage in a human-readable format.

---

#### **Killing a Process**
1. **Terminate a Process by PID:**
   - `kill PID`: Terminates the process with the specified PID.

For example:
   ```
   ps aux | grep some-process
   kill 1234  # Replace 1234 with the actual PID of the process.
   ```
