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
| 1      | HDFS - Home     | /user/talentum                | /user/cloudera        |
| 2      | LABS_HOME       | /talentum/hdp/pigandhive/labs  | ~/hdp/pigandhive/labs |
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

# 📂 HDFS Management Options

There are several ways to manage HDFS (Hadoop Distributed File System):

### 🖥️ Ambari Web UI
- **Type:** Browser-based interface
- **Use:** Manage HDFS configuration and services
- **By:** Hadoop **Administrators** (NOT developers)
- **Extra:** Provides a **graphical dashboard** to manage clusters easily.

---

### 📊 NameNode UI
- **Type:** Browser-based interface
- **Use:** Monitor HDFS status and browse directories
- **Extra:** NameNode is the **master** that manages the filesystem namespace and regulates access to files.

---

### 🗂️ DataNode UI
- **Type:** Browser-based interface
- **Use:** View **block scanner reports**
- **Extra:** Each DataNode stores actual data and periodically reports to the NameNode.

---

### 🖱️ HDFS Command-Line Tools
- **Type:** Command-line based
- **Use:** Interact with files, directories, and HDFS metadata
- **Extra:** 
  - **Most preferred** tool due to **automation capabilities**.  
  - Automation = Time saving ⏳ + Efficiency ✅
  - The future is **automation**.

---

### 📝 Manual Configuration
- **Type:** Direct file editing
- **Use:** Manually edit Hadoop configuration files
- **Warning:** ❗ Not compatible with Ambari. Manual errors can happen easily.

---

> 🔥 **Remember:**  
> - If you are a **Hadoop Administrator** → Set up and manage production clusters.
> - If you are a **Hadoop Developer** → Solve business problems using Big Data.

---

# 🛠️ Command-Line Management

## ⬢ Introduction to Command-Line Tools

| Command        | Purpose                                                              | Who Uses It?            |
|-----------------|-----------------------------------------------------------------------|--------------------------|
| `hdfs dfs`      | Manage files, directories, and metadata                              | Hadoop Developers        |
| `hdfs fsck`     | Check and report file system inconsistencies (**does not repair**)    | Hadoop Administrators    |
| `hdfs dfsadmin` | File system information, statistics, and administration tasks        | Hadoop Administrators    |

> ✅ Mastering these commands = More power & flexibility!

---

# 📦 Determining Storage Space Consumed

Use the `du` (disk usage) command to check **how much space** a file or directory uses.

### ► Key Points:
- **Command:** `hdfs dfs -du [options] [path]`
- **Note:** 
  - It **does not** consider **replication factor**.
  - It shows the **actual file size** on HDFS.

### ► Options:
- `-s`: Show **summary** only (total size)
- `-h`: Show in **human-readable form** (e.g., MB, GB)  
  *(because humans find it difficult to understand raw bytes!)*
- `-l`: **List** the size of each file within a directory

---

