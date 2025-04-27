# 📚 Big Data - HDFS Concepts & Components

---

## 📂 About HDFS (Hadoop Distributed File System)

![image](https://github.com/user-attachments/assets/683eca0c-d835-4c13-9e94-c079e59c7ea1)

### 🗣️ Conversation Between Hadoop Client and HDFS:

- **Hadoop Client:**  
  "I have a 200 TB file that I need to store."

- **HDFS:**  
  "Wow! That's **big data**! I'll distribute it across the cluster."

- **Hadoop Client:**  
  "Sounds risky! What happens if a drive fails?"

- **HDFS:**  
  "No worries! I’m **designed for failover** and handle drive failures automatically."

✅ **Key Takeaway:**  
HDFS **splits and distributes** big files across nodes while **keeping replicas** for reliability!

---

## 🗃️ Hadoop vs RDBMS

| Feature | Hadoop | RDBMS |
|:--------|:-------|:------|
| Data Access | Reads entire file sequentially | Uses indexes for fast lookup |
| Data Structure | No structure maintained | Structured with indexes |
| Scaling | Easily scalable with more nodes | Limited by server capacity |
| Performance | Great for big, sequential reads | Great for quick, small queries |
| Failover | In-built replication | Depends on database setup |

---

### 📈 Example Calculation:

- **500 GB** data file read sequentially:
  - **Without Hadoop**:  
    - ~61 minutes (assuming 1,030 Mbps transfer speed).
  - **With Hadoop (example setup)**:
    - 2,000 blocks (each 256 MB)
    - 1.9 seconds to read each block
    - 40-node cluster with 8 disks per node
    - 🔥 Entire 500 GB read in about **14 seconds**!

✅ Use [Data Transfer Calculator](https://www.calctool.org/other/data-transfer) to check time for different file sizes!

---

## 📑 HDFS Characteristics

| Feature | Description |
|:--------|:------------|
| **Hierarchical** | Files organized in parent-child directories |
| **Distributed** | Stored across multiple drives/nodes |
| **Replicated** | Automatic multiple copies of data blocks |
| **Write-once, read-many** | Optimized for one-time writing, multiple-time reading |
| **Sequential Access** | Designed for large, continuous reads/writes |
| **Multiple Readers** | Many clients can read at the same time |
| **Single Writer** | Only one writer allowed at a time for file consistency |
| **Append-only** | Can add data at end; cannot modify existing content |

✅ **Designed for speed, reliability, and huge scale!**

---

## 🧩 HDFS Components: Introduction to NameNode and DataNodes

![image](https://github.com/user-attachments/assets/7a24c394-a44f-4746-b73b-aaf252211a0e)

---

### 🧠 NameNode (Master Node)

- Maintains the **file system metadata**:
  - 📄 File Names
  - 📁 Directory Names
  - 🗂️ File System Hierarchy
  - 🔐 Permissions and Ownerships
  - 🕓 Last Modification Times
  - 🛡️ ACLs (Access Control Lists)
  
✅ **Important:**  
NameNode **does NOT store** the actual data blocks!

---

### 🖥️ DataNode (Worker Node)

- **Stores actual data blocks**.
- Responsible for:
  - Saving file chunks.
  - Replicating chunks across other DataNodes.
  
✅ **Important:**  
DataNodes **only deal with data**, not metadata.

---

# 📋 Quick Flashcards: HDFS Revision 📚

---

### 📌 1. What is HDFS?

➡️ Distributed storage system that stores large data across multiple nodes with automatic replication.

---

### 📌 2. What if a DataNode fails?

➡️ No problem — HDFS has **replication** to recover automatically!

---

### 📌 3. How does Hadoop read large files faster?

➡️ Splits files into **blocks**, distributes across nodes, and reads them in **parallel**.

---

### 📌 4. Who maintains file metadata in HDFS?

➡️ **NameNode** (Master node).

---

### 📌 5. Who stores actual file data blocks?

➡️ **DataNodes** (Worker nodes).

---

### 📌 6. Can multiple clients read from HDFS at the same time?

➡️ **Yes!** HDFS supports multiple readers.

---

### 📌 7. Can multiple clients write to the same file simultaneously?

➡️ **No!** Only **one writer** is allowed at a time.

---

# 🏗️ HDFS Architecture and Writing Process

---

## 🌐 HDFS Architecture Overview

![image](https://github.com/user-attachments/assets/04fc069c-4bd1-431b-be72-b33eedc3a1d2)

### 🖥️ Daemons in HDFS:

- **NameNode** and **DataNodes** run as **Java Virtual Machine (JVM)** processes.

---

### 📂 Primary NameNode (Master)

Manages **Namespace** and **Metadata**:

| Category | Details |
|:---------|:--------|
| **Namespace** | 📂 Directory names, 📄 File names |
| **Metadata** | 🔒 Permissions, 👤 Ownership, 🧩 Block size, ♻️ Replication level, 🕓 Access/modification times, 🧹 User quotas |

✅ **Memory-Based Service**:
- **Journaling**: Safely records changes (like edits) made to the file system.
- **Block Map**: Maps **file names** ➔ **block IDs**.

⏳ **Important:**  
All of this is stored in **memory** (RAM) for super-fast performance!

---

### 🔄 Secondary NameNode (or Standby NameNode)

- Performs **Checkpointing**:
  - Merges disk-based edits + in-memory state.
  - Helps in faster recovery if the Primary NameNode fails.

✅ **Tip:** Secondary NameNode is **NOT** a backup NameNode, but helps in **snapshotting metadata**!

---

### 🏗️ DataNode (Worker)

- **Actually stores** the **data blocks**.
- Handles **block replication** as directed by the NameNode.

---

## 🔄 How HDFS Writes a File (Simple View)

![image](https://github.com/user-attachments/assets/88f8b0d1-25b3-4b14-ae2a-762756a38487)

**Step-by-step:**

1. 📩 **Client** sends file **write request** to the **NameNode**.
2. 📋 **NameNode** responds: tells how to split and where to store blocks.
3. 📦 **Client** breaks file into **blocks** and sends each block to a **DataNode**.
4. 🧬 **DataNode** **replicates** each block to two other DataNodes (as per replication policy).

✅ **Result:**  
File is safely distributed across multiple nodes with backups!

---

## 📝 Detailed View: Writing to HDFS

![image](https://github.com/user-attachments/assets/e72fcbf9-0ee9-45c4-936b-1c582fb8c3d4)

### Detailed Steps:

| Step | Action |
|:-----|:-------|
| 1️⃣ | Client requests to **write** file to HDFS |
| 2️⃣ | NameNode provides a **lease** (temporary lock) for the filename |
| 3️⃣ | Client asks for **block IDs** and **DataNode list** |
| 4️⃣ | NameNode sends **block IDs** + list of target **DataNodes** |
| 5️⃣ | Client writes **data** and **checksums** to the **first DataNode** |
| 6️⃣ & 7️⃣ | **Data pipeline** is created: first DataNode forwards to second, second to third |
| 8️⃣ | Final DataNode verifies **checksums** to ensure data integrity |
| 9️⃣ & 🔟 | **Acknowledgements** travel back through the pipeline |
| 1️⃣1️⃣ | Final ack to **Client** confirming successful write! |

✅ **Quick Tip:**  
If any write fails, retries happen, ensuring data safety.

---

## 🔍 What is a Checksum?

✅ A **checksum** is a small-sized block of data derived from the actual file content.

- Used to **verify** if the data has been **corrupted** during transfer.
- Example:  
  ➔ You calculate checksum of your file  
  ➔ After transfer, recalculate checksum  
  ➔ If both match, data is safe! 🔒

➡️ In HDFS, checksums ensure **block data is correctly written** and **replicated** across nodes.

---

# 🎯 Quick Flashcards for Revision 📚

---

### 📌 1. Where is HDFS metadata stored?

➡️ In **NameNode's memory** (RAM).

---

### 📌 2. What does Secondary NameNode do?

➡️ Creates **checkpoints** (snapshot + merge edits).

---

### 📌 3. What is Journaling?

➡️ Safely **recording changes** made to the HDFS namespace.

---

### 📌 4. What happens if a DataNode fails during write?

➡️ **Replication** ensures there are **backup copies**.

---

### 📌 5. What is a data pipeline in HDFS write?

➡️ Block travels from **first DataNode ➔ second ➔ third**, ensuring replication.

---

## 🛠 Replication and Block Placement in HDFS

![image](https://github.com/user-attachments/assets/58246c0f-3891-46b2-8b2d-f187bc77069a)

### Goals during Block Placement:
- **Minimize Write Cost**
- **Maximize Availability and Read Performance**

**Maximum Availability** means:
- Copies of blocks should be placed on different machines and preferably different racks.

---

## 💻 LABS_HOME Setup (Linux VM)

Commands:
```bash
mkdir /home/talentum/hdp/pigandhive/labs
cp shared/data/stocks.csv /home/talentum/hdp/pigandhive/labs/demos
cd /home/talentum/hdp/pigandhive/labs/demos
head -10 stocks.csv
wc -l stocks.csv
ls -lh stocks.csv
```

---

## 🗂 Path Mapping

| Sr. No. | HDP           | BigData (Host)           | Cloudera (VM)        |
|--------|----------------|--------------------------|----------------------|
| 1      | HDFS - Home     | /user/root                | /user/talentum        |
| 2      | LABS_HOME       | /root/hdp/pigandhive/labs  | ~/hdp/pigandhive/labs |
| 3      | STAGING_AREA    | Host mapped mount point   | Mount point on VM     |

---

## ⚙️ Block Size Experiment

- Trying to store `stocks.csv` (3.5 MB) with custom block size.

Commands:
```bash
# Check if Hadoop is running
jps 

# Start Hadoop if not running
bash Start-Hadoop-Hive.sh

# Set blocksize = 1 MB (1048576 bytes) and put file into HDFS
hdfs dfs -D dfs.blocksize=1048576 -put stocks.csv
```

- Default HDFS block size = **128 MB** if not specified.
- If wrong block size given (e.g., 30 bytes), `put` operation **fails**.

Check result with:
```bash
echo $?
```
- Output `0` → Success
- Output `1` → Failure

---

## 🧩 What Happens Internally?

- File is split into 4 blocks (each ~1MB, last block smaller).
- 3 copies (replicas) needed normally, but only **1 machine** is available → replication factor = 1.

Check file and blocks:
```bash
hdfs fsck /user/talentum/stocks.csv -files -blocks -locations
```
Shows:
- Block IDs
- Replication status
- DataNode location
- File system health

---

## 📂 Deleting and Re-uploading to HDFS

```bash
hdfs dfs -rm stocks.csv
hdfs dfs -put stocks.csv
```
- After re-uploading, the whole file went into **one block** (since default settings used).

---

## 🔗 Connect to Data Blocks

- To inspect a data block manually:
  1. Copy the **block ID**.
  2. Connect to the node (usually through an edge node):
     ```bash
     ssh {ipAddress}
     ssh resourcemanager
     ```
---

**Quick Note**:  
When you uploaded with a 1MB block size → 4 blocks were created.  
When uploaded normally (no custom block size) → only **1 block** created for the 3.5MB file.

---

# 📂 Persisting File System Information on the NameNode

![image](https://github.com/user-attachments/assets/0a2e2c2c-f1b9-4187-b1d4-333a063942ac)

- 🧠 **File system state** is maintained and served from **memory**.
- ⚡ Memory is **fast**, but it’s **volatile** (data is lost if power goes off).
- 💾 To prevent data loss, **file system state is regularly saved (persisted)** to **disk**.

---

# 🚀 The NameNode Startup Process

![image](https://github.com/user-attachments/assets/8829b3f4-f5da-4665-83f3-0de3e93c2660)

1. 📚 NameNode reads two important files: **fsimage_N** and **edits_N**.
2. 🛠️ It **merges** transactions from **edits_N** into **fsimage_N**.
3. 🆕 A new, updated **fsimage_N+1** is created and saved to disk. A **new empty edits_N+1** file is also created.
4. 🚧 During this, **NameNode is in "Safemode"** (🔒 read-only mode).
5. 📝 After safemode, clients (applications) can **create new files** in HDFS.
6. 📄 New transactions (like creating a file) are **logged in edits_N+1**.

---
# 🛠️ Useful Cloudera Commands

We are running this on **Cloudera**.

- To **search for `hdfs-site.xml`** (an important configuration file):

```bash
sudo find / -type f -name hdfs-site.xml
```
- `-type f` → search for files  
- `-name` → specify file name  
- `/` → start search from **root directory**  
- `sudo` → run with **admin/root permissions**

➡️ Once you find the path, **open a new terminal** and **navigate** to it.

In `hdfs-site.xml`, you can find properties like:

```xml
dfs.namenode.name.dir
```

🔵 **Important**:  
There are **separate configuration files** for each Hadoop component:
- **HDFS** → hdfs-site.xml
- **YARN** → yarn-site.xml
- **MapReduce** → mapred-site.xml

👉 These `.xml` config files are **very sensitive** — make sure you edit them carefully!

---

# 🧹 NameNode Safemode Commands

To check or work with NameNode safemode:

```bash
hdfs dfsadmin -help safemode
```

---

# 🧠 NameNode Startup — Detailed View

![image](https://github.com/user-attachments/assets/97bb47e9-e137-4436-b416-a20115b70297)

1. 🚧 NameNode **starts in Safemode** (read-only mode).
2. 🔓 Once the namespace is verified, NameNode **exits Safemode** and enters normal **read-write** mode.

---

# 🛡️ NameNode Checkpoint Operation

![image](https://github.com/user-attachments/assets/8c3625d7-5ac7-429e-9c84-cad0718ca6e2)

✅ **Why checkpoints are important**:
- If edits file grows endlessly, it will slow down startup and use lots of memory.

🔄 **Checkpoint process**:
1. Primary NameNode **creates a new edits file**.
2. Secondary/Standby NameNode **retrieves current edits and fsimage files**.
3. 🔗 It **merges them in memory**.
4. 🖼️ **New fsimage** is created.
5. 📤 New fsimage is **sent back** to the Primary NameNode.
6. 🧹 Primary NameNode saves the **new fsimage** and continues using the **new edits file**.

---
# 📖 Reading Data in HDFS

![image](https://github.com/user-attachments/assets/9adb3612-635c-4e96-b620-a5a9ebf26fcf)

1. 📬 Client **requests a file** from the NameNode.
2. 🧭 NameNode **responds with a sorted list of DataNodes** that have the file’s blocks.
3. 🏃 Client **reads data directly** from the **closest DataNode** (for faster access).
4. 🔍 Client **verifies data** using **block checksums** to ensure data integrity.

---

# 🧱 The DataNode Block Reports

![image](https://github.com/user-attachments/assets/efd13284-aed8-427a-89a0-1766de3bc3c5)

---

# 🔎 DataNode Block Reports — Detailed View

![image](https://github.com/user-attachments/assets/4b8c129e-94bf-441c-82bf-f40b5fbec3b8)

✅ **Block Reports** are how DataNodes tell the NameNode what blocks they have.

**At Startup**:
- After DataNode starts, it sends a **full block report** to NameNode after **3 minutes**.
- Config setting:  
  ```bash
  dfs.blockreport.initialDelay = 120
  ```

**During Operation**:
- DataNodes send **updated block reports** every **6 hours**.
- Config setting:  
  ```bash
  dfs.blockreport.intervalMsec = 21600000
  ```

**Large number of blocks**:
- If too many blocks (>1 million), the report is **split across multiple heartbeats**.
- Config setting:
  ```bash
  dfs.blockreport.split.threshold = 1000000
  ```

---

# ✅ Quick Summary

- NameNode maintains **filesystem metadata** in memory, and persists it periodically.
- **Startup** involves reading fsimage and edits, merging them, and starting in **Safemode**.
- **Checkpointing** is necessary to prevent **edits file** from growing too large.
- **Reading** happens directly from DataNodes after NameNode guidance.
- **DataNode block reports** keep NameNode updated about where blocks are stored.

---

# ❌ DataNode Failure

![image](https://github.com/user-attachments/assets/168f6ba4-eb89-43f7-812f-a63462e17810)

- 🛰️ **NameNode monitors** DataNodes using **heartbeats**.
- 🫀 **Heartbeat Frequency**: Every **3 seconds**.
- ⚙️ Config property:  
  ```bash
  dfs.heartbeat.interval
  ```

---

# 🔎 DataNode Failure — Detailed View

![image](https://github.com/user-attachments/assets/4237b5e2-4a07-48ea-a6eb-de19647ac2a8)

- 🔥 **If heartbeats stop**:
  - 🕒 **After 30 seconds** ➔ DataNode declared **Stale** (used only if needed).
    - Controlled by:
      ```bash
      dfs.namenode.stale.datanode.interval
      ```
  - ⏳ **After 10.5 minutes** ➔ DataNode declared **Dead** (no longer used).
    - Controlled by:
      ```bash
      dfs.namenode.heartbeat.recheck-interval
      ```

- 🧬 When a DataNode **dies**, NameNode **re-replicates the data blocks** to maintain replication factor.

---

# 💿 Failed DataNode Disks

![image](https://github.com/user-attachments/assets/cad580ba-f7d1-4e4c-9d76-dce1d8120b17)

- 💥 A DataNode typically has **multiple disks** to:
  - Boost **I/O performance** 📈
  - Increase **storage space** 🗄️
- ⚠️ More disks ➔ More chances of failure!

- 🛑 By **default**, if even **one disk fails**, the **entire DataNode stops** offering service.

- ⚙️ To allow tolerance for failed disks, use:  
  ```bash
  dfs.datanode.failed.volumes.tolerated
  ```
  - Default: **0** (no tolerance).

---

# 🛠️ HDFS Commands

Basic syntax:  
```bash
hdfs dfs -command [arguments]
```

⚡ Here are some important commands:

| Command | Purpose |
|:---|:---|
| `-cat` | Display file content (uncompressed). |
| `-text` | Display file content (works for compressed files too). |
| `-chgrp`, `-chmod`, `-chown` | Change group/permissions/ownership. |
| `-put`, `-get`, `-copyFromLocal`, `-copyToLocal` | Move files between local filesystem and HDFS. |
| `-ls`, `-ls -R` | List files and directories (R = recursively). |
| `-mv`, `-moveFromLocal`, `-moveToLocal` | Move files. |
| `-stat` | Show file statistics (block size, blocks count, etc.). |

🛟 To see help for any command:  
```bash
hdfs dfs -help
```

---

# ✏️ Examples of HDFS Commands

- 📁 **Create a directory**:
  ```bash
  hdfs dfs -mkdir mydata
  ```

- 📂 **Upload a file** to HDFS:
  ```bash
  hdfs dfs -put numbers.txt mydata/
  ```

- 📃 **List files** inside the directory:
  ```bash
  hdfs dfs -ls mydata
  ```

🧭 Here, `/mydata` is the **relative path to the HOME directory**.

---

# 🔐 HDFS File Permissions

- 🧑‍💻 **Files and directories** have an **Owner** and a **Group**.
- Permission symbols:
  - `r` = read permission
  - `w` = write permission
  - `x` = execute/access permission (needed to access directories)

![image](https://github.com/user-attachments/assets/9df616b6-0920-41d1-9fd7-6beaf8154d03)

---

# 📑 File and Directory Attributes

![image](https://github.com/user-attachments/assets/323ace1c-3c0c-445f-a24c-25403fdf003d)

---

# 🔒 HDFS Permissions (Detailed Table)

| Permission | Directory Action | File Action |
|:---|:---|:---|
| r (read) | View (list) directory contents | View file contents |
| w (write) | Create/delete files or subdirectories | Write or append to files |
| x (execute) | Access a directory (needed for `cd`) | *Ignored* for files in HDFS |

- 👨‍💻 **Most specific user class** permission (Owner > Group > Others) is applied to each user.

![image](https://github.com/user-attachments/assets/7d7f8154-aa29-45fd-9b96-21957565806d)

---

# 🏠 HDFS Home Directories

⬢ Users and applications usually have a **home directory** in HDFS.

- **Purpose**: Control and restrict access to files using **permissions**.
- 📁 Typical Home Directory path:
  ```bash
  /user/username
  ```

![image](https://github.com/user-attachments/assets/41f4c2bc-3b5d-4a12-9a88-952908105245)

---

# ✅ Quick Recap

- **DataNode heartbeats** are vital for their health status.
- **Stale** ➔ after 30s; **Dead** ➔ after 10.5 minutes.
- **Disk failure** can stop a DataNode (unless tolerance is configured).
- **HDFS commands** allow uploading, downloading, permissions handling, etc.
- **Permissions** protect files and directories just like Linux/Unix systems.
- **Home directories** act as a user’s private workspace.

---
