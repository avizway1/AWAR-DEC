### **Important User Management Commands in Linux**

1. **Create a New User**
   - Command:  
     ```bash
     sudo useradd username
     ```
2. **Set a Password for the User**
   - Command:  
     ```bash
     sudo passwd username
     ```
     This sets or updates the password for the user.

3. **Enable Password Authentication**
   - **Step 1:** Edit the SSH configuration file to enable password authentication:  
     ```bash
     sudo vim /etc/ssh/sshd_config
     ```
   - **Step 2:** Locate and update these lines:
     ```plaintext
     PasswordAuthentication yes
     ```
   - **Step 3:** Restart the SSH service to apply changes:
     ```bash
     sudo systemctl restart sshd
     ```

4. **Switch to Another User**
   - Command:  
     ```bash
     su - username
     ```
     This command allows you to log in as another user and access their environment.
To add a user to the `wheel` group, which grants sudo permissions on many Linux distributions, you can use the following command:

```bash
sudo usermod -aG wheel username
```
---

### Verify the User's Group Membership
After adding the user, you can verify their group memberships using:
```bash
groups username
```
---

### **Additional User Management Commands**
- **Delete a User:**  
  ```bash
  sudo userdel username
  ```
  To delete the user along with their home directory:
  ```bash
  sudo userdel -r username
  ```

- **View User Details:**  
  ```bash
  id username
  ```
- **View Currently Logged-in Users:**  
  ```bash
  who
  ```
---

**To log in directly as another user to your EC2 instance without using a keypair, you can set up password-based authentication.
**
---

#### 1. **Switch to the User and Set a Password**
   - Create a new user (if not already created):
     ```bash
     sudo useradd -m username
     ```
   - Set a password for the user:
     ```bash
     sudo passwd username
     ```

#### 2. **Enable Password Authentication for SSH**
   - Edit the SSH configuration file:
     ```bash
     sudo vim /etc/ssh/sshd_config
     ```
   - Look for the following lines and update them:
     ```plaintext
     PasswordAuthentication yes
     ```
   - Save and exit the editor.

#### 3. **Restart the SSH Service**
   - Restart the SSH service to apply changes:
     ```bash
     sudo systemctl restart sshd
     ```
#### 4. **Connect to the EC2 Instance**
   - Use an SSH client to log in with the username and password:
     ```bash
     ssh username@<EC2-Public-IP>
     ```
   - You will be prompted for the password set in Step 1.


---
Permissions in Linux control who can read, write, or execute a file or directory. Here's a breakdown of key concepts and commands:

---

### **File Permissions**
- Permissions are grouped into **User (u)**, **Group (g)**, and **Others (o)**.
- Each group has **read (r)**, **write (w)**, and **execute (x)** permissions.

Example:
```
-rw-r--r--
```
- `-`: Regular file.
- `rw-`: User permissions (read + write).
- `r--`: Group permissions (read only).
- `r--`: Others permissions (read only).

---

### **Permission Representation**
Permissions can be represented in two ways: **Alphabetical** and **Numerical**.

#### **Alphabetical Way**
- `chmod u+rwx filename`: Grants `read`, `write`, and `execute` permissions to the user.
- `chmod g-w filename`: Removes `write` permission from the group.
- `chmod o+x filename`: Adds `execute` permission for others.

#### **Numerical Way**
- Each permission is represented by a number:
  - Read (r) = **4**
  - Write (w) = **2**
  - Execute (x) = **1**
- Add the values for each group:
  - Example: `rwx` = 4 + 2 + 1 = **7**
  - Example: `rw-` = 4 + 2 + 0 = **6**
- Command: 
  - `chmod 755 filename` → User: `rwx`, Group: `r-x`, Others: `r-x`.

---

### **Important Commands**

#### **View Permissions**
```bash
ls -l
```

#### **Modify Permissions**
```bash
chmod 777 filename  # Full permissions for everyone.
chmod 755 filename  # Full permissions for user, read & execute for group and others.
chmod u+x filename  # Add execute for user.
chmod g-w filename  # Remove write for group.
```

#### **Change Ownership**
- Change the owner:
  ```bash
  chown new_user filename
  ```
- Change the group:
  ```bash
  chgrp new_group filename
  ```

---

### **Example Scenarios**

#### **Scenario 1: Full Permissions for Everyone**
```bash
chmod 777 example.txt
```
- User, group, and others can read, write, and execute the file.

#### **Scenario 2: Restrict Permissions**
```bash
chmod 640 example.txt
```
- User: read + write, Group: read, Others: no access.

#### **Scenario 3: Add Execute Permission for User**
```bash
chmod u+x script.sh
```
- Adds execute permission to the user.

#### **Scenario 4: Change Ownership**
```bash
chown alice example.txt
```
- Changes the file owner to `alice`.

--- 
In Linux, file and directory permissions can be managed not just numerically, but also symbolically using the `chmod` command with the following characters:

---

### **Permission Characters**
- **`+`**: **Add** permission.
- **`-`**: **Remove** permission.
- **`=`**: **Set** permission (overwrites existing permissions).

---

### **Examples**

#### **Adding Permissions**
```bash
chmod u+x file.txt  # Add execute permission for the user.
chmod g+r file.txt  # Add read permission for the group.
chmod o+w file.txt  # Add write permission for others.
```

#### **Removing Permissions**
```bash
chmod u-x file.txt  # Remove execute permission for the user.
chmod g-r file.txt  # Remove read permission for the group.
chmod o-w file.txt  # Remove write permission for others.
```

#### **Setting Permissions**
```bash
chmod u=r file.txt  # Set read-only permission for the user.
chmod g=rw file.txt # Set read and write permissions for the group.
chmod o=x file.txt  # Set execute-only permission for others.
```

---

### **Combining Permissions**
You can combine changes for different user groups in a single command:
```bash
chmod u+rwx,g+rx,o-w file.txt
```
- User gets read, write, and execute permissions.
- Group gets read and execute permissions.
- Others lose write permission.

---