### ► Example:
![image](https://github.com/user-attachments/assets/6c8687a3-82f8-460c-abb7-c699ee8c5ac2)

---

# 📈 Monitoring File System Space

Use the `df` (disk free) command to **monitor HDFS capacity and free space**.

### ► Key Points:
- **Command:** `hdfs dfs -df [-h]`
- **Reports:** 
  - Total HDFS capacity
  - Amount of storage **used** 
  - Amount of **free** storage

- `-h`: Shows output in **human-readable** form.

---

### ► Example:
![image](https://github.com/user-attachments/assets/48825ddf-aa9b-4ae3-9f10-40e695153921)

---

# 🎯 Final Tip for Beginners

✅ Start by using **command-line tools** because they give you **better control** and prepare you for **real-world production** scenarios.

✅ **Practice commands** daily — run simple operations like creating directories, copying files, checking space.

✅ **Visualize** what's happening inside HDFS with the help of **UIs** when you are stuck.

---

# 🧠 HDFS Management & Commands – Quick Revision Table

| Topic                       | Key Points                                                                 |
|------------------------------|----------------------------------------------------------------------------|
| **Ambari Web UI**             | Web-based HDFS management (Admin Use)                                      |
| **NameNode UI**              | Monitor NameNode status, browse HDFS directories                           |
| **DataNode UI**              | View block scanner reports of DataNodes                                    |
| **HDFS Command-line Tools**  | File, directory, metadata operations (Automation Focus)                    |
| **Manual Configuration**     | Direct config file editing (⚠️ Not Ambari compatible)                     |
| **Hadoop Administrator**     | Cluster setup, monitoring, fixing                                          |
| **Hadoop Developer**         | Solving business problems with Big Data                                    |

---

# ⚙️ Important HDFS Commands

| Command            | Use Case                                                       | Extra Notes                           |
|--------------------|------------------------------------------------------------------|---------------------------------------|
| `hdfs dfs`          | File/Directory management (copy, move, delete)                  | Developers use it most                |
| `hdfs fsck`         | Check file system health (only reports issues)                  | Admin tool, **no repair**              |
| `hdfs dfsadmin`     | File system info and administration                             | Admin tool                             |

---

# 📏 Space Monitoring Commands

| Command           | Purpose                                | Options                                  |
|-------------------|-----------------------------------------|------------------------------------------|
| `hdfs dfs -du`     | Shows space used by files/directories   | `-s`: summary, `-h`: human readable, `-l`: list contents |
| `hdfs dfs -df`     | Shows total capacity and free space     | `-h`: human readable                     |

---

# 🚀 Pro Tips

- Prefer **automation** over manual work. Learn scripting 📜.
- Use **UIs** (Ambari, NameNode, DataNode) when you need a quick visual check.
- Always remember: **HDFS space reports are without considering replication** unless specified otherwise.
- Practice command-line operations daily to get comfortable! 🎯

---

# 🛠️ Checking File System Consistency

**Goal:** Use the `hdfs fsck` command to verify the health and consistency of the HDFS file system.

---

## ⬢ When Should You Run `fsck`?

- 📛 When concerned about possible **file (data block) corruption**  
- ⚡ After an **HDFS** or **hardware malfunction**  
- 🔄 Before **upgrading** HDFS to a newer version  

---

## ⬢ Key Points About `fsck`
- 🚫 `fsck` **does not repair** corrupt blocks.  
- 📋 It **only reports** issues (unlike Linux `fsck`, which can also repair).
- 📚 `fsck` reads block and metadata information **only from the NameNode**.
- 🖥️ **DataNodes are NOT contacted** during `fsck`.
- 🔑 You must have **access permissions** for the files/directories being checked.
- 👑 **HDFS superuser** has access to everything.

---

## 📜 Command Example:

```bash
hdfs fsck /user/cloudera/soccer_scores.csv -files -blocks -locations
```

- To see available paths:  
```bash
hdfs dfs -ls /
```

---

![image](https://github.com/user-attachments/assets/215dc8ab-9eb1-4bfb-85f9-0e596e7ea907)

---

# 📝 fsck Command Syntax

```bash
hdfs fsck [path] [options] [> output_file]
```

| Option         | Description                                                      | Notes                            |
|----------------|-------------------------------------------------------------------|----------------------------------|
| `-files`       | Lists the files and directories being checked                    | Basic check                      |
| `-blocks`      | Lists **block ID numbers**                                        | Requires `-files -blocks`        |
| `-locations`   | Lists **DataNode locations** of each block                        | Requires `-files -blocks -locations` |
| `-racks`       | Shows **rack name** before each DataNode location                 | Useful if **rack awareness** enabled |
| `-move`        | Moves corrupted files to `/lost+found` directory                  | Recovery action                  |
| `-delete`      | Deletes corrupted files                                           | Destructive action (use carefully!) |
| `-openforwrite`| Lists files **open for writing** (these files are not fully checked) | Open files = still being written |

---

# 🧐 Understanding fsck Output

| Term                    | Meaning                                                                 | Action by NameNode             |
|--------------------------|------------------------------------------------------------------------|---------------------------------|
| ✅ Minimally replicated blocks | At least **one good replica** exists                                  | No immediate action needed      |
| ➕ Over-replicated blocks | More copies than needed (exceeds replication factor)                   | NameNode will **delete extra**  |
| ➖ Under-replicated blocks| Fewer copies than needed (below replication factor)                     | NameNode will **create copies** |
| ♻️ Mis-replicated blocks  | Multiple replicas on the **same DataNode** (bad distribution)           | NameNode will **move blocks**   |
| ❌ Corrupt blocks         | **All replicas** are corrupt (checksum errors)                          | **User must fix manually!** 🚨  |

> ⚡ **Important:**  
> Only corrupt blocks **require user intervention**. HDFS automatically handles under/over/mis-replication.

---

# 📋 Primary Output Example

```bash
hdfs fsck /user/root
```

This provides a **health report** of all files under `/user/root`.

---

![image](https://github.com/user-attachments/assets/dc46cd92-23ca-4978-836d-f645d1499556)

---

# 🧠 Quick Recap

| Action                          | When to Use                                   |
|----------------------------------|-----------------------------------------------|
| `hdfs fsck`                     | Check file system consistency                 |
| `-files -blocks -locations`      | Get detailed block and DataNode info           |
| `-move` / `-delete`              | Handle corrupted files carefully              |
| **Superuser** role               | Needed for full access checking               |

---

✅ **Pro Tip:**  
Always run `fsck` **after any suspected issues** or **before major upgrades** to avoid data loss or cluster instability.

---

# 🔍 Exploring fsck Options in Detail

The `hdfs fsck` command becomes **even more powerful** with specific options.  
Each option adds more information about files, blocks, locations, and racks.

---

# 📄 1. The `–files` Option

👉 **Command:**  
```bash
hdfs fsck /user/root -files
```

- Lists all **files and directories** being checked.
- Shows file names without diving into block or location details.

---

![image](https://github.com/user-attachments/assets/6fa24ff2-d38f-4412-9901-23ad6bcd3d35)

---

# 🧩 2. The `–blocks` Option

👉 **Command:**  
```bash
hdfs fsck /user/root -files -blocks
```

- Lists **Block IDs** for each file.
- Each **block** has a **unique Block ID**.

💡 **Details to Understand:**
- **Block Pool ID** example:  
  ```
  BP-1472918407-172.17.0.2-1431707688874
  ```
  - Same across all DataNodes in a cluster.
- **Data Block ID** example:  
  ```
  blk_1073742266_1442
  ```
  - Each block replica across DataNodes has the **same Block ID**.

---

![image](https://github.com/user-attachments/assets/176b26f7-6475-45f0-aafa-1121e5667492)

---

# 📍 3. The `–locations` Option

👉 **Command:**  
```bash
hdfs fsck /user/root -files -blocks -locations
```

- Adds **DataNode locations** for each block ID.
- You can now see **which DataNode** stores a particular block.

---

![image](https://github.com/user-attachments/assets/14329217-ea8c-4d52-8114-e97d00c1ff95)

---

# 🌐 4. The `–racks` Option

👉 **Command:**  
```bash
hdfs fsck /user/root -files -blocks -locations -racks
```

- Adds **Rack Information** for each DataNode.
- Helps identify **where** (in terms of rack) blocks are stored.

💡 **Important:**  
If **Rack Awareness** is not configured, the default rack shown will be:  
```
/default-rack
```

---

![image](https://github.com/user-attachments/assets/4ee50cb6-7b38-42ac-8ba8-a6747365376f)

---

# 🧠 Quick Summary Table

| Option Used                   | Purpose                                               | Notes                                    |
|---------------------------------|-------------------------------------------------------|------------------------------------------|
| `-files`                       | Lists all checked files/directories                   | Basic listing                           |
| `-blocks`                      | Lists block IDs of files                              | Needs `-files` option too                |
| `-locations`                   | Shows DataNode locations of each block                | Needs `-files -blocks` options           |
| `-racks`                       | Displays rack name with each DataNode location        | Useful if **Rack Awareness** is enabled  |

---

# ✨ Key Takeaways

- Adding options (`-files -blocks -locations -racks`) **gradually increases** the depth of information.
- Even if **rack awareness** is not configured, you can still see **default-rack**.
- Always start with **`-files`**, then expand to **`-blocks`**, **`-locations`**, and **`-racks`** for full insights.

---

✅ **Pro Tip:**  
While debugging file or block issues in Hadoop, **use more detailed fsck commands** to quickly pinpoint where exactly a block resides or where a replication issue is happening.

---

# ⚙️ Distributed File System Administration (dfsadmin)

`dfsadmin` is a **powerful command-line tool** for **HDFS administrators** to manage and maintain HDFS.

---

## 🛠️ Basics of dfsadmin

- **Purpose:** Administration tasks like monitoring, controlling safe mode, checkpointing, etc.
- **Syntax:**  
  ```bash
  hdfs dfsadmin [options]
  ```
- **Getting Help:**  
  ```bash
  hdfs dfsadmin –help
  ```
- **Important:**  
  - You **must be** the **HDFS superuser** to execute most `dfsadmin` commands.
  - In **production**, regular users are **never** granted superuser privileges. (Handled via Ambari or secured admins)

---

# 📚 Common dfsadmin Examples

| Task                              | Command                                       | Purpose                                              |
|-----------------------------------|-----------------------------------------------|------------------------------------------------------|
| Enter Safe Mode                   | `hdfs dfsadmin –safemode enter`               | Pauses all write operations to HDFS (read-only mode) |
| Force a Checkpoint (fsimage save) | `hdfs dfsadmin –saveNamespace`                | Creates a new **fsimage** + **edits** snapshot       |
| Create Only New Edits File        | `hdfs dfsadmin –rollEdits`                    | Rolls the edits log without a full checkpoint        |
| Leave Safe Mode                   | `hdfs dfsadmin –safemode leave`               | Resume normal HDFS operations (write enabled)        |
| Fetch fsimage File (Backup)       | `hdfs dfsadmin –fetchImage`                   | Download latest fsimage for remote backup            |

---

✅ **Checkpointing** and **Safe Mode** control are **critical** during **NameNode HA (High Availability)** setups!

---

![image](https://github.com/user-attachments/assets/b2591161-661c-4c5b-ae33-d46d348af36f)

---

# 📈 Health, Status, and Usage Reports

👉 **Command:**  
```bash
hdfs dfsadmin –report
```

- Shows detailed info like:
  - Total/used/free storage
  - Number of DataNodes live and dead
  - DataNode-specific health
- **Similar** to what you see on the **NameNode UI**!

---

![image](https://github.com/user-attachments/assets/36fa9b72-3a76-48be-ab02-22a22adff6b8)

---

# 📂 Core Hadoop Configuration Files

Ambari installs Hadoop configuration files at:  
```bash
/etc/hadoop/conf
```

These files define the **core behavior** of the Hadoop ecosystem (HDFS, YARN, MapReduce, etc.)

| 📄 File Name        | 📚 File Format            | ⚙️ Purpose                                                                              |
|---------------------|----------------------------|----------------------------------------------------------------------------------------|
| `core-site.xml`      | Hadoop configuration XML   | General Hadoop settings (common to HDFS, YARN, MapReduce)                              |
| `hdfs-site.xml`      | Hadoop configuration XML   | HDFS-specific settings (NameNode, DataNode configuration)                              |
| `yarn-site.xml`      | Hadoop configuration XML   | YARN (ResourceManager & NodeManager) settings                                          |
| `mapred-site.xml`    | Hadoop configuration XML   | MapReduce job configuration settings                                                   |
| `hadoop-env.sh`      | Bash script                 | Sets environment variables like Java path, memory settings                             |
| `log4j.properties`   | Java properties file        | Configures Hadoop system logs for debugging and monitoring                             |

---

✅ **Logs** configured by `log4j.properties` are **critical** for **troubleshooting errors** and **performance tuning**.

---

# 🔍 Finding Important Config Files

**Find `hdfs-default.xml`:**  
```bash
sudo find / -type f -name hdfs-default.xml
```
![image](https://github.com/user-attachments/assets/4e058def-a9da-4267-9d17-cd7cf3654a3d)

---

**Find `core-site.xml`:**  
(No manual search needed if you know default Ambari path: `/etc/hadoop/conf`)

Still, to search manually:
```bash
sudo find / -type f -name core-site.xml
```

![image](https://github.com/user-attachments/assets/6fffa45a-8dcf-4898-a010-f14940728212)

---

# 🎯 Key Takeaways:

- `dfsadmin` = command-line administrator's toolbox 🛠️
- **Safe Mode** = freezes HDFS writes
- **fsimage and edits** are central to **NameNode durability**
- Hadoop config files live in **`/etc/hadoop/conf`** (Ambari-managed)
- Always ensure **superuser access** when doing `dfsadmin` tasks.

---

✅ **Pro Tip:**  
In real production clusters, most `dfsadmin` functionality has a **web UI alternative** via **Apache Ambari** or **Cloudera Manager**, making manual command use less frequent — but it's crucial to **understand the commands** in case UI access is unavailable.

---

# 🛠️ Hadoop Configuration Management

---

## ⚙️ Configuration Precedence

👉 In Hadoop, **configuration settings** are applied **in layers**, following a **precedence order**:

- **Default Configuration** → inherited by  
- **Per-Cluster Configuration** → overridden by  
- **Per-Node Configuration** → overridden by  
- **Per-Job Configuration**

---

✅ **Important Notes:**

- A **running job** uses a **combination** of all these configurations.
- Nodes with **different hardware** may require customized `*-site.xml` files.

---

![image](https://github.com/user-attachments/assets/d52af6a4-aa05-4510-8c09-c3367e174878)

---

## 🛡️ Final Properties

- Some properties are marked as **final** in the XML configuration.
- **Final properties** **cannot be overridden** by:
  - User job configurations
  - Command-line overrides (like `-Dprop=value`)
- They guarantee **system stability** for critical settings.

Example visual:
![image](https://github.com/user-attachments/assets/5c6f647d-5f92-4b67-9f72-a3ffa8423b82)

---

## 📁 Other Framework Configuration Files

Other Hadoop ecosystem components (like Hive, Pig, Zookeeper) **use the same** file structure:

| 📄 File Type         | 🔍 Purpose                                              |
|----------------------|---------------------------------------------------------|
| `*-default.xml`       | Default settings provided by framework developers       |
| `*-site.xml`          | Site-specific configuration overrides                   |
| `*-env.sh`            | Bash environment variable setups                        |
| `*-log4j.properties`  | Logging configuration for troubleshooting and monitoring |

---

➡️ **Example Configuration Directories:**

| 📂 Path                         | 📚 What it Configures             |
|----------------------------------|----------------------------------|
| `/etc/ambari-server/conf`        | Ambari Server                    |
| `/etc/ambari-agent/conf`         | Ambari Agent                     |
| `/etc/hive/conf`                 | Apache Hive                      |
| `/etc/pig/conf`                  | Apache Pig                       |
| `/etc/zookeeper/conf`            | Apache Zookeeper                 |
| ...and more!

---

🔎 **Finding a configuration file (e.g., `hive-site.xml`):**

```bash
sudo find / -type f -name hive-site.xml
```

![image](https://github.com/user-attachments/assets/0140f6f9-3183-4c0e-bf96-0e58cbfbfbee)

---

## 🛠️ Configuration Management Options

| Method                | Description                                        | Benefit                                           |
|------------------------|----------------------------------------------------|---------------------------------------------------|
| Ambari Web UI          | Graphical browser-based management tool            | Very easy to use; no manual editing needed        |
| REST APIs (Ambari, WebHDFS, YARN, etc.) | Use HTTP (GET, POST, PUT, DELETE) to manage clusters | Enables integration and automation via web tools |
| Manual Editing         | Manually edit XML and SH files                     | No dependency on Ambari; useful in minimal setups |
| Command Line Utilities | Per-framework commands (like `hdfs dfsadmin`)      | Great for scripting and automation                |

---

# 📝 Lesson Review Questions

1. **Which component of HDFS maintains the namespace of the distributed filesystem?**  
   ➔ **Answer:** NameNode

2. **What is the default replication factor for files in HDFS?**  
   ➔ **Answer:** 3

3. **True or False:**  
   _The client sends the entire file to the NameNode, and the NameNode then sends data to DataNodes._  
   ➔ **Answer:** **False**  
   _(The client sends block data **directly to DataNodes**, NameNode only manages metadata.)_

4. **Which property is used to specify the block size for a file stored in HDFS?**  
   ➔ **Answer:** `dfs.blocksize`

5. **The NameNode maintains the filesystem namespace using which two sets of files?**  
   ➔ **Answer:**  
   - `fsimage` (snapshot of HDFS metadata)
   - `edits` (log of changes since the last snapshot)

6. **What does this command do?**  
   ```bash
   hdfs dfs -ls -R /user/thomas/
   ```  
   ➔ **Answer:** Recursively lists all files and directories under `/user/thomas/`

7. **What does this command do?**  
   ```bash
   hdfs dfs -ls /user/thomas/
   ```  
   ➔ **Answer:** Lists the files and subdirectories **directly** under `/user/thomas/` (non-recursive)

---

# 🎯 Quick Summary:

- Hadoop config follows **Default → Cluster → Node → Job** precedence.
- **Final properties** cannot be changed by users.
- **Different frameworks** (Hive, Pig, etc.) have similar config structures.
- **Ambari** makes config management easy, but manual and CLI options exist too.

---

# 🚀 Ingesting Data into HDFS

---

## 📚 Topics to be Covered:

- Options for Data Input
- The Hadoop Client
- WebHDFS
- Overview of Sqoop
- Importing Data
- The Sqoop Export Tool
- Exporting to a Table
- Labs: HDFS Importing/Exporting from/to RDBMS using Sqoop
- Lab: Importing Log Data into HDFS using Flume

---

## 🧠 What is Ingestion in Big Data?

**Data Ingestion** means:
- **Connecting** to multiple data sources 📡
- **Extracting** the data 📦
- **Detecting changes** (incremental data)

In short: It's **bringing the data into your Big Data system** (like Hadoop)! 🚚✨

---

## 🔥 Options for Data Input into Hadoop

![image](https://github.com/user-attachments/assets/1906c7cf-9e14-44c1-8b77-c88b49740cc9)

🔵 At the **center**, we have **Hadoop**.

Different options to **ingest data**:
- 🖥️ **Hadoop Client (Edge Node)**  
  ➔ Command: `hdfs dfs -put`
- 🔗 **Connectors to RDBMS** using **Sqoop**  
  ➔ Import relational database data into HDFS.
- 🔥 **Flume**  
  ➔ Capture **streaming data** (e.g., logs) and push it into HDFS.
- ⚡ **Apache Storm**  
  ➔ Real-time **data processing**.
- 🌊 **Apache NiFi** (developed by Hortonworks)  
  ➔ **Dataflow automation** tool (full form: Niagara Files).
- 🌩️ **Spark Streaming**  
  ➔ Handle **real-time data streams**.
- 🛠️ **MapReduce**  
  ➔ Custom-written jobs for batch processing.
- 🌐 **WebHDFS**  
  ➔ Access Hadoop over **HTTP REST API**.

✅ **Important Term:**  
**Edge Node** ➔ A machine where **Hadoop client libraries** are installed but **not a DataNode or NameNode**.

---

## 🖥️ The Hadoop Client — The `put` Command

### 👉 The `put` Command:
- Same as `copyFromLocal`
- **Best used** for uploading files from a **local machine** to **HDFS**.
- Common in **scripts** for **batch uploads**.

### ➡️ Syntax:
```bash
hdfs dfs -put <localsrc> <dst>
```

- `<localsrc>` → Path to your **local file/folder** 📁
- `<dst>` → **Destination directory** in **HDFS** 📂

---

## ⚙️ Java Native API vs. WebHDFS Access

### 🔵 Java Native API (hdfs dfs):
- Needs Hadoop **client installed** ✅
- Uses **RPC** (Remote Procedure Call) for communication 🔗
- Best for:
  - Admins
  - CLI scripts
  - Traditional Java apps

### 🟢 WebHDFS REST API:
- No Hadoop client needed 🚫
- Communicates using **HTTP** 🌍
- Best for:
  - **Web apps**
  - Non-Java applications (like Python, PHP)

---

![image](https://github.com/user-attachments/assets/deba3137-5890-4e58-b7a7-618a1aa13f92)

---

## 🛰️ How Machines Know Where the NameNode is?

When transferring data across machines, we must know:
- **IP addresses**
- **Ports**

👉 But instead of manually providing them, **Hadoop handles this automatically** via **configuration files**!

🔍 To locate important config file:
```bash
sudo find / -type f -name core-site.xml
```
(core-site.xml stores vital information like the NameNode address.)

---

### 📂 Look inside core-site.xml:

```bash
cat /etc/hadoop/conf.pseudo/core-site.xml
```

Sample Outputs:  
![image](https://github.com/user-attachments/assets/da904864-9ae9-4d33-a0f4-bc17bdd63227)  
![image](https://github.com/user-attachments/assets/0bce61b7-d129-47a4-bf85-500d593db9f7)

---

✅ **Important Observations:**
- The **core-site.xml** file is present **inside `/etc`** directory.
- Anything inside `/etc` is **automatically available** in the **Java Classpath**.
- Java applications **read** `core-site.xml` to find **NameNode IP and port**.

---

## 🌐 What is REST API?

🔵 REST (Representational State Transfer) is a **web standard** to communicate between applications using **HTTP**.

🔵 Suppose you write an app using **Python Flask**.  
Since it’s **not Java**, it **can't use Hadoop RPC** directly.

✅ So, we use **WebHDFS REST API** to:
- **Connect** your app with Hadoop
- **Send or retrieve data** over HTTP easily 📡

🧩 Example:  
Python app ➔ WebHDFS API ➔ Hadoop HDFS

---

# 🎯 Summary:

| 🛠️ Topic | 📚 Description |
|:--------|:---------------|
| Data Ingestion | Pulling data into Hadoop from external sources |
| Hadoop Client (`put`) | Uploading local files to HDFS |
| Java Native API | Uses RPC; needs Hadoop installed |
| WebHDFS API | Uses HTTP; good for non-Java apps |
| core-site.xml | Configuration file storing NameNode address |

---

# 📖 Quick Visual Cheatsheet:

- `hdfs dfs -put` ➔ Upload files manually 📂
- **Sqoop** ➔ Import/export structured data 🔗
- **Flume** ➔ Capture live data streams 📈
- **WebHDFS** ➔ Use HTTP to communicate 🌐
- **Edge Node** ➔ Client-only machine 🚀

---

# 🌐 WebHDFS — Accessing HDFS Over the Web

---

## ✨ WebHDFS Features

- 🔵 Supports **all HDFS file administration operations**.
- 🛠️ Enables access to HDFS from **programming languages other than Java**.
  - (**Note:** Java API access still requires Java.)
- 🚀 **Faster access** compared to `hdfs dfs` when the client is **remote**.
- 🖥️ Requires **no additional servers**.
  - WebHDFS is already **built into the NameNode and DataNode**.
- 📶 **Uses the full bandwidth** of the Hadoop cluster:
  - Redirects **read/write operations** to appropriate **DataNodes** directly.
- 🔒 Supports **Kerberos authentication** using SPNEGO (Simple and Protected GSSAPI Negotiation Mechanism).
- 🧩 **Completely open-source** — freely available to everyone!

---

## ⚙️ WebHDFS Enabled by Default

✅ To verify if WebHDFS is enabled:
- Check `hdfs-site.xml` configuration file.
- Or check through **Ambari**.

Example screenshots:  
![image](https://github.com/user-attachments/assets/5cb1a866-7f5e-4e24-b227-dce115c69e5c)  
![image](https://github.com/user-attachments/assets/0f351bb1-6f09-459d-a920-db430b84ba53)

🔵 Look for a property like:
```xml
<property>
  <name>dfs.webhdfs.enabled</name>
  <value>true</value>
</property>
```
If it's set to `true`, **WebHDFS is active**! 🔥

---

## 🧩 WebHDFS Operations — HTTP Methods

In WebHDFS, we use **standard HTTP methods** to perform operations:

| 🌍 HTTP GET         | 📤 HTTP PUT         | 📨 HTTP POST         | 🗑️ HTTP DELETE      |
|---------------------|---------------------|----------------------|---------------------|
| OPEN                | CREATE              | APPEND               | DELETE              |
| GETFILESTATUS       | MKDIRS               |                      |                     |
| LISTSTATUS          | RENAME               |                      |                     |
| GETCONTENTSUMMARY   | SETREPLICATION       |                      |                     |
| GETFILECHECKSUM     | SETOWNER             |                      |                     |
| GETHOMEDIRECTORY    | SETPERMISSION        |                      |                     |
| GETDELEGATIONTOKEN  | SETTIMES             |                      |                     |
|                     | RENEWDELEGATIONTOKEN |                      |                     |
|                     | CANCELDELEGATIONTOKEN|                      |                     |

✅ **Note:**  
- If no HTTP method is specified, **GET** is the default method!

---

## 🛜 WebHDFS Examples (1) — Basic Operations

We interact with WebHDFS using **URLs** and **curl** command.

🔵 **WebHDFS API Prefix:**
```plaintext
http://<NameNode>:50070/webhdfs/v1/<path>?op=<operation>&user.name=<username>
```

| 🛠️ Task              | 📚 Example |
|-----------------------|------------|
| Create Directory      | `curl -i -X PUT "http://<NameNode>:50070/webhdfs/v1/web/mydata?op=MKDIRS&user.name=jason"` |
| List Directory        | `curl -i "http://<NameNode>:50070/webhdfs/v1/web/mydata?op=LISTSTATUS&user.name=jason"` |
| Read File             | `curl -i -L "http://<NameNode>:50070/webhdfs/v1/web/mydata/webdata?op=OPEN&user.name=jason"` |

📌 **curl** stands for **Client URL** — it helps interact with web services directly from the command line.

---

## 🛜 WebHDFS Examples (2) — Writing Data (Advanced)

✍️ **Writing a file** is a **two-step process** in WebHDFS:

### Step 1: Create a file **name** on the NameNode
```bash
curl -i -X PUT "http://<NameNode>:50070/webhdfs/v1/web/mydata/largefile.json?op=CREATE"
```
- This only creates an **empty file entry** in HDFS.

---

### Step 2: Upload the **file contents** to the DataNode
```bash
curl -i -X PUT -T largefile.json "http://<DataNode>:50075/webhdfs/v1/web/mydata/largefile.json?op=CREATE&user.name=root&namenoderpcaddress=node1:8020&overwrite=false"
```
- `-T largefile.json` → tells `curl` to **send the file contents**.

---

✅ **Shortcut:** You can **combine both steps** into one command:
```bash
curl -i -X PUT -L -T largefile.json "http://<NameNode>:50070/webhdfs/v1/web/mydata/largefile.json?op=CREATE&user.name=root"
```
- `-L` → Automatically follows HTTP redirects between NameNode and DataNode.
- Quicker for scripts and applications!

---

# 🎯 Quick Summary Table

| 🛠️ Feature           | 📚 Description |
|----------------------|----------------|
| WebHDFS Access       | Uses HTTP (REST API) to talk to HDFS |
| Faster Access        | Directs read/write to DataNodes |
| Authentication       | Supports Kerberos with SPNEGO |
| Two-Step Write       | Create filename first, upload file second |
| curl Command         | Tool to send HTTP requests easily |

---

# 🔥 Cheat Sheet — Important WebHDFS URL Parts

| URL Part | Meaning |
|----------|---------|
| `http://<NameNode>:50070/webhdfs/v1/` | Base API endpoint |
| `<path>` | HDFS path you are operating on |
| `op=`    | The operation you want (CREATE, OPEN, LISTSTATUS etc.) |
| `user.name=` | User name who is performing the action |

---

# 🌐 WebHDFS — Practical Usage and Examples

---

## 📖 WebHDFS: Basic REST API Operations

WebHDFS uses **REST API** to access the full HDFS filesystem!  
Here are some examples:

| 🌍 URL Example | 🔥 What it does |
|----------------|----------------|
| `http://host:port/webhdfs/v1/test/mydata.txt?op=OPEN` | Open and read `mydata.txt` |
| `http://host:port/webhdfs/v1/user/root/data?op=MKDIRS` | Create a directory `data` |
| `http://host:port/webhdfs/v1/test/mydata.txt?op=APPEND` | Append data to `mydata.txt` |

✅ **Key format:**  
```plaintext
http://<host>:<port>/webhdfs/v1/<path>?op=<operation>
```

---

# 🧪 LAB: Using WebHDFS Commands

---

## 🛠️ 1. Listing a Directory `/user/cloudera`

Command:
```bash
curl -i "http://quickstart.cloudera:50070/webhdfs/v1/user/cloudera?op=LISTSTATUS"
```

Result snapshot:  
![image](https://github.com/user-attachments/assets/88f64846-8317-4a2a-9736-34bc18c201cf)

📚 **Important concepts:**
- **Header** — from start till `Transfer-Encoding`
- **Payload** — from `FileStatuses` onwards (actual file data)
- **Important Header Field:**  
  ```plaintext
  Content-Type: application/json
  ```
  This tells us that **payload is JSON format**.

---

## 📄 2. Opening and Reading a File `/user/cloudera/stocks.csv`

Command:
```bash
curl -i -L "http://quickstart.cloudera:50070/webhdfs/v1/user/cloudera/stocks.csv?op=OPEN"
```

Result snapshots:  
![image](https://github.com/user-attachments/assets/cd898be0-ddef-4ee7-aa62-e886203b9576)  
![image](https://github.com/user-attachments/assets/dcf02792-080e-4999-b8d4-0da2d8730d33)  
![image](https://github.com/user-attachments/assets/c3dd595b-a7d6-4b54-91b3-b0fe59288bb3)

✅ **Notes:**
- `-L` flag tells `curl` to **follow redirects** automatically (because `OPEN` operation redirects to DataNode).
- Output will be the **content of stocks.csv** file.

---

## 🗂️ 3. Creating a New Directory `/user/cloudera/data`

Command:
```bash
curl -i -X PUT "http://quickstart.cloudera:50070/webhdfs/v1/user/cloudera/data?user.name=cloudera&op=MKDIRS"
```

Result snapshot:  
![image](https://github.com/user-attachments/assets/f419691d-7ba5-45f8-ac8e-7fe48d66a829)

🔍 **Verification using Hadoop command:**
```bash
hdfs dfs -ls
```

Result snapshot:  
![image](https://github.com/user-attachments/assets/f0f1c3af-3685-4d3c-818d-077ff7fc64d8)

✅ If the new directory `/user/cloudera/data` shows up, the command worked!

---

## 📝 4. Writing a File to HDFS in **Single Curl Command**

Suppose you have a file `small_blocks.txt` in `/home/cloudera/labs/demos/`.

Command:
```bash
cd /home/cloudera/labs/demos

curl -i -X PUT -T small_blocks.txt \
"http://quickstart.cloudera:50075/webhdfs/v1/user/cloudera/small_blocks.txt?op=CREATE&user.name=cloudera&namenoderpcaddress=quickstart.cloudera:8020&overwrite=false"
```

Result snapshot:  
![image](https://github.com/user-attachments/assets/0b7f0a28-ef31-46c7-95fd-bf1b2306a453)

✅ **Explanation:**
- `-T small_blocks.txt` → sends the file contents.
- `op=CREATE` → creates the new file.
- `namenoderpcaddress` helps locate correct cluster settings.

---

## 🗑️ Deleting a Specific File

Result snapshots:  
![image](https://github.com/user-attachments/assets/3614dd54-c493-459d-bad8-dbe293fcb1c4)  
![image](https://github.com/user-attachments/assets/f6c8a584-9dc5-4e33-b0cc-790da6b11eb7)

✅ You can use **HTTP DELETE method** with curl to delete files via WebHDFS.

**Example:**
```bash
curl -i -X DELETE "http://<host>:50070/webhdfs/v1/<path>?op=DELETE&user.name=<username>"
```

🔵 If successful, the file will be **permanently deleted** from HDFS!

---

# 📋 Quick Recap Table

| 🌍 Task | 🛠️ Command |
|--------|------------|
| List Directory | curl -i "…?op=LISTSTATUS" |
| Open File | curl -i -L "…?op=OPEN" |
| Create Directory | curl -i -X PUT "…?op=MKDIRS" |
| Upload File | curl -i -X PUT -T <file> "…?op=CREATE" |
| Delete File | curl -i -X DELETE "…?op=DELETE" |

---

# 🧠 Key Points to Remember

- `-i` → Include header in output
- `-X` → Specify HTTP method (PUT, DELETE)
- `-T` → Upload file contents
- `-L` → Follow redirects automatically
- Always check **Content-Type** in header to know payload format!

---

# 🖥️ Working with BigDataVM, Hadoop, and WebHDFS

---

## 🔥 Starting Hadoop on BigDataVM

First, start the Hadoop services:
```bash
bash Start-Hadoop-Hive.sh
```
✅ This starts Hadoop and Hive services needed for HDFS access.

Snapshot:  
![image](https://github.com/user-attachments/assets/5b1c881f-f074-497e-a69c-6083c4e6f341)

---

## 🌐 1. List Directory `/user/talentum`

Command:
```bash
curl -i "http://talentum-virtual-machine:50070/webhdfs/v1/user/talentum?op=LISTSTATUS"
```

Result:  
![image](https://github.com/user-attachments/assets/b63375a2-d71a-4358-a770-4b19ccf34118)

✅ This lists all files and folders under `/user/talentum`.

---

## 📄 2. Open a File `/user/talentum/shared/stocks.csv`

Attempted command:
```bash
curl -i -L "http://talentum-virtual-machine:50070/webhdfs/v1/user/talentum/shared/stocks.csv?op=OPEN"
```
⚠️ Error: **File not found!**

### ➡️ **Solution:**
Upload `stocks.csv` manually into HDFS:
```bash
hdfs dfs -put /home/talentum/stocks.csv /user/talentum
```
- Had issues because of **DataNode failure**.
- Fixed by **restarting Hadoop services**, then retried the `hdfs dfs -put` command.

✅ After success, re-running `curl -i -L ...` opened the file correctly!

Snapshot:  
![image](https://github.com/user-attachments/assets/2afdd416-0828-4063-aed7-d547205abd8b)

---

## 📂 3. Adding `small_blocks.txt` to HDFS via WebHDFS

First, verify the file's presence:
```bash
cp /home/talentum/small_blocks.txt /home/talentum
```
(to make sure it’s at the right location)

Upload command:
```bash
curl -i -X PUT -T small_blocks.txt \
"http://talentum-virtual-machine:50075/webhdfs/v1/user/talentum/small_blocks.txt?op=CREATE&user.name=talentum&namenoderpcaddress=localhost:9000&overwrite=false"
```

Snapshot:  
![image](https://github.com/user-attachments/assets/630fc08d-1ca5-4b8a-b138-279b096203ec)

✅ `small_blocks.txt` successfully uploaded to HDFS!

Final Output:  
![image](https://github.com/user-attachments/assets/bdc69c46-eeca-4806-a823-39c2782f5a91)

---

# ⚙️ Automating with Shell Script

---

### 📁 Project Requirement:
- First team generates data.
- Output file is given to second team (which may use any programming language).
- **Shell script** collects data automatically.

---

### 📜 Creating the automation script

Command to create a new file:
```bash
vim automatelist.sh
```

Content inside `automatelist.sh`:
```bash
#!/bin/bash

curl -i "http://talentum-virtual-machine:50070/webhdfs/v1/user/talentum?op=LISTSTATUS" > automateoutput.txt
```

Snapshot:  
![image](https://github.com/user-attachments/assets/c25c72f8-18d9-4e69-889d-4983c8a6330d)

✅ This script fetches directory listing and saves it into `automateoutput.txt`.

---

### 🖥️ Running the script

Command:
```bash
bash automatelist.sh
```
Snapshot:  
![image](https://github.com/user-attachments/assets/5ba09b76-f794-4158-85df-199cb926bb29)

Check output:
```bash
cat automateoutput.txt
```
Snapshot:  
![image](https://github.com/user-attachments/assets/26eb2b2d-0212-4bfc-97d0-159d41d8d135)

✅ Now, `automateoutput.txt` can be shared with the next team for further processing!

---

# 💤 Suspended Mode (HIBERNATION)

- You can **suspend** the Virtual Machine instead of shutting down.
- It saves the machine's **state** so that you can **resume instantly** later.

---

# 🛠️ Dynamic Script for Different Machines

Modified Shell Script:
```bash
#!/bin/bash

curl -i "http://$1:50070/webhdfs/v1/user/cloudera?op=LISTSTATUS" > automateoutput.txt
```

- `$1` → first command-line argument (hostname/IP)
- Makes the script **flexible** for different VMs!

Running it:
```bash
./automatelist.sh quickstart.cloudera
```

Snapshot:  
![image](https://github.com/user-attachments/assets/6066b605-08ee-449c-a0e8-f8ddd290441e)

✅ It works dynamically based on input hostname!

---

# ✨ Quick Summary Table

| 📌 Task | 🛠️ Command |
|--------|-----------|
| Start Hadoop | bash Start-Hadoop-Hive.sh |
| List Directory | curl -i "…?op=LISTSTATUS" |
| Open File | curl -i -L "…?op=OPEN" |
| Upload File | hdfs dfs -put /path/file /hdfs/path |
| Upload via WebHDFS | curl -i -X PUT -T file "…?op=CREATE" |
| Automation Script | vim automatelist.sh |
| Dynamic VM Access | ./automatelist.sh <hostname> |

---

# 📂 Demo: Putting Files in HDFS with Java

Let's learn how to build a Java application to send (ingest) files into Hadoop HDFS!

---

## 🔨 What Does "Build a Java Application" Mean?

It means **three simple steps**:
- **Write** the source file (`.java`)
- **Compile** the source file into a class file (`.class`)
- **Package** the class files into a **library** (`.jar`)

This `.jar` file can then run on **Hadoop Cluster**.

---

## 🛠 Steps to Build Java MR (MapReduce) Application Using Eclipse IDE

### 1️⃣ Create an Eclipse Java Project

👉 In Eclipse:
- File ➡️ New ➡️ Project ➡️ Java Project
- Name it: **HDFS_API**

![Create Project](https://github.com/user-attachments/assets/af78585f-412a-4ec3-b1bd-e89c6beec0b5)

👉 If a `.rar` file (compressed project) is provided, **extract** it first.

---
### 2️⃣ Set JDK Properly (⚙️ JRE vs JDK)

- Use **default JRE** (Example: `jdk1.7.0_67-cloudera`)
- Eclipse doesn't have its own JDK, it uses the one installed on your machine.

![JRE vs JDK](https://github.com/user-attachments/assets/4faa3eeb-eb26-4bfd-ae16-a2fc11c5a92b)

✔️ Click **Next** and **Finish**.

---

### 3️⃣ Understand the Project Structure

- **src/** ➡️ contains your `.java` files (the source code)

![src folder](https://github.com/user-attachments/assets/3f80c255-a11e-4533-a83b-20c42105fcf5)

---

### 4️⃣ Create a Package (📦)

👉 Right-click on Project ➡️ New ➡️ Package  
Name it **hdfs**.

- A package groups related Java classes.

![create package](https://github.com/user-attachments/assets/4f88660b-332b-4a33-8f34-3ad042994a3b)

- Our work with HDFS will go into this package.

![package hdfs](https://github.com/user-attachments/assets/c621691e-ccb7-4b17-9235-3ef191076e4e)

- Final package view:

![package created](https://github.com/user-attachments/assets/6f2f6941-f702-4f4a-a256-13124064168c)

---

### 5️⃣ Import Source Files

- Copy the `.java` file (code) inside the **hdfs** package.

---

### 6️⃣ Solve Compilation Errors (🛠️ Add Hadoop Libraries)

Problem: You'll get errors because Eclipse cannot find Hadoop classes.

Solution:
- Right-click Project ➡️ Build Path ➡️ Configure Build Path ➡️ Libraries ➡️ **Add External JARs**
- Navigate to `/usr/lib/hadoop/client`
- **Select all JAR files** and click OK twice.

![add external jars](https://github.com/user-attachments/assets/d898291e-4acf-4f92-a983-4c358a7a5316)

👉 **Tip:** Turn on **Autosave** in Eclipse to compile automatically whenever you save the code!

---

### 7️⃣ Successful Compilation ✅

- If no red marks (errors) ➡️ Your Java code is successfully compiled.

---

## 📦 Step 8: Create a JAR File

How to create `.jar` (Java library file):

1. Right-click Project ➡️ Export ➡️ Java ➡️ JAR File ➡️ **Next**
2. Choose the location: `/home/cloudera/shared/data/HDFS_API`
3. Rename your jar: **inputcounties.jar**
4. Click OK ➡️ Next ➡️ Next ➡️ Finish!

---

## 🧪 Step 9: Verify the JAR File

Check that your `.jar` file is created.

![verify jar](https://github.com/user-attachments/assets/2fb0acbc-6008-4ec9-aa3b-4a0e7caff367)

---

## 🚀 Step 10: Run the JAR on Hadoop Cluster

1. Open Terminal.
2. Go to the folder where your jar file is located.
3. Run:

```bash
yarn jar inputcounties.jar
```
But if it gives an error, you need to also **mention the class name** inside the jar:

```bash
yarn jar inputcounties.jar hdfs.InputCounties
```
- Here `inputcounties.jar` = your jar file
- `hdfs.InputCounties` = your **package name** + **main class name**

4. Check success/failure by typing:

```bash
echo $?
```
- `0` = Success
- Non-zero = Error

---
### Important Visuals:

- Running JAR Example:

![run yarn jar](https://github.com/user-attachments/assets/cc65a643-3c26-444b-8d27-0814a04217db)

- Successful Execution:

![execution output](https://github.com/user-attachments/assets/be98ebd5-626e-42e7-ae8e-1d9051a6d425)

- Another Output Example:

![hadoop output](https://github.com/user-attachments/assets/dedb7b56-3f0a-48ac-beeb-db28b24d74de)

---

# 🧠 Final Quick Summary

| Step | Action |
|:----:|:------|
| 1 | Create Java project |
| 2 | Create package inside project |
| 3 | Import Java code |
| 4 | Fix errors by adding Hadoop JARs |
| 5 | Compile successfully |
| 6 | Create `.jar` file |
| 7 | Verify the `.jar` |
| 8 | Run using `yarn jar` command |
| 9 | Debug if necessary (`echo $?`) |

---

# 🌟 And that's it!

**You have now learned how to build a Java MapReduce application and run it on a Hadoop cluster!** 🚀  

---

Different types of client applications:

Web Client: This is a client application that runs in a web browser. It does not require installation on the user's device, as it relies on web technologies like HTML, CSS, and JavaScript. Examples include Gmail, Google Docs, and Microsoft Outlook Web App.

Thick Client (or Fat Client): This type of client application is installed directly on the user's device and often performs substantial processing locally. It typically interacts with a server but does not rely entirely on the server for functionality. Examples include Microsoft Word, Adobe Photoshop, and desktop email clients like Outlook.

---

Download ideaintellj
and put it into home of big data

There is no eclipse in this environment
WE are going to install intellij
Open in Libra office

sudo snap remove intellij-idea-community
Delete if already present

Now install
Installation is in tar format
now we are compressing it
gunzip is used to do it. In short it is known as gzip
We are extracting now.

Manual for tar: man tar

![image](https://github.com/user-attachments/assets/16dc1973-6efd-46ea-a1f3-5a66afafc183)

To extract gz, use z
What is verbose?
What is zxvf in linux

We are extracting now
sudo tar -zxvf 'Copy of ideaIC-2018.2.8.tar.gz' -C /opt/
![image](https://github.com/user-attachments/assets/b35cf63a-fb3c-4cc5-aa89-f50707b7237d)
![image](https://github.com/user-attachments/assets/e03de164-db22-427e-80f4-4a927a2ca389)

ls -lh /opt/
![image](https://github.com/user-attachments/assets/7ae6434e-36ef-495a-a880-ebb8c5ca4c69)

Here, opt is created in /

![image](https://github.com/user-attachments/assets/6c4b149d-1212-4a9e-8a9a-1fb1c0779444)

cd /opt
ls
ls -lh
![image](https://github.com/user-attachments/assets/14753432-b8fc-4719-9ba2-2cb1b0101ec2)

ls -lh idea-IC-182.5262.2/
![image](https://github.com/user-attachments/assets/308ea8f5-3193-485e-9e4c-5b35e35f8316)

Now we have copied the folder HDFS_API present in our STAGING AREA TO LABS_HOME:

![image](https://github.com/user-attachments/assets/d5defc89-dfd7-470d-a48f-23c57bbe9b6c)

C![image](https://github.com/user-attachments/assets/20cd258d-da2a-4019-9ded-751c119c1bea)

![image](https://github.com/user-attachments/assets/e2993d72-15c0-4846-8741-e64a3fc6f875)

tHERE ARE MANY SHELL SCRIPTS
![image](https://github.com/user-attachments/assets/febe7a3e-6b6f-4c6e-be28-a5980ea81123)

./idea.sh

A screen will pop up

![image](https://github.com/user-attachments/assets/ec22c7df-23f7-4138-ad44-7edb6433f606)
Click on OK.

A screen will appear here:

![image](https://github.com/user-attachments/assets/feedff35-a79a-4022-af5f-66c93c65dafd)

Select the Darcula
Click on Next desktop entry 
![image](https://github.com/user-attachments/assets/7721b60d-2f64-4a2b-82b9-3dfe6dad6c2b)
next launcher script



![image](https://github.com/user-attachments/assets/a8d7b788-00c0-4a45-b595-0b468a4002b1)

![image](https://github.com/user-attachments/assets/6006b891-82ed-4540-be33-93df37fa9a87)

Next default plugins
![image](https://github.com/user-attachments/assets/6e416d83-ed66-4499-89d3-a4c73264ead3)
Options shown on this screen:
Build tools: We can integrate build tools.
Version Control: Git is a version Control.
Test Tools
Swing: java has swing, python has tkinter
Android
Other Tools
Plugin Development

Click on Next: Featured Plugins
![image](https://github.com/user-attachments/assets/41049e86-2531-4e39-b6b2-6ff20f9ca163)

Tools:
Scala
IdeaVim

Now click on Start uisng InteliJ IDEA, it will start
![image](https://github.com/user-attachments/assets/92221197-2f7d-4a93-b36d-57f9eddbf20f)

Create new project
![image](https://github.com/user-attachments/assets/3ff04d4a-2be7-4b7d-92a0-d66160f8d180)

---

We were having a machine with eclipse and created a project and the libraries required for project were there in the ide itself.
Then we added jars there.
We did this yesterday in Eclipse.

But, our machine today, we don't have libraries here in the intellij.
We will be using Code Repository: Maven Repo
This has all the dependencies for all the projects.
For example, hadoop requires Hadoop client side libraries.
We need to connect our project to maven repo.
We can't only create java project in intellij.
Additional task is to pull the libraries also.
We will need to create Maven Java Project. 

---

We can create Java Project, Android, Intellij platform plugin, kotlin, projects here in intellij IDEA.
But we are interested in Maven here.
By default Project SDK is 1.8 here because it is showing java project.
select maven project
![image](https://github.com/user-attachments/assets/f82efa36-dc9a-450a-8524-4806ba252156)

Click NExt
![image](https://github.com/user-attachments/assets/416fe088-1ed1-4ed4-95da-386a4ec6eb17)

We need to give the address of dependencies here
That address will be combinateion of groupid and artifactid
Every project will have a unique id and is shown by groupid and artifact id
group id: org.example

![image](https://github.com/user-attachments/assets/8033d701-0859-4f92-9d8a-f0a0be404983)

artifact id: HDFS_API
![image](https://github.com/user-attachments/assets/295115a5-c34e-4e80-90a2-df3903c419e9)

Click on Next
artifact id has been taken as project name: ~/IdeaProjects/HDFS_API
![image](https://github.com/user-attachments/assets/daf42a48-03c0-4dad-a228-37bf8a94ffe2)

Click on Finish

![image](https://github.com/user-attachments/assets/2e4fb860-9b71-4826-9549-2d78b529c4fb)
Click on Enable Autoimport when the dialog box pops up which asks maven projects need to be imported
IT will start downloading the dependencies then

---

Every maven file is uniquely identified by a file called as pom (Project object model)
The file which we are seeing on the screen is pom file.
It contains groupid and artifact id which we specified.

Go to terminal linux:
go inside ideaprojects folder
![image](https://github.com/user-attachments/assets/79b57e7c-4707-481c-96c6-18cd50c23d61)

It should contain HDFS_API folder and inside it a pom.xml file and src folder
![image](https://github.com/user-attachments/assets/9dc5e940-999b-4f9a-844a-58d1fa9f101e)

By the way, why are we using different environments to do the same task. We are using cloudera and BigDataVM.
The answer is to get new learning. We get to know what automation is. Production environment is completely server based, ui based. Not to go in comfort zone. 
We can also use Eclipse on BigDataVM. 

---

Every maven file is identified by three points:
groupid, artifactid and version

![image](https://github.com/user-attachments/assets/9f7049af-054f-47e9-ac16-b6b4a8d277ac)

Files in our project:
![image](https://github.com/user-attachments/assets/e113018e-9876-488b-b53d-2baa9269b726)


in Eclipse
src contains all the code files
in Intellij
src > main > java > code files will be stored here

Yesterday, the package name was hdfs

now, select java right click new package
package anme is hdfs

![image](https://github.com/user-attachments/assets/6076f390-dde1-4fd1-b154-4902a2532ee1)

Moving the InputCounties.java file from HDFS folder of staging area into src/main/java folder:

![image](https://github.com/user-attachments/assets/cedfaa2c-1aed-44bd-b5b1-9d387adb3ee3)
![image](https://github.com/user-attachments/assets/62bb386a-d56c-40b6-bf63-706d973f7cee)

the java file is showing error because of the client side libraries because it is not being present.
They have to be added in the class path.
maven project needs the client side libraries.
pom.xml represents the project in maven.
We must tell pom.xml what are our requirements.

Checking hadoop version in terminal

![image](https://github.com/user-attachments/assets/159241d4-f4f1-4bf9-bae2-e13bb986ba49)

We require hadoop client side library for version 2.7.3

We need to google: maven repository hadoop client 2.7.3

This is the dependency:
![image](https://github.com/user-attachments/assets/5c639aaf-8e75-4891-8732-2d9c6f88a6e1)

Our project too has groupId, artifactId, version
We need to put this dependencies in our project

Now, how to put that dependency

Return to HDFS_API in Intellij:
![image](https://github.com/user-attachments/assets/68016171-d608-4114-b383-fa10c7592bb0)

We have put dependencies related to hadoop client
![image](https://github.com/user-attachments/assets/4ac8bd3e-a1e8-4c60-8708-ef7f45e6bd76)

Errors of InputCounties.java has been resolved.

External Libraries:
![image](https://github.com/user-attachments/assets/e14b2895-9758-4e7d-adfd-b0b8cc557a0f)


The hadoop library version needs to be same when working in projects with different teams. Different version system will result in errors.

The responsibility of creating jar file is of pom.xml

![image](https://github.com/user-attachments/assets/76ebd900-8aa2-43b5-a850-771534e86d5e)

Then selecting directory path

![image](https://github.com/user-attachments/assets/1dc8d5b7-2a39-4ece-8aaa-ac890b9077c6)

Selecting hadoop client

![image](https://github.com/user-attachments/assets/ca81dd5d-8cbd-4930-9a97-b298c1e06ab4)

This is what we see in the file manager:

![image](https://github.com/user-attachments/assets/815c607d-63e1-44eb-be91-bb586f210ff4)
We have folders for groupID, then artifactID and then the version

Opening Maven Projects from right side of the screen:

![image](https://github.com/user-attachments/assets/19c5e50f-109d-4f46-a990-1ca3511394a1)

First select clean and run
This command deltes jar file if already exists
![image](https://github.com/user-attachments/assets/af31f989-539d-48fc-bc98-e9885ef72766)

then select package and run
Creating new jar file
![image](https://github.com/user-attachments/assets/2e24fefd-0711-42fc-927e-6c4291bd7b9e)
![image](https://github.com/user-attachments/assets/7ba1c725-56d2-4e19-b22b-3f13d61fd853)

![image](https://github.com/user-attachments/assets/bef548aa-75b8-4986-87b3-4a4a93d6cac4)

This is just the warning and not the error:
![image](https://github.com/user-attachments/assets/b24801c5-758c-40ee-8626-515b5a62c190)

The code has executed successfully:
![image](https://github.com/user-attachments/assets/47431671-b28b-4167-b5de-b30e9f1bfdb8)

Checking counties files in hdfs:
![image](https://github.com/user-attachments/assets/839da4f4-0d0a-4c3a-b0ed-9c2560efdf91)

Create a new Maven Project HDFS_API_1

---

Yarn helps Map reduce to run its resources on Hadoop.
If we don't specify the YARN command, we are not able to execute the Map Reduce Project.
YARN is also responsible for running SPARK on Hadoop.

-tf command is used for verification.
The reason we are putting jar file in the counties folder is in the InputCounties.java file.

---

Understanding InputCounties.java:

```java
package hdfs;
import java.io.IOException;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;

public class InputCounties {


	public static void main(String[] args) throws IOException{
		Configuration conf = new Configuration(); // Refer Configuration details below
		Path dir = new Path("counties");  // Refer Path details below
		FileSystem fs = FileSystem.get(conf); // Refer FileSystem details below
		
		//original code
		/*if(!fs.exists(dir)) {
			fs.mkdirs(dir);
		}*/
		
		//Amit: Above code is replaced as shown below
		if(!fs.exists(dir)) { // Refer exists below
			fs.mkdirs(dir); // Refer mkdirs below
		} else {
			fs.delete(dir, true); // Refer delete below
		}

// For above section refer exists below
		
		System.out.println("Created counties directory in HDFS");
		
		for(int i = 1; i <= 4; i++) {
			String filename = "counties_" + i + ".csv";
			Path localSrc = new Path("counties/" + filename);
			Path dest = new Path("counties/" + filename);  // Refer copyFromLocalFile below
			fs.copyFromLocalFile(localSrc, dest); // Similar to put command 
		}		
		
	}

}
```

Configuration:
Configurations are specified by resources. A resource contains a set of name/value pairs as XML data. Each resource is named by either a String or by a Path. If named by a String, then the classpath is examined for a file with that name. If named by a Path, then the local filesystem is examined directly, without referring to the classpath.

Unless explicitly turned off, Hadoop by default specifies two resources, loaded in-order from the classpath:

    core-default.xml: Read-only defaults for hadoop.
    core-site.xml: Site-specific configuration for a given hadoop installation.

    These two files represent a file system which is HDFS File System.

Applications may add additional resources, which are loaded subsequent to these resources in the order they are added.

Class Path:
Names a file or directory in a FileSystem. Path strings use slash as the directory separator. A path string is absolute if it begins with a slash.

File System:
An abstract base class for a fairly generic filesystem. It may be implemented as a distributed filesystem, or as a "local" one that reflects the locally-connected disk.
static FileSystem 	get(Configuration conf)
Returns the configured filesystem implementation.
fs is a reference pointing to filesystem object


## copyFromLocalFile

public void copyFromLocalFile(Path src,
                      Path dst)
                        throws IOException

The src file is on the local disk. Add it to FS at the given dst name and the source is kept intact afterwards

Parameters:
    src - path
    dst - path
Throws:
    IOException

source is from the local file system and destination is from the hdfs
relative path is being provided for the same


## exists

public boolean exists(Path f)
                throws IOException

Check if exists.

Parameters:
        f - source file
Throws:
    IOException

## mkdirs

public static boolean mkdirs(FileSystem fs,
              Path dir,
              FsPermission permission)
                      throws IOException

create a directory with the provided permission The permission of the directory is set to be the provided permission as in setPermission, not permission&~umask

Parameters:
    fs - file system handle
    dir - the name of the directory to be created
    permission - the permission of the directory
    Returns:
        true if the directory creation succeeds; false otherwise
    Throws:
        IOException
    See Also:
        create(FileSystem, Path, FsPermission)

## delete

@Deprecated
public boolean delete(Path f)
                throws IOException

Deprecated. Use delete(Path, boolean) instead.
Delete a file

Throws:
    IOException

---

Create Project
Create Package: test
Create class: Test

Create a variable whose name is Donald pointing to a string object
And then print it.
What happens in this code internally:

```java
package test;

public class Test {
	
	public static void main(String args[]) {
		String name = "Donald";
		System.out.println("The name of the person is: " + name);
	}

}
```

Output:
The name of the person is: Donald

Working:
java test.Test

java is searching for the main method
name is the reference variable which is local and belongs to main and is stored on stack because name is present on the stack currently
The actual value "Donald" is stored on the Heap

We can store "Donald" with (new String)

We are getting the same output when we used .toString() method with the variable `name`. (name.toString())
Dereferencing means using .toString() method

Employee.java:
package test;

public class Employee {
	
	private int sal;
	private String name;
	
	public Employee(String name, int sal) {
		
		this.name = name;
		this.sal = sal;
	}
}

Test.java:
package test;

public class Test {
	
	public static void main(String args[]) {
//		String name = "Donald";
//		System.out.println("The name of the person is: " + name.toString());
		
		Employee e = new Employee("Donald", 1);
		System.out.println("Employee Details are: " + e);
	
	
	}

}

Output:
Employee Details are: test.Employee@4f2410ac

Here, in this output, memory output is being printed. But we want the original values.

---

Now, we made the changes:

Employee.java:

package test;

public class Employee {
	
	private int sal;
	private String name;
	
	public Employee(String name, int sal) {
		
		this.name = name;
		this.sal = sal;
	}
	
	public String toString() {
		return "Name: " + name + ", Sal: " + sal;
	}
}

Output: Employee Details are: Name: Donald, Sal: 1

---

We want to print what is present inside Configuration conf.
When we made changes in the InputCounties.java and then ran the program from BUILD PATH step:

public static void main(String[] args) throws IOException{
		Configuration conf = new Configuration();
		Path dir = new Path("counties");
		FileSystem fs = FileSystem.get(conf);
		System.out.println(conf);
  
We got the following output:

yarn jar HDFS_API-1.0-SNAPSHOT.jar hdfs.InputCounties
Configuration: core-default.xml, core-site.xml, mapred-default.xml, mapred-site.xml, yarn-default.xml, yarn-site.xml, hdfs-default.xml, hdfs-site.xml
Created counties directory in HDFS

![image](https://github.com/user-attachments/assets/38966272-33b8-48ca-a0c9-44c243182d72)

---

We want to print what is present in the conf files:

Configuration conf = new Configuration();
		System.out.println(conf.get("fs.defaultFS"));
		Path dir = new Path("counties");
		FileSystem fs = FileSystem.get(conf);

Output:
![image](https://github.com/user-attachments/assets/f4f852af-b261-4455-a932-625997c6db0a)








