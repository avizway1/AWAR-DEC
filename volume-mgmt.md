## Volumes Management in AWS

### **What is IOPS?**
**IOPS** stands for **Input/Output Operations Per Second**. It is a performance measurement used to describe the speed at which a storage device can read and write data. This metric is particularly important for applications that rely on high-performance storage, such as databases and high-traffic websites.

### **How IOPS is Calculated**
IOPS is calculated based on the following factors:

1. **Block Size:** 
   - The size of the data blocks being read or written.
   - Common block sizes are 4 KB, 8 KB, or larger.

2. **Latency:**
   - The time taken to process a single I/O request. This includes:
     - **Queue latency:** Time spent waiting in the queue.
     - **Disk latency:** Time taken by the storage media to complete the operation.

3. **Throughput:**
   - The rate at which data is transferred, typically measured in MB/s.

### **IOPS Formula**

**IOPS= Throughput×1024 / BlockSize**

- **Throughput** is in MB/s.
- **Block Size** is in KB.

### **Example**
If a storage device has:
- **Throughput:** 128 MB/s
- **Block Size:** 4 KB

The IOPS can be calculated as:

**IOPS= 128 ×1024 / 4 = 32,768IOPS**

---

### Root Volume
- **Contains OS**: Supported types are `gp2`, `gp3`, `io1`, `io2`, and `magnetic`.


#### Storage Types:
1. **General Purpose SSD (gp2, gp3)**
   - **Suitable for**: Most common workloads.
   - **Key Features**:
     - Low latency.
     - Min: 1 GiB, Max: 16 TiB.
     - Max IOPS: 16,000.
     - gp2: 3 IOPS per GiB with a minimum of 100 IOPS.
     - gp3: Allows specifying required IOPS.

2. **Provisioned IOPS SSD (io1, io2)**
   - **Suitable for**: Workloads requiring specific IOPS or exceeding 16,000 IOPS (e.g., I/O-intensive database workloads).
   - **Key Features**:
     - Min: 4 GiB, Max: 16 TiB.
     - Max IOPS: 64,000 (io1, io2).
     - io2 Block Express: Min: 4 GiB, Max: 64 TiB, Supports up to 256,000 IOPS.

3. **HDD**:
   - **Throughput Optimized HDD (st1)**:
     - Suitable for big data, data warehousing, and log processing.
     - Min: 125 GiB, Max: 16 TiB.
     - Max IOPS: 500, Throughput: 500 MB/s.
   - **Cold HDD (sc1)**:
     - Suitable for less frequently accessed data.
     - Lower cost than st1.
     - Min: 125 GiB, Max: 16 TiB.
     - Max IOPS: 250, Throughput: 250 MB/s.

4. **Magnetic (Standard)**:
   - **Suitable for**: Low-cost storage solutions for less frequently accessed data.
   - Min: 1 GiB, Max: 1 TiB.
---
### **AWS EBS Volume Types and Primary Use Cases**

1. **gp2 (General Purpose SSD):**  
   - **Use Case:** Balanced performance for most workloads.  
   - **Example/Industry:** Small databases, development environments (e.g., retail websites).

2. **gp3 (General Purpose SSD):**  
   - **Use Case:** Cost-effective storage with the ability to provision IOPS and throughput separately.  
   - **Example/Industry:** Application servers, virtual desktops (e.g., SaaS platforms).

3. **io1 (Provisioned IOPS SSD):**  
   - **Use Case:** High-performance storage for critical, latency-sensitive applications.  
   - **Example/Industry:** Large databases (e.g., financial transaction systems).

4. **io2 (Provisioned IOPS SSD):**  
   - **Use Case:** Durable, high-performance storage for mission-critical workloads.  
   - **Example/Industry:** ERP systems, OLTP databases (e.g., healthcare or manufacturing).

5. **st1 (Throughput Optimized HDD):**  
   - **Use Case:** Low-cost, high-throughput storage for large, sequential workloads.  
   - **Example/Industry:** Data warehouses, log processing (e.g., analytics firms).

6. **sc1 (Cold HDD):**  
   - **Use Case:** Lowest-cost storage for infrequently accessed data.  
   - **Example/Industry:** Archiving, backups (e.g., media archives for entertainment).  

---

### File Systems
- **Windows**: FAT, FAT32, NTFS, ReFS.
- **Linux**: ext3, ext4, xfs.

### EBS (Elastic Block Storage)
- Block-based storage designed to run OS and applications.
- **Root Volume**: Supports SSD and magnetic.
- **Additional Volume**: Supports SSD, HDD, and magnetic (st1, sc1).

### Free Tier
- 30 GB of `gp2` or standard storage.
- 20% of volume size or 5 GB, whichever is higher.

---

### Making Additional Volumes Available

#### Windows OS
1. **Disk Management** (`diskmgmt.msc`):
   - Choose volume → Make it online → Initialize disk → Create simple volume → Format with NTFS/FAT.

#### Linux OS
1. **Identify New Volume**:
   - `lsblk`: List block-based devices.
   - `df -Th`: List available volumes.
   - Example: `/dev/xvdf` (new volume).

2. **Prepare Volume**:
   - Check file system: `file -s /dev/xvdf`.
     - Output “data”: No file system.
     - Output ext3/xfs: File system present.
   - Create file system: `mkfs -t xfs /dev/xvdf`.
   - Create mount point: `mkdir newvolume`.
   - Mount volume: `mount /dev/xvdf newvolume/`.

3. **Make Mount Persistent**:
   - Check current mounts: `cat /etc/mtab`.
   - Example Entry:
     ```
     /dev/xvdf /home/ec2-user/newvolume xfs rw,relatime,attr2,inode64,noquota 0 0
     ```
   - Add entry to `/etc/fstab`:
     ```
     /dev/xvdf /home/ec2-user/newvolume xfs rw,relatime,attr2,inode64,noquota 0 0
     ```
   - Apply changes: `mount -a`.

---

### Increasing Volume Size
1. Increase the size in the AWS console.
2. Install `xfsprogs`: `yum install xfsprogs`.
3. Expand volume:
   ```
   xfs_growfs -d /volume-Mountpoint
   xfs_growfs -d /home/ec2-user/newvolume
   ```

**Note**: Decreasing volume size is not supported.

