### **What is Linux?**  
Linux is an open-source operating system (OS) based on the Unix architecture. It is widely used for servers, desktops, mobile devices, and embedded systems due to its stability, flexibility, and security. The Linux OS consists of the **Linux kernel** (core system) and various software and tools provided by Linux distributions.  

Linux is a family of open-source, Unix-like operating systems that are built on the Linux kernel. The kernel, initially developed by Linus Torvalds, was first released on September 17, 1991.

---

### **Why Use Linux?**  
1. **Open Source**: Free to use, modify, and distribute.  
2. **Security**: Robust against malware and viruses due to strong permissions and active community updates.  
3. **Stability**: Reliable for servers, databases, and mission-critical tasks.  
4. **Flexibility**: Customizable to fit specific use cases—servers, desktops, IoT, etc.  
5. **Community Support**: Backed by a large community offering solutions and regular updates.  
6. **Cost-Effective**: No licensing fees, reducing overall costs.  
7. **Performance**: Efficient use of resources, making it ideal for both low-end and high-end systems.  
8. **Cross-Platform**: Runs on a wide range of hardware, from embedded devices to supercomputers.  

---

### **What Does Open Source Mean?**  
Open Source refers to software whose source code is freely available for anyone to view, modify, and distribute.  
**Key Characteristics**:  
- **Transparency**: Source code is accessible.  
- **Collaboration**: Encourages contributions from developers worldwide.  
- **Customization**: Freedom to adapt software to individual needs.  
- **Free Distribution**: Redistribution without legal or financial barriers.  
Examples: Linux, Apache, MySQL, Kubernetes.  

---

