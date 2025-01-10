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

### **How to Add a Repository**
Repositories in Linux are sources where packages are stored and managed.

- **Repository Configuration:**  
  - Files located in `/etc/yum.repos.d/` or `/etc/dnf/dnf.conf` contain information about enabled repositories.

#### **1. Repository Location:**
- On **Amazon Linux 2023** and other RPM-based distributions:  
  `/etc/yum.repos.d/*.repo`  
  - Contains `.repo` configuration files.

#### **2. EPEL Repository Installation:**
- **Amazon Linux 2 (YUM):**
  ```bash
  sudo amazon-linux-extras install epel -y
  ```
- **Amazon Linux 2023 (DNF):**
  ```bash
  sudo dnf install epel-release -y
  sudo dnf config-manager --set-enabled epel
  ```
- Verify the repository:  
  ```bash
  dnf repolist
  ```

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
   systemctl start httpd
   systemctl enable httpd
   ```

---

