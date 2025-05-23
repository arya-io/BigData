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

## 💻 Types of Client Applications

Client applications are software programs that interact with a server to retrieve or send data. They come in various types depending on how and where they operate. Let's explore the main types:

---

### 🌐 1. **Web Client**

**Definition:**  
A **Web Client** is a client application that runs inside a web browser. It doesn't need to be installed on your device.

**Key Features:**
- No installation required ✅  
- Runs on web technologies like **HTML**, **CSS**, and **JavaScript**  
- Needs an active **internet connection** to function properly  
- Easy to update and access from multiple devices 🌍  

**Examples:**
- **Gmail** (email through browser)  
- **Google Docs** (online word processing)  
- **Microsoft Outlook Web App**

**Use Case:**  
Great for users who want quick access from anywhere without installing anything.

---

### 🖥️ 2. **Thick Client (or Fat Client)**

**Definition:**  
A **Thick Client** is installed directly on the user’s device. It can do most of the processing locally and doesn't rely heavily on the server.

**Key Features:**
- Requires installation on your computer 💽  
- Performs **heavy processing** on the client side  
- May sync or fetch data from the server but can work offline as well  
- Typically **faster** for tasks requiring more resources  

**Examples:**
- **Microsoft Word** (desktop version)  
- **Adobe Photoshop**  
- **Outlook (desktop version)**

**Use Case:**  
Best for users who need full-featured, responsive apps with or without internet.

---

# 💻 Setting Up IntelliJ IDEA on BigDataVM

We will now do the same Java HDFS project, but this time using **IntelliJ IDEA** inside **BigDataVM** (no Eclipse here).

---

## 📥 Step 1: Download IntelliJ Installer

- Download the `ideaintellj` file and put it inside the **home directory** of BigDataVM.
- The file is usually in `.tar.gz` format — this is a compressed file.

---

## 🧹 Step 2: Clean Up (Remove Existing IntelliJ)

If IntelliJ is already installed via Snap, remove it:

```bash
sudo snap remove intellij-idea-community
```

This ensures a **fresh setup**.

---

## 📦 Step 3: Extract the IntelliJ Tar File

We are now going to extract the `.tar.gz` file.

📘**Note:**  
- `.gz` is a gzip compressed format  
- `tar` is used to extract it  
- `man tar` shows the **manual** for the `tar` command  

### 📌 Command Breakdown:  
```bash
sudo tar -zxvf 'Copy of ideaIC-2018.2.8.tar.gz' -C /opt/
```

✅ Explanation of options:
- `z`: unzip `.gz` files (gzip)
- `x`: extract
- `v`: verbose (shows progress)
- `f`: file (specifies the file name)
- `-C /opt/`: extract contents into `/opt/` directory

📷 Extraction in progress:

![Extracting IntelliJ](https://github.com/user-attachments/assets/16dc1973-6efd-46ea-a1f3-5a66afafc183)

📷 Extraction done:

![Extracted](https://github.com/user-attachments/assets/b35cf63a-fb3c-4cc5-aa89-f50707b7237d)  
![Progress](https://github.com/user-attachments/assets/e03de164-db22-427e-80f4-4a927a2ca389)

---

## 📁 Step 4: Navigate to the Extracted Folder

Let's explore the extracted files.

### Check if it exists:
```bash
ls -lh /opt/
```
📷 Result:

![opt folder](https://github.com/user-attachments/assets/7ae6434e-36ef-495a-a880-ebb8c5ca4c69)

📝 `opt/` is a system folder where software is often installed manually.

---

### Move into `/opt`:
```bash
cd /opt
ls
ls -lh
```
📷 Result:

![cd opt](https://github.com/user-attachments/assets/6c4b149d-1212-4a9e-8a9a-1fb1c0779444)

---

### List IntelliJ Files:

```bash
ls -lh idea-IC-182.5262.2/
```

📷 Inside IntelliJ folder:

![ideaIC contents](https://github.com/user-attachments/assets/14753432-b8fc-4719-9ba2-2cb1b0101ec2)  
![idea files](https://github.com/user-attachments/assets/308ea8f5-3193-485e-9e4c-5b35e35f8316)

---

## 🧠 Quick Recap: Terminal Commands Used

| Command | Purpose |
|--------|---------|
| `sudo snap remove intellij-idea-community` | Remove old IntelliJ |
| `gunzip` / `gzip` | Used for .gz compression/decompression |
| `man tar` | Opens help/manual for tar |
| `tar -zxvf file.tar.gz -C /opt/` | Extract tar.gz to /opt |
| `ls -lh /opt/` | List files with sizes in /opt |
| `cd /opt` | Navigate to /opt |
| `ls -lh idea-IC-*` | Check IntelliJ files |

---

# 🚀 Launching IntelliJ IDEA & Setting Up HDFS Project

We’ve already extracted IntelliJ to `/opt/`. Now we’ll launch it and set up our **Java MapReduce project (HDFS_API)** for editing and execution.

---

## 🗂️ Step 1: View IntelliJ Contents

Let’s make sure IntelliJ files are correctly extracted:

```bash
ls -lh idea-IC-182.5262.2/
```

📷 IntelliJ folder structure:

![IntelliJ contents](https://github.com/user-attachments/assets/308ea8f5-3193-485e-9e4c-5b35e35f8316)

---

## 🛠️ Step 2: Copy HDFS_API Project to Workspace

Now we copy the `HDFS_API` project from **Staging Area** to your **LABS_HOME directory**, which is your workspace inside BigDataVM.

📷 Copying Project:

![Copying to Labs_Home](https://github.com/user-attachments/assets/d5defc89-dfd7-470d-a48f-23c57bbe9b6c)

📷 Confirmation (destination view):

![Labs_Home structure](https://github.com/user-attachments/assets/20cd258d-da2a-4019-9ded-751c119c1bea)

📷 Project Folder:

![HDFS_API copied](https://github.com/user-attachments/assets/e2993d72-15c0-4846-8741-e64a3fc6f875)

---

## 🐚 Step 3: Run IntelliJ IDEA

Inside the extracted IntelliJ folder, there are **many shell scripts**.

We need to run `idea.sh` to start the IntelliJ GUI.

📷 List of scripts:

![Shell scripts in IntelliJ](https://github.com/user-attachments/assets/febe7a3e-6b6f-4c6e-be28-a5980ea81123)

### ▶️ Run the script:
```bash
./idea.sh
```

📷 After running the script, IntelliJ starts and a welcome/config screen appears:

![IntelliJ welcome screen](https://github.com/user-attachments/assets/ec22c7df-23f7-4138-ad44-7edb6433f606)

➡️ Click **OK** to continue.

---

## 📋 Step 4: IntelliJ First Launch Screen

Once loaded, you’ll see the full interface of IntelliJ IDEA where you can **import your existing HDFS_API project** and start working on it.

📷 Main screen:

![IntelliJ GUI loaded](https://github.com/user-attachments/assets/feedff35-a79a-4022-af5f-66c93c65dafd)

---

## 🧠 Summary of Steps:

| Step | Description |
|------|-------------|
| ✅ View IntelliJ files | `ls -lh idea-IC-*` |
| 📁 Copy Project | Move `HDFS_API` to workspace |
| 💻 Launch IntelliJ | Run `./idea.sh` |
| 🔧 Start Config | Accept and load IntelliJ GUI |
| 📦 Ready to import project | You’ll now import `HDFS_API` into IntelliJ |

---

# 🎨 Setting Up IntelliJ IDEA GUI & Creating Project

Let’s go through the setup screens of IntelliJ after launching it. This is the final step before you can start coding!

---

## 🌙 Step 1: Select Theme

Choose a **theme**. Most people prefer **Darcula** (dark mode) for better eye comfort.

📷 Theme selection screen:

![Darcula Theme](https://github.com/user-attachments/assets/7721b60d-2f64-4a2b-82b9-3dfe6dad6c2b)

---

## 💻 Step 2: Desktop Entry & Launcher Script

✔️ Check **Desktop Entry** – this allows IntelliJ to appear in your system menu for easy access later.

✔️ Select **Launcher Script** – this helps launch IntelliJ from terminal using `idea.sh`.

📷 Screens:

![Desktop entry](https://github.com/user-attachments/assets/a8d7b788-00c0-4a45-b595-0b468a4002b1)  
![Launcher script](https://github.com/user-attachments/assets/6006b891-82ed-4540-be33-93df37fa9a87)

---

## 🧩 Step 3: Configure Default Plugins

This screen shows available **tools and plugins** IntelliJ can support:

📷 Plugin setup screen:

![Default plugins](https://github.com/user-attachments/assets/6e416d83-ed66-4499-89d3-a4c73264ead3)

### Key Plugin Areas:
- **Build Tools** 🧱: Helps compile/build your Java projects.
- **Version Control** 🔧: Git for managing code changes.
- **Test Tools** 🧪: For automated testing.
- **Swing UI Designer** 🎨: Java’s GUI tool (like Python’s Tkinter).
- **Android** 🤖: For mobile development.
- **Other Tools**: General utilities.
- **Plugin Development** 🧩: For writing IntelliJ plugins.

Click **Next**.

---

## 🌟 Step 4: Featured Plugins

Here you can optionally install additional tools like:

📷 Featured Plugins:

![Featured plugins](https://github.com/user-attachments/assets/41049e86-2531-4e39-b6b2-6ff20f9ca163)

- **Scala**: If working with Scala in the future.
- **IdeaVim**: Vim keybindings support.

✅ Choose if needed or leave default, then click **Start using IntelliJ IDEA**.

📷 Final launch screen:

![Start IntelliJ](https://github.com/user-attachments/assets/92221197-2f7d-4a93-b36d-57f9eddbf20f)

---

## 🏁 Step 5: Create a New Project

Now we are ready to create or import a Java project!

📷 Create Project Screen:

![Create new project](https://github.com/user-attachments/assets/3ff04d4a-2be7-4b7d-92a0-d66160f8d180)

Choose:
- **Java** as the language
- **Project SDK**: Select `jdk1.7.0_67-cloudera` or whichever is installed

📌 If importing existing project like `HDFS_API`, choose **Import Project** instead of New Project.

---

## 🧠 Summary:

| Step | Action |
|------|--------|
| 🎨 Choose Theme | Pick Darcula or Light |
| 🖥️ Enable Desktop Entry | So IntelliJ is easy to access later |
| 📂 Enable Launcher Script | Use from terminal with `idea.sh` |
| 🧩 Plugin Setup | Keep default or add more (like Git, Vim, Scala) |
| 🚀 Launch IntelliJ | Click “Start using IntelliJ IDEA” |
| 📁 Create/Import Project | Set up new or open existing HDFS_API project |

---

You're now ready to **configure the build path, fix errors, compile your Java HDFS code, and create the JAR** inside IntelliJ.
---

# ☕ Setting Up a Maven Java Project in IntelliJ IDEA

In Eclipse, libraries were often **bundled manually** by adding `.jar` files directly. In IntelliJ, we use **Maven** to automate the management of libraries and dependencies via a central repository.

---

## 🗃️ What is Maven?

- **Maven** is a **build automation tool** used primarily for Java projects.
- It manages:
  - Project structure
  - Dependencies (external libraries)
  - Build lifecycle (compiling, testing, packaging)

---

## 🧱 Why Use Maven in IntelliJ?

- IntelliJ doesn’t have libraries pre-installed.
- We need to **connect to a code repository (Maven Repository)**.
- Dependencies like **Hadoop client libraries** can be pulled automatically from the repo.

---

## 🛠️ Step-by-Step: Create a Maven Project in IntelliJ

### 1. **Create a New Maven Project**
In the IntelliJ welcome screen or File → New → Project:

- Choose **Maven**
- Make sure the **Project SDK is Java 1.8**
- 📷 ![Select Maven](https://github.com/user-attachments/assets/f82efa36-dc9a-450a-8524-4806ba252156)

Click **Next**

---

### 2. **Configure Maven Project Details**

You will need to provide:
- `groupId`: like a namespace (e.g., `org.example`)
- `artifactId`: project name (e.g., `HDFS_API`)

📷 Group ID:
![group id](https://github.com/user-attachments/assets/8033d701-0859-4f92-9d8a-f0a0be404983)

📷 Artifact ID:
![artifact id](https://github.com/user-attachments/assets/295115a5-c34e-4e80-90a2-df3903c419e9)

Click **Next**

---

### 3. **Project Location**
- IntelliJ will create the project in: `~/IdeaProjects/HDFS_API`
- 📷 ![project location](https://github.com/user-attachments/assets/daf42a48-03c0-4dad-a228-37bf8a94ffe2)

Click **Finish**

---

### 4. **Enable Auto-Import**

Once the project is created, IntelliJ will ask:

> "Maven projects need to be imported."

✅ Click **Enable Auto-Import**  
📷 ![enable autoimport](https://github.com/user-attachments/assets/2e4fb860-9b71-4826-9549-2d78b529c4fb)

This starts downloading all dependencies from Maven Central.

---

## 📄 What is `pom.xml`?

The file `pom.xml` (Project Object Model) is the **heart of every Maven project**.

It contains:
- `groupId`
- `artifactId`
- `version`
- `dependencies`: Libraries required (like Hadoop)

📌 You will add dependencies for Hadoop here later.

---

## 🖥️ Navigate in Terminal

To explore the project from terminal:

```bash
cd ~/IdeaProjects/
ls
```

📷 ![terminal navigation](https://github.com/user-attachments/assets/79b57e7c-4707-481c-96c6-18cd50c23d61)

---

## ✅ Summary

| Step | Description |
|------|-------------|
| 🔧 Maven Project | Use Maven instead of plain Java for dependency management |
| 🏷️ groupId/artifactId | Uniquely identify your project |
| 📦 pom.xml | Lists all project dependencies |
| 🌐 Maven Repo | Automatically pulls required `.jar` files |
| 📁 Location | Saved in `~/IdeaProjects/HDFS_API` |
| 📥 Auto-import | Makes sure dependencies are downloaded and updated |

---

You're now ready to **edit `pom.xml` and add Hadoop dependencies**.

---

# ☁️ Setting Up HDFS Java Project in IntelliJ with Maven (BigDataVM)

---

## 🧭 Project Structure (Maven)

After creating the Maven project:

- The project folder `HDFS_API` should contain:
  - `pom.xml` → Project descriptor
  - `src/` → Source code directory

📷 ![project structure](https://github.com/user-attachments/assets/9dc5e940-999b-4f9a-844a-58d1fa9f101e)

---

## ❓ Why Use Different Environments?

- **Cloudera** (GUI-based) vs. **BigDataVM** (Server/Terminal-based)
- Reason: **More learning!**
  - Understand **automation**
  - Avoid **comfort zone**
  - Real-world production environments are **server-based** (less UI)

✅ Note: Eclipse *can* be used on BigDataVM, but using IntelliJ gives experience with another powerful IDE.

---

## 🧾 Maven Identity

Every Maven project is uniquely identified by:
- **groupId**: Like an organization name (e.g., `org.example`)
- **artifactId**: Project name (e.g., `HDFS_API`)
- **version**: Version number (e.g., `1.0-SNAPSHOT`)

📷 ![maven identifiers](https://github.com/user-attachments/assets/9f7049af-054f-47e9-ac16-b6b4a8d277ac)

---

## 🗃️ Folder Structure Comparison

| Tool      | Location of Code Files        |
|-----------|-------------------------------|
| Eclipse   | `src/`                        |
| IntelliJ  | `src/main/java/`              |

---

## 📦 Creating a Package in IntelliJ

1. Navigate to: `src > main > java`
2. Right-click on `java` → New → Package
3. Name the package `hdfs`

📷 ![create package](https://github.com/user-attachments/assets/6076f390-dde1-4fd1-b154-4902a2532ee1)

---

## 📂 Add Java File to the Package

- Move `InputCounties.java` from STAGING AREA to:  
  `src/main/java/hdfs/`

📷 ![move file](https://github.com/user-attachments/assets/cedfaa2c-1aed-44bd-b5b1-9d387adb3ee3)  
📷 ![file placed](https://github.com/user-attachments/assets/62bb386a-d56c-40b6-bf63-706d973f7cee)

---

## ❌ Why is the Java File Showing Errors?

- Because **required Hadoop libraries are missing**
- Maven **does not automatically know** which dependencies you need

✅ You must **explicitly declare libraries** inside `pom.xml`

---

## 🔍 Check Your Hadoop Version

Run the command in terminal:

```bash
hadoop version
```

📷 ![hadoop version](https://github.com/user-attachments/assets/159241d4-f4f1-4bf9-bae2-e13bb986ba49)

🟢 **Required version**: `2.7.3`  
You need the **Hadoop client-side library for version 2.7.3**

---

## 🛠️ What’s Next?

You'll now add this dependency to `pom.xml`:

```xml
<dependencies>
  <dependency>
    <groupId>org.apache.hadoop</groupId>
    <artifactId>hadoop-client</artifactId>
    <version>2.7.3</version>
  </dependency>
</dependencies>
```

---

# ☁️ Adding Hadoop Dependency in Maven (IntelliJ IDEA – BigDataVM)

---

## 🔍 Step 1: Search for the Correct Dependency

To add Hadoop client library for version `2.7.3`, search:

```
maven repository hadoop client 2.7.3
```

📷 ![dependency search result](https://github.com/user-attachments/assets/5c639aaf-8e75-4891-8732-2d9c6f88a6e1)

---

## 📥 Step 2: Add the Dependency in `pom.xml`

Your Maven project already has:
- `groupId`
- `artifactId`
- `version`

Now, add the Hadoop dependency inside the `<dependencies>` tag of your `pom.xml` file:

```xml
<dependency>
  <groupId>org.apache.hadoop</groupId>
  <artifactId>hadoop-client</artifactId>
  <version>2.7.3</version>
</dependency>
```

📷 ![adding dependency](https://github.com/user-attachments/assets/4ac8bd3e-a1e8-4c60-8708-ef7f45e6bd76)

---

## ✅ Step 3: Confirm Dependency is Working

- **InputCounties.java** errors should disappear automatically
- **External Libraries** should now show `Hadoop 2.7.3`

📷 ![external libraries](https://github.com/user-attachments/assets/e14b2895-9758-4e7d-adfd-b0b8cc557a0f)

---

## ⚠️ Important Notes

- Always use the **same Hadoop version** across team projects.
- Mismatched versions can lead to **runtime or compilation errors**.

---

## 📦 Maven Handles Jar Creation

- `pom.xml` also controls **how the final `.jar` file is created**
- It handles:
  - Dependencies
  - Build lifecycle
  - Plugins

📷 ![jar control by pom](https://github.com/user-attachments/assets/76ebd900-8aa2-43b5-a850-771534e86d5e)

---

## 📂 Selecting Directory and Library for Setup

1. Choose directory for project or output
📷 ![directory selection](https://github.com/user-attachments/assets/1dc8d5b7-2a39-4ece-8aaa-ac890b9077c6)

2. Confirm `hadoop-client` library selection
📷 ![hadoop library selected](https://github.com/user-attachments/assets/ca81dd5d-8cbd-4930-9a97-b298c1e06ab4)


---

# 🧰 Creating a JAR File using Maven in IntelliJ IDEA

---

## 📁 Maven Folder Structure (in File Manager)

When Maven builds the project, it creates nested folders in this format:

```
~/.m2/repository/
└── groupID/
    └── artifactID/
        └── version/
```

📷 ![file manager view](https://github.com/user-attachments/assets/815c607d-63e1-44eb-be91-bb586f210ff4)

---

## 📦 Accessing Maven Lifecycle in IntelliJ

1. Go to the **right-side panel** and click on **Maven Projects**  
📷 ![maven projects panel](https://github.com/user-attachments/assets/19c5e50f-109d-4f46-a990-1ca3511394a1)

---

## 🧹 Step 1: Run `clean`

- Deletes the old `.jar` file (if any exists)
📷 ![clean command](https://github.com/user-attachments/assets/af31f989-539d-48fc-bc98-e9885ef72766)

---

## 📦 Step 2: Run `package`

- This compiles the code and creates a new `.jar` file in the `target/` folder
📷 ![package command](https://github.com/user-attachments/assets/2e24fefd-0711-42fc-927e-6c4291bd7b9e)  
📷 ![jar file generated](https://github.com/user-attachments/assets/7ba1c725-56d2-4e19-b22b-3f13d61fd853)  
📷 ![jar confirmation](https://github.com/user-attachments/assets/bef548aa-75b8-4986-87b3-4a4a93d6cac4)

---

## ⚠️ Maven Warning (Safe to Ignore)

- This message is a **warning**, *not* an error.
- Warnings do not block the jar creation process.
📷 ![warning](https://github.com/user-attachments/assets/b24801c5-758c-40ee-8626-515b5a62c190)


---

# ✅ Execution and Maven Project Recap

---

## 🏁 Code Execution Successful

- The **MapReduce job** using the JAR file ran successfully.
📷 ![execution success](https://github.com/user-attachments/assets/47431671-b28b-4167-b5de-b30e9f1bfdb8)

---

## 📂 Verifying Output in HDFS

- Checked for the `counties` files in HDFS to confirm output generation.
📷 ![hdfs output](https://github.com/user-attachments/assets/839da4f4-0d0a-4c3a-b0ed-9c2560efdf91)

---

## 🆕 Creating a New Maven Project

- Created a new Maven project named **HDFS_API_1** for further experimentation or versioning.

---

## 🧠 Additional Concepts

### 🔹 YARN (Yet Another Resource Negotiator)
- YARN **allocates resources** and **manages jobs** in Hadoop.
- It is essential for running:
  - **MapReduce**
  - **Spark**
- If YARN is not invoked properly, MapReduce jobs will **not execute**.

### 🔹 Why place the JAR file in the `counties` folder?
- The **InputCounties.java** file is **hardcoded** or **configured** to use data from the `counties` directory.

---

## 🔍 `-tf` Command
- Used to **verify** the contents of a `.jar` file before execution.
  ```bash
  jar -tf <filename>.jar
  ```

---

# 🧾 **Understanding `InputCounties.java` in Hadoop HDFS**

This Java program creates a **directory named `counties` in HDFS** and copies multiple `.csv` files from the local file system into that HDFS directory.

---

## 🧠 **Core Logic Explained**

```java
Configuration conf = new Configuration();
Path dir = new Path("counties");
FileSystem fs = FileSystem.get(conf);
```

### 🔧 **What is `Configuration`?**
- It loads the configuration files of Hadoop:
  - `core-default.xml` – Default Hadoop settings (read-only).
  - `core-site.xml` – Site-specific Hadoop settings.
- These define the **file system type**, e.g., HDFS.

```java
if (!fs.exists(dir)) {
    fs.mkdirs(dir);
} else {
    fs.delete(dir, true);
}
```

### 📁 **What happens here?**
- If the HDFS directory `counties` **doesn't exist**, it's created using `mkdirs()`.
- If it **already exists**, it's deleted (using `delete()`) and then created fresh.
- This ensures that the directory is **reset** for each run.

```java
for (int i = 1; i <= 4; i++) {
    String filename = "counties_" + i + ".csv";
    Path localSrc = new Path("counties/" + filename);
    Path dest = new Path("counties/" + filename);
    fs.copyFromLocalFile(localSrc, dest);
}
```

### 🔁 **What's happening here?**
- A loop runs 4 times (i=1 to 4).
- For each iteration:
  - It creates a filename like `counties_1.csv`, `counties_2.csv`, etc.
  - It copies each file from the **local system** into the **HDFS directory** using `copyFromLocalFile()`.

---

## 🧰 **Key Classes & Methods in Hadoop FS**

### ⚙️ `Configuration`
- Holds **Hadoop settings** loaded from XML files.
- Can load multiple resources using paths or classpath.

---

### 📂 `Path`
- Represents a file or directory in the **HDFS or local file system**.
- It uses **slashes `/`** as directory separators.
- Absolute if it starts with `/`, else relative.

---

### 🌐 `FileSystem`
- Abstract class for both **local** and **distributed** file systems like HDFS.
- Accessed using:
  ```java
  FileSystem fs = FileSystem.get(conf);
  ```

---

## 🔎 **Important Methods**

### 📄 `copyFromLocalFile(Path src, Path dst)`
- Copies a file from **local filesystem** to **HDFS**.
- Local file remains **unchanged**.
- Similar to the shell command:
  ```
  hadoop fs -put localfile hdfsfile
  ```

---

### ❓ `exists(Path f)`
- Checks if the file or directory **exists** in the file system.
- Returns `true` or `false`.

---

### 🏗️ `mkdirs(Path dir)`
- Creates a **directory structure** in HDFS.
- Takes **path** and **permission** (optional).

---

### 🗑️ `delete(Path f, boolean recursive)`
- Deletes a **file or directory**.
- The `true` flag means:
  - If it’s a directory, delete **everything inside recursively**.
- Deprecated simpler version:
  ```java
  fs.delete(dir);  // Old style
  ```

---

## ✅ **Output**
If everything runs successfully:
```
Created counties directory in HDFS
```

---

# 🧾 **Creating a Project and Understanding Code Behavior**

In this section, we will learn how to create a **Java project**, work with **strings**, and explore object references and memory management.

---

## 🧠 **Creating and Running a Simple Java Program**

### **Step-by-Step Explanation**

```java
package test;

public class Test {
    
    public static void main(String args[]) {
        String name = "Donald";
        System.out.println("The name of the person is: " + name);
    }
}
```

### 🖨️ **Output:**
```
The name of the person is: Donald
```

---

### 🔍 **What's Happening Internally?**

1. **String Object**:
   - `"Donald"` is a **string literal**.
   - The **reference variable `name`** points to the string literal `"Donald"`.
   - **Memory Allocation**:
     - The **string value** ("Donald") is stored in the **Heap** (which holds objects).
     - The **reference variable `name`** is stored on the **Stack** (where local variables are stored).

2. **Dereferencing**:
   - Dereferencing means using a method (like `.toString()`) to access the content of the object the reference is pointing to.
   - For example, `name.toString()` gives you the same result.

---

## 🧰 **Creating and Using Custom Classes**

### 🧑‍💻 **Employee.java** Class Definition

```java
package test;

public class Employee {
    
    private int sal;
    private String name;
    
    public Employee(String name, int sal) {
        this.name = name;
        this.sal = sal;
    }
}
```

### 👨‍💼 **Test.java** with Employee Object

```java
package test;

public class Test {
    
    public static void main(String args[]) {
        Employee e = new Employee("Donald", 1);
        System.out.println("Employee Details are: " + e);
    }
}
```

### 🖨️ **Output:**
```
Employee Details are: test.Employee@4f2410ac
```

### 📌 **Explanation:**
- In the above code, **`System.out.println(e)`** prints the **memory address** of the `Employee` object.
- This happens because **`toString()` method** is not overridden, so the default `toString()` implementation from `Object` class is used, which returns the **memory address** of the object.

---

## 🧑‍🔧 **Improving Output by Overriding `toString()`**

### 🔧 **Modified `Employee.java` with `toString()` Method**

```java
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
```

### 🖨️ **Output After Change:**
```
Employee Details are: Name: Donald, Sal: 1
```

### 📌 **What's Changed?**
- Now, the **`toString()` method** has been overridden to return the **actual values** of the object (`name` and `sal`), instead of just printing the memory reference.

---

## 🧑‍💻 **Printing Configuration Details from `InputCounties.java`**

We want to print the configuration settings used in Hadoop when running the program. Here's how we do it:

### **Modified `InputCounties.java`**

```java
public static void main(String[] args) throws IOException {
    Configuration conf = new Configuration();
    Path dir = new Path("counties");
    FileSystem fs = FileSystem.get(conf);
    System.out.println(conf);
}
```

### 🖨️ **Output:**

```
yarn jar HDFS_API-1.0-SNAPSHOT.jar hdfs.InputCounties
Configuration: core-default.xml, core-site.xml, mapred-default.xml, mapred-site.xml, yarn-default.xml, yarn-site.xml, hdfs-default.xml, hdfs-site.xml
Created counties directory in HDFS
```

### 📌 **Explanation:**
- The `conf` object holds the Hadoop **configuration resources** (like `core-site.xml`, `mapred-site.xml`, etc.).
- These are the default configuration files loaded by Hadoop, which define the system settings for HDFS, MapReduce, YARN, etc.

---

## 🖨️ **Printing Specific Configuration Values**

If you want to print a specific value from the configuration, you can use the `get()` method:

### **Modified `InputCounties.java` to Print `fs.defaultFS`**

```java
Configuration conf = new Configuration();
System.out.println(conf.get("fs.defaultFS"));
Path dir = new Path("counties");
FileSystem fs = FileSystem.get(conf);
```

### 🖨️ **Output:**
![image](https://github.com/user-attachments/assets/f4f852af-b261-4455-a932-625997c6db0a)

### 📌 **Explanation:**
- `conf.get("fs.defaultFS")` retrieves the value of `fs.defaultFS`, which specifies the default file system URI.
- This value is typically defined in the `core-site.xml` configuration file, and the output will show the **URI of the default file system** (like HDFS or local).

---

# 🧠 **Big Data Project Notes – Beginner Friendly**

## 💻 Development Environment: BigDataVM

All development is carried out inside a virtual machine pre-configured with Big Data tools (Hadoop, Cloudera, etc.). Ensure the VM is properly set up before starting.

---

## 🧩 **Task 1: Ingest CSV into HDFS using Java (Hadoop Client)**

### 📁 Project Details:
- **Project Name:** `Stock_Upload`
- **Group ID:** `org.cdac`
- **Package Name:** `org.cdac.pune`
- **Class Name:** `UploadStock`
- **File to Ingest:** `stocks.csv`

---

### ⚙️ **Step-by-Step Guide**

#### 1️⃣ Create Maven Project:
Use a Maven-based Java project to manage dependencies and structure.

**Directory Structure:**
```
Stock_Upload/
├── src/
│   └── main/
│       └── java/
│           └── org/
│               └── cdac/
│                   └── pune/
│                       └── UploadStock.java
├── pom.xml
```

#### 2️⃣ Java Code: UploadStock.java

```java
package org.cdac.pune;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;

import java.io.IOException;

public class UploadStock {

    public static void main(String[] args) throws IOException {
        // Configuration for Hadoop
        Configuration conf = new Configuration();
        Path localFilePath = new Path("path/to/your/stocks.csv");  // Local file path
        Path hdfsDestPath = new Path("/stocks/stocks.csv");  // HDFS destination path

        // Get FileSystem object for HDFS
        FileSystem fs = FileSystem.get(conf);

        // Copy the file from local system to HDFS
        fs.copyFromLocalFile(localFilePath, hdfsDestPath);
        
        System.out.println("File successfully uploaded to HDFS");
    }
}
```

This Java program reads a local file (`stocks.csv`) and writes it into HDFS.

> 📸 **Reference Screenshots:**
![Project Structure](https://github.com/user-attachments/assets/54392749-b429-4e65-8299-4f2ff1f6f4ec)  
![Java Code Snippet 1](https://github.com/user-attachments/assets/c30a70cb-3089-48c5-9ada-d4afa3d158c3)  
![Java Code Snippet 2](https://github.com/user-attachments/assets/32e83170-59ee-418e-804e-d802b60e86f9)

---

### ✅ **Expected Output After Execution**
Once the program runs successfully:
- `stocks.csv` should be visible inside HDFS.

> 📸 **Output Verification:**
![HDFS View 1](https://github.com/user-attachments/assets/16eee65c-b7cf-44fe-9c74-d4360ba87c02)  
![HDFS View 2](https://github.com/user-attachments/assets/33cf4d63-14d1-41a7-836b-be4c8d25b90d)

---

## 🚀 **Task 2: Run JAR on Cloudera**

### 🧳 Step-by-Step Instructions

#### 1️⃣ Package Java Code into a JAR
Use Maven to create the JAR file:
```bash
mvn clean package
```
Your JAR file will be located at:
```
target/Stock_Upload-1.0-SNAPSHOT.jar
```

#### 2️⃣ Copy JAR to Cloudera VM
Use a method like `scp` or shared folders to move the `.jar` to the Cloudera VM.

#### 3️⃣ Run the JAR in Cloudera Terminal
Inside Cloudera:
```bash
hadoop jar Stock_Upload-1.0-SNAPSHOT.jar org.cdac.pune.UploadStock /path/to/stocks.csv /user/hdfs/stocks.csv
```

> 📸 **Execution Screenshots:**
![Cloudera Jar Add](https://github.com/user-attachments/assets/4a63bc1c-060f-47c1-93e4-6d3fcc6b8651)  
![Terminal Output 1](https://github.com/user-attachments/assets/fe7de6fb-f545-478f-aa54-e9f87a644597)  
![Terminal Output 2](https://github.com/user-attachments/assets/d67bb699-e2d9-42d8-92f4-092ac2ef6a43)  
![HDFS Confirmation](https://github.com/user-attachments/assets/7ba6fda6-82aa-4384-a503-e3309409e29d)

---

## 📝 Summary
| Component | Description |
|----------|-------------|
| **Language** | Java |
| **Tool** | Hadoop Client |
| **CSV File** | stocks.csv |
| **Goal** | Ingest CSV into HDFS |
| **Run** | Locally via Java → JAR → Cloudera |

---

## 🎯 Tips for Beginners:
- 🧪 Test your code locally before deploying to Cloudera.
- 🛠 Use meaningful log messages in your Java code to debug easily.
- 🧾 Always check file paths carefully—both local and HDFS paths.
- 💡 Try exploring Hadoop FileSystem commands to verify data:
```bash
hadoop fs -ls /user/hdfs/
hadoop fs -cat /user/hdfs/stocks.csv
```

---