### **Where to Download the Linux Kernel Source Code?**  
The Linux kernel source code is hosted on the official website and version control platforms.  
1. **Official Website**: [kernel.org](https://www.kernel.org)  
2. **Git Repository**:  
   ```bash
   git clone https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git
   ```
   Developers can download, explore, or contribute to the Linux kernel.  

---

### **Linux Distributions**  
A **Linux Distribution (Distro)** combines the Linux kernel with additional software (desktop environments, package managers, utilities, etc.) to provide a complete OS tailored for different use cases.  

#### **Popular Linux Distributions**  
1. **General Use**:  
   - Ubuntu  
   - Fedora  
   - Linux Mint  
   - Manjaro  

2. **Enterprise Servers**:  
   - Red Hat Enterprise Linux (RHEL)  
   - SUSE Linux Enterprise Server (SLES)  
   - Oracle Linux  

3. **Community Servers**:  
   - CentOS Stream  
   - Rocky Linux  
   - AlmaLinux  

4. **Developers**:  
   - Arch Linux  
   - Debian  

5. **Penetration Testing**:  
   - Kali Linux  
   - Parrot OS  

6. **Lightweight Systems**:  
   - Puppy Linux  
   - Lubuntu  

7. **IoT and Embedded Systems**:  
   - Raspbian (for Raspberry Pi)  
   - Yocto Project  

Each distribution caters to specific needs, making Linux versatile and widely adopted.

---

### **Linux Directory Structure Overview**
The Linux file system is organized hierarchically, with `/` as the root. Each directory has a specific purpose, ensuring clear separation of system, user, and software files. Understanding these directories helps in managing and troubleshooting Linux systems effectively.

---

#### **1. `/` (Root Directory):**  
- **Purpose**: The top-level directory, the parent of all other directories.  
- **Analogy**: Similar to `C:\` in Windows.  
- **Key Note**: Everything in Linux starts from this root directory.

---

#### **2. `/root` (Root User’s Home Directory):**  
- **Purpose**: The home directory for the root user (superuser).  
- **Analogy**: Equivalent to `C:\Users\Administrator` in Windows.  
- **Key Note**: Provides a private workspace for the root user.

---

#### **3. `/home` (Users' Home Directory):**  
- **Purpose**: The home directory for regular (non-root) users.  
- **Analogy**: Equivalent to `C:\Users\<username>` in Windows.  
- **Key Note**: Each user gets a subdirectory within `/home`.

---

#### **4. `/bin` (Binary Executables):**  
- **Purpose**: Contains essential binary files used by all users (e.g., `ls`, `cp`, `mv`).  
- **Key Note**: Commands in `/bin` are available in single-user mode and are critical for system operation.

---

#### **5. `/boot` (Boot Loader Files):**  
- **Purpose**: Contains the Linux kernel, boot configuration, and related files.  
- **Key Note**: Essential for starting the OS (e.g., `vmlinuz`, `grub`).

---

#### **6. `/dev` (Device Files):**  
- **Purpose**: Contains files that represent hardware devices like hard disks (`/dev/sda`) or CD-ROMs (`/dev/cdrom`).  
- **Analogy**: Similar to **Device Manager** in Windows.  
- **Key Note**: Provides an interface to interact with devices.

---

#### **7. `/etc` (Configuration Files):**  
- **Purpose**: Stores system-wide configuration files (e.g., `/etc/passwd`, `/etc/resolv.conf`).  
- **Key Note**: Critical for system settings and service management.

---

#### **8. `/usr` (User Programs):**  
- **Purpose**: Contains user-level programs and libraries (e.g., installed software).  
- **Analogy**: Similar to `C:\Program Files` in Windows.  
- **Key Note**: It includes subdirectories like `/usr/bin`, `/usr/lib`, and `/usr/share`.

---

#### **9. `/sbin` (System Binaries):**  
- **Purpose**: Contains system administration commands (e.g., `ifconfig`, `iptables`).  
- **Key Note**: Only root or superusers can execute commands here.

---

#### **10. `/var` (Variable Files):**  
- **Purpose**: Contains data that changes frequently (e.g., logs, databases).  
- **Examples**:  
  - Log files: `/var/log/messages`  
  - Databases: `/var/lib/mysql`  
- **Key Note**: Used for data that grows dynamically.

---

#### **11. `/mnt` (Mount Points):**  
- **Purpose**: Temporary mount point for file systems.  
- **Key Note**: Empty by default, used for manual mounting.

---

#### **12. `/media` (Removable Media):**  
- **Purpose**: Mount point for removable media (e.g., USB, CDs).  
- **Key Note**: Automatically used by the system for devices like pen drives.

---

#### **13. `/lib` and `/lib64` (Library Files):**  
- **Purpose**: Contains essential shared libraries used by programs.  
- **Analogy**: Similar to `.dll` files in Windows.  
- **Key Note**: Library files have `.so` (Shared Object) extensions.

---

#### **14. `/proc` (Process Information):**  
- **Purpose**: A virtual directory containing runtime system information (e.g., processes, RAM, CPU).  
- **Key Note**: Its contents change dynamically based on system state.

---

#### **15. `/opt` (Optional Software):**  
- **Purpose**: Contains optional third-party software and add-ons.  
- **Key Note**: A separate directory is created for each software package.

---

### **Linux Commands Quick Reference**

---

#### **Environment and User Commands:**
1. **`env`**: Displays all the environment variables for the current user.  
2. **`whoami`**: Shows the current user.  

---

#### **System and Information Commands:**
4. **`uname`**: Prints system information.  
   - **`uname -a`**: Prints all available system information.  
5. **`man <command>`**: Opens the manual for the specified command (e.g., `man uname`).  
6. **`history`**: Displays a list of recently executed commands.

---

#### **File and Directory Commands:**
7. **`pwd`**: Prints the current working directory.  
8. **`ls`**: Lists files and directories in the current location.  
   - **`ls -a`**: Includes hidden files in the listing.  
   - **`ls <path>`**: Lists files and directories in the specified path (e.g., `ls /etc/`).  
9. **`touch <filename>`**: Creates an empty file with the specified name.

---

#### **Directory Navigation Commands:**
10. **`cd`**: Changes the current directory.  
11. **`cd ..`**: Moves up one directory level.  
12. **`cd <path>`**: Changes to the specified path (e.g., `cd /home/user/`).

---

#### **Privilege Escalation:**
13. **`sudo su`**: Switches to the root user (requires the user's password for sudo access).

---

#### **Path and Utility Commands:**
14. **`which <command>`**: Displays the path to the binary of a command (e.g., `which ls` shows `/usr/bin/ls`).

---
### **File and Directory Management in Linux**
---

#### **1. Create Files and Directories**
- **`touch <FILE>`**: Creates an empty file with the specified name.  
  Example:  
  ```bash
  touch myfile.txt
  ```
- **`mkdir <NAME>`**: Creates a new directory with the specified name.  
  Example:  
  ```bash
  mkdir myfolder
  ```

---

#### **2. Copy Files and Directories**
- **Copy File**:  
  ```bash
  cp <FILE> <TARGET>
  ```
  Example:  
  ```bash
  cp myfile.txt /home/user/
  ```

- **Copy Directory (Recursive)**:  
  ```bash
  cp -R <DIR> <TARGET>
  ```
  Example:  
  ```bash
  cp -R myfolder /home/user/
  ```

---

#### **3. Move Files and Directories**
- **Move File**:  
  ```bash
  mv <FILE> <TARGET>
  ```
  Example:  
  ```bash
  mv myfile.txt /home/user/
  ```

- **Move Directory**:  
  ```bash
  mv <DIR> <TARGET>
  ```
  Example:  
  ```bash
  mv myfolder /home/user/
  ```

---

#### **4. Rename Files or Directories**
- **Rename File or Directory**:  
  ```bash
  mv <SOURCE> <NEW_NAME>
  ```
  Example:  
  ```bash
  mv myfile.txt newfile.txt
  mv myfolder newfolder
  ```

---

#### **5. Delete Files and Directories**
- **Delete File**:  
  ```bash
  rm <FILE>
  ```
  Example:  
  ```bash
  rm myfile.txt
  ```

- **Delete Empty Directory**:  
  ```bash
  rmdir <DIR>
  ```
  Example:  
  ```bash
  rmdir myfolder
  ```

- **Delete Non-Empty Directory (Recursive)**:  
  ```bash
  rm -r <DIR>
  ```
  Example:  
  ```bash
  rm -r myfolder
  ```

- **Force Delete (Skip Prompts)**:  
  ```bash
  rm -rf <DIR>
  ```
  Example:  
  ```bash
  rm -rf myfolder
  ```

---

#### **6. Delete All Files in a Directory**
- **Delete Everything Inside a Directory**:  
  ```bash
  rm <DIR>/*
  ```
  Example:  
  ```bash
  rm test/*
  ```

- **Recursive Delete (Including Subdirectories)**:  
  ```bash
  rm -r test
  ```
  Example:  
  ```bash
  rm -r test
  ```

---

### Linux File Viewing and Manipulation Commands:

1. **`cat filename`**  
   - **Purpose**: Displays the entire contents of a file.  
   - **Example**:  
     ```bash
     cat example.txt
     ```

2. **`more filename`**  
   - **Purpose**: Displays file contents page by page, useful for long files.  
   - **Example**:  
     ```bash
     more example.txt
     ```
   - **Navigation**:  
     - Press `Enter` to scroll line by line.  
     - Press `Space` to scroll page by page.

3. **`head /etc/passwd`**  
   - **Purpose**: Displays the first 10 lines of a file by default.  
   - **Example**:  
     ```bash
     head example.txt
     ```

4. **`tail /etc/passwd`**  
   - **Purpose**: Displays the last 10 lines of a file by default.  
   - **Example**:  
     ```bash
     tail example.txt
     ```

5. **`head -n 2 /etc/passwd`**  
   - **Purpose**: Displays the first `n` lines of a file.  
   - **Example**:  
     ```bash
     head -n 5 example.txt  # Displays the top 5 lines
     ```

6. **`tail -n 2 /etc/passwd`**  
   - **Purpose**: Displays the last `n` lines of a file.  
   - **Example**:  
     ```bash
     tail -n 5 example.txt  # Displays the bottom 5 lines
     ```

7. **`pr /etc/passwd`**  
   - **Purpose**: Formats a file for printing.  
   - **Example**:  
     ```bash
     pr example.txt
     ```

8. **`sort /etc/passwd`**  
   - **Purpose**: Sorts file contents in alphabetical order.  
   - **Example**:  
     ```bash
     sort example.txt
     ```
   - **Options**:  
     - `-r`: Reverse order sorting.  
       ```bash
       sort -r example.txt
       ```
---

### Using ZIP Format in Linux

#### Install ZIP and UNZIP tools:
1. **Install `zip`:**  
   ```
   sudo yum install zip -y
   ```
2. **Install `unzip`:**  
   ```
   sudo yum install unzip -y
   ```

#### Zip Commands:

1. **Zip multiple files into an archive:**  
   ```
   zip archive.zip file1.txt file2.txt file3.txt
   ```
   - Creates a `archive.zip` containing `file1.txt`, `file2.txt`, and `file3.txt`.

2. **Zip all files in the current directory:**  
   ```
   zip archive.zip *
   ```
   - Adds all files in the current directory to `archive.zip`.

3. **Zip an entire folder (including its subdirectories):**  
   ```
   zip -r archive.zip mydirectory
   ```
   - Creates a zip file named `archive.zip` containing the folder `mydirectory` and all its contents recursively.

#### Unzip Commands:
1. **Unzip an archive:**  
   ```
   unzip archive.zip
   ```
   - Extracts the contents of `archive.zip` into the current directory.
#### tar.gz Zip Commands:
1. **Create a .tar.gz archive:**  
   ```
   tar -czvf myfile.tar.gz file1 file2 folder1
   ```
  
2. **Unzip a .tzr.gz archive:**  
   ```
   tar -xzvf myfile.tar.gz
   ```
   - Extracts the contents of `myfile.tar.gz` into the current directory.
---

### Understanding `ECHO` command.

1. **Print text to the terminal:**
   ```bash
   echo "Hello, World!"
   ```
   Output:
   ```
   Hello, World!
   ```

2. **Redirect output to a file:**
   ```bash
   echo "This is a test" > file.txt
   ```
   - Writes "This is a test" into `file.txt`.

3. **Append text to a file:**
   ```bash
   echo "Adding another line" >> file.txt
   ```
   - Adds "Adding another line" to `file.txt`.
   
4. **Print a variable value:**
   ```bash
   name="Avinash"
   echo "Hello, $name!"
   ```
   Output:
   ```
   Hello, Avinash!
   ```
---

### **What is `grep` in Linux?**
- `grep` (Global Regular Expression Print) is a powerful command-line tool used for searching text within files.
- It searches files for lines that match a specified pattern and prints them.


### **Examples of `grep`**

1. **Search for a word in a file:**
   ```bash
   grep "word" filename.txt
   ```
   - Searches for "word" in `filename.txt`.

2. **Case-insensitive search:**
   ```bash
   grep -i "word" filename.txt
   ```
   - Matches "word", "Word", or "WORD".

3. **Search for a word in multiple files:**
   ```bash
   grep "word" file1.txt file2.txt
   ```
   - Searches for "word" in both `file1.txt` and `file2.txt`.

4. **Search recursively in directories:**
   ```bash
   grep -r "word" /path/to/directory
   ```
   - Searches for "word" in all files under the specified directory.

5. **Using `grep` with pipes:**
    ```bash
    ps aux | grep "process"
    ```
    - Filters the output of `ps aux` to show lines containing "process".
---
