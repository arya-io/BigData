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

## HDFS Management Options

There are several options for managing HDFS:

Ambari Web UI: Browser-based, HDFS configuration and service management interface. IT is used by Hadoop administrators and not the developers.

NameNode UI: Browser-based interface for basic status monitoring and directory browsing

DataNode UI: Browser-based interface, most commonly used to get block scanner reports (a scanner report is shown later)

HDFS command-line tools: Various command-line tools to interact with the HDFS service and its files, directories, and metadata (described later). Most preferred tool because it provides automation. World is going behind automation.

Manual configuration: Manually editing configuration files (not compatible with Ambari administration)

There are two aspects:
Either You will work as administrator: create production level cluster 
Or Hadoop Developer: solve business problems related to big data

---

## Command-Line Management

⬢ Introduction to command-line management tools:

hdfs dfs: HDFS Shell to manage files, directories, and their metadata (Executed by Hadoop Developers)
hdfs fsck: Checks and reports on file system inconsistencies (does not repair) (Executed by Hadoop Administrator)
hdfs dfsadmin: Reports basic file system information and statistics and performs various file system administration tasks (Executed by Hadoop Administrator)

---

## Determining Storage Space Consumed
► The HDFS Shell du command reports the number of bytes consumed by a file or directory. (Does not
account for replication)
► Syntax: hdfs dfs –du [-s] [-h] [path]

-s: summary
-h: human readable form
-l: list the contents and the file size in bytes
We can't read bytes so we use human readable form

Examples:
![image](https://github.com/user-attachments/assets/6c8687a3-82f8-460c-abb7-c699ee8c5ac2)

---

## Monitoring File System Space
► The HDFS Shell df command reports the file system’s total capacity, along
with the current amount of free and used storage space.
► Syntax: hdfs dfs –df [-h]
► Examples:
![image](https://github.com/user-attachments/assets/48825ddf-aa9b-4ae3-9f10-40e695153921)

---

## Checking File System Consistency

⬢ The HDFS fsck command checks file system consistency.
⬢ Run fsck when:
► There is concern about possible file (data block) corruption
►After an HDFS or hardware malfunction 
► Prior to upgrading HDFS to a newer version
⬢ fsck does not repair data blocks.
► It only reports, unlike Linux fsck (Linux fsck show inconsistencies and can be used to repair)
⬢ An fsck reads block and metadata information from only the NameNode.

hdfs dfs fsck [absolute path of stocks.csv on hdfs] -file -blocks -locations
We will be using:
hdfs fsck /user/cloudera/soccer_scores.csv -files -blocks -locations

![image](https://github.com/user-attachments/assets/215dc8ab-9eb1-4bfb-85f9-0e596e7ea907)

To see the path, use:
hdfs dfs -ls /

► DataNodes are never contacted by fsck. ⬢ Must have access permissions to the directories and files being checked
► The HDFS superuser has access to all files and directories.

---

## fsck Syntax
► Syntax:
► hdfs fsck [path] [options] [> <output_file>]

-files: Reports a list of file and directories checked
-blocks: Reports block ID numbers checked (requires `–files –blocks` syntax)
-locations: Reports a list of DataNodes locations for each block ID number (requires – 
`files –blocks –locations` syntax)

-racks: Prepends the rack name on each reported DataNode location (requires at least – 
`files –blocks –racks` syntax). Really only useful if HDFS rack awareness has been configured (described in another lesson).

-move: Moves files with corrupted data blocks to the `/lost+found` directory
-delete: Deletes files with corrupted data blocks
-openforwrite: List files open for write during fsck (open files are not checked)

---

## Understanding fsck Output:

fsck reports:
⬢ Minimally replicated blocks:
► Blocks having at least one good replica
⬢ Over-replicated blocks:
► Blocks that exceed the file’s replication factor (NameNode will delete)
⬢ Under-replicated blocks:
► Blocks that do not meet the file’s replication factor (NameNode will replicate)
⬢ Mis-replicated blocks:
► Blocks replicated more than once on the same DataNode (NameNode will move)
⬢ Corrupt blocks:
► Blocks where all replicas report checksums errors (NameNode will not repair)
► User action required!

---

## The Primary Output

► hdfs fsck /user/root

![image](https://github.com/user-attachments/assets/dc46cd92-23ca-4978-836d-f645d1499556)

---

## The –files Option
► hdfs fsck /user/root -files

![image](https://github.com/user-attachments/assets/6fa24ff2-d38f-4412-9901-23ad6bcd3d35)

---

## The –blocks Option
► hdfs fsck /user/root –files –blocks
► The file big1 has three blocks, each with a unique block ID.
  ► HFDS generated block pool ID: BP-1472918407-172.17.0.2-1431707688874
    ► The same block pool across all DataNodes
  ► Data block ID: blk_1073742266_1442, and two others
    ► The same ID for all of a block’s replicas

![image](https://github.com/user-attachments/assets/176b26f7-6475-45f0-aafa-1121e5667492)

---

The –locations Option

► hdfs fsck /user/root –files –blocks -locations

![image](https://github.com/user-attachments/assets/14329217-ea8c-4d52-8114-e97d00c1ff95)

---

## The –racks Option
► hdfs fsck /user/root –files –blocks –locations –racks
► Rack name is /default-rack if rack awareness is not configured.
  ► Rack awareness and rack naming are described in another lesson.

/default-rack/ is the rack here
fsck command gives file, blocks, locations, location in which cluster

![image](https://github.com/user-attachments/assets/4ee50cb6-7b38-42ac-8ba8-a6747365376f)

---

## Distributed File System Administration Command

⬢ dfsadmin is a set of HDFS administration tools.
  ► Ambari is gaining more and more of dfsadmin functionality.
⬢ Syntax: hdfs dfsadmin [options]
  ► Over 30 options, only a few options are shown here.
  ► Getting more information and help: hdfs dfsadmin –help
⬢ You must be the HDFS superuser.

You are never a superuser in production.

---

## dfsadmin Examples

When and why to use?

⬢ Transition a NameNode into safe mode:
  ► hdfs dfsadmin –safemode enter
⬢ Force a NameNode checkpoint (generates new fsimage and edits files)
  ► hdfs dfsadmin –saveNamespace
⬢ Or create only a new edits file:
  ► hdfs dfsadmin -rollEdits
Gives output: Log not rolled. Name node is in safe mode.
⬢ Exit NameNode safe mode:
  ► hdfs dfsadmin –safemode leave
⬢ Download the latest fsimage file (useful for doing remote backups):
  ► hdfs dfsadmin -fetchImage

Some of these commands are required when configuring NameNode HA.

![image](https://github.com/user-attachments/assets/b2591161-661c-4c5b-ae33-d46d348af36f)

---

## Heath, Status, and Usage Reports
► hdfs dfsadmin –report can
display status and usage information
similar to the NameNode UI.

![image](https://github.com/user-attachments/assets/36fa9b72-3a76-48be-ab02-22a22adff6b8)

---

## Core Hadoop Configuration Files

⬢ Ambari installs the core Hadoop configuration files in /etc/hadoop/conf.

Here's the information converted into a Markdown table:

| File Name        | File Format              | File Purpose                                                                 |
|------------------|--------------------------|-------------------------------------------------------------------------------|
| core-site.xml    | Hadoop configuration XML | Hadoop core configuration settings that can be used by HDFS, YARN, MapReduce, and others |
| hdfs-site.xml    | Hadoop configuration XML | HDFS configuration settings (NameNode and DataNode)                          |
| yarn-site.xml    | Hadoop configuration XML | YARN configuration settings                                                  |
| mapred-site.xml  | Hadoop configuration XML | MapReduce configuration settings                                             |
| hadoop-env.sh    | Bash script              | Environment variables used by various Hadoop scripts and programs            |
| log4j.properties | Java properties          | System log file configuration settings                                       |

logs are used for debugging


To find the file hdfs-default.xml:
`sudo find / -type f -name hdfs-default.xml`
![image](https://github.com/user-attachments/assets/4e058def-a9da-4267-9d17-cd7cf3654a3d)

To get the size of that particular file:

To find the core-site.xml file:
![image](https://github.com/user-attachments/assets/6fffa45a-8dcf-4898-a010-f14940728212)

---

## Configuration Precedence

► A running job’s actual configuration is a combination of the default, per-site, possibly per-
node, and per-job configuration.

Default Configuration inherits from extends, overrides from Per-Cluster* Configuration inherits from extends, overrides from Per-Job Configuration

*Cluster nodes with different hardware configurations commonly need different *-site.xml files.

![image](https://github.com/user-attachments/assets/d52af6a4-aa05-4510-8c09-c3367e174878)

---

## Final Properties

► Final properties cannot be overridden by user applications.
► For example, no 
–D
prop=value

![image](https://github.com/user-attachments/assets/5c6f647d-5f92-4b67-9f72-a3ffa8423b82)

## Other Framework Configuration Files

⬢ Other Hadoop frameworks often use configuration files with similar formats
and naming conventions.
  ► Examples: *-default.xml, *-site.xml, *-env.sh, *-log4j.properties
⬢ Other frameworks use their own dedicated configuration directories:
  ► /etc/ambari-server/conf
  ► /etc/ambari-agent/conf
  ► /etc/hive/conf
  ► /etc/pig/conf
  ► /etc/zookeeper/conf
  ► and so on...

Find a file hive-site.xml:

sudo find / type f -name hive-site.xml
![image](https://github.com/user-attachments/assets/0140f6f9-3183-4c0e-bf96-0e58cbfbfbee)

---

## Configuration Management Options

⬢ Hadoop includes several options for configuration management:

Here's your information converted into a Markdown table:

| Option                  | Description                                     | Benefit                                                                 |
|-------------------------|-------------------------------------------------|-------------------------------------------------------------------------|
| Ambari Web UI           | Browser-based graphic user management interface | Ease of use, pre-built and ready to go                                 |
| REST APIs: Ambari, WebHDFS, YARN, etc. | HTTP verb (GET, PUT, POST, DELETE) management interface | Integration with other web-based management interfaces, can be used for testing and troubleshooting cluster |
| Manual editing          | Manually edit and distribute configuration files, manually restart services | No reliance on graphic user interface, no need to install Ambari, not compatible with Ambari management |
| Command-line            | Per-framework command-line management utilities | Scriptable, no reliance on a graphic user interface                    |

---

## Lesson Review

1. Which component of HDFS is responsible for maintaining the namespace of the
distributed filesystem?
1. What is the default file replication factor in HDFS?
1. True or False: To input a file into HDFS, the client application passes the data to the
NameNode, which then divides the data into blocks and passes the blocks to the
DataNodes.
1. Which property is used to specify the block size of a file stored in HDFS?
1. The NameNode maintains the namespace of the filesystem using which two sets of files?
1. What does the following command do? hdfs dfs -ls -R /user/thomas/
1. What does the following command do? hdfs dfs -ls /user/thomas/

---

# Ingesting Data into HDFS

## Topics to be covered:
Topics Covered
• Options for Data Input • The Hadoop Client • WebHDFS
• Overview of Sqoop
• Importing a Data
• The Sqoop Export Tool • Exporting to a Table
• Labs: HDFS Importing/Exporting from/to RDBMS using Sqoop
• Lab: Importing Log Data into HDFS using Flume

---

## What is Ingestion in Big Data?

Big Data Ingestion involves connecting to various data sources, extracting the data, and detecting the changed data.

---

## Options for Data Input

![image](https://github.com/user-attachments/assets/1906c7cf-9e14-44c1-8b77-c88b49740cc9)

At the center, we have Hadoop.

Hadoop client command, to be given from edgenode: hdfs dfs -put
Edgenode is the hardware machine where hadoop client side library is installed.
We can ingest the data into Hadoop using Connectors to RDBMS.
Sqoop is used to import the data RDBMS into HDFS.
Flume is used to capture streaming data and push it to HDFS.
Storm is also used to process the data.
nifi is developed by hotnworks. nifi is the name of the company (niagara files)
Spark Streaming
MapReduce
WebHDFS

---

## The Hadoop Client
The put Command
  • Same as copyFromLocal
Perfect for inputting local files into HDFS
  • Useful in batch scripts
Usage:
  hdfs dfs -put <localsrc> ... <dst>

---

## Java Native API Versus WebHDFS Access

hdfs dfs: 
• Requires installation and client HDFS configuration files
• Uses RPC to communicate 
• Useful for users and administrators in scripts and the command line

WebHDFS REST API commands:
• Requires no installation or client configuration files 
• Uses HTTP to communicate 
• Useful for programmers writing Web apps

![image](https://github.com/user-attachments/assets/deba3137-5890-4e58-b7a7-618a1aa13f92)

We need to transfer data from one machne to another. In order to do that we need IP address for both because we have to specify it in port. But we don't have any. Then how, do they know where the namenode is?

It is done through this command:
sudo find / -type f -name core-site.xml

![image](https://github.com/user-attachments/assets/0bbabbfa-0d5b-4691-b2cf-74a683c9b91f)

cat /etc/hadoop/conf.pseudo/core-site.xml

![image](https://github.com/user-attachments/assets/da904864-9ae9-4d33-a0f4-bc17bdd63227)
![image](https://github.com/user-attachments/assets/0bce61b7-d129-47a4-bf85-500d593db9f7)

Client machine is edge node. This information must be with the client machine.
Anything inside /etc will automatically inside class path of java application.
Web Client knows HTTP. It uses the prot 50070. And it understands only HTTP protocol. It has to use RESTAPI to interact with Hadoop.
RPC information resides in core-site.xml
Java application uses this information.

What is REST API?
Suppose We are creating a application using Python's Flask framework.
it should communicate with hadoop, extract or load into hadoop.
problem is that it is not a java based application but a python. Then how to make a connectivity. Then use web based api to interact with hadoop.

---

## WebHDFS Features

⬢ Supports all HDFS file administration operations
⬢ Enables access to HDFS from programming languages other than Java
  ► API access is through Java only.
⬢ Enables faster access than hdfs dfs when the client is remote to the cluster
⬢ Requires no additional servers
  ► WebHDFS is built into the NameNode and DataNode
⬢ Uses the full bandwidth of the Hadoop cluster for moving data
  ► Read and write operations are redirected to the appropriate DataNodes.
⬢ Is compatible with Kerberos authentication
  ► Uses Simple and Protected GSSAPI Negotiation Mechanism (SPNEGO), which extends Kerberos to Web
applications
⬢ Is completely open source

---

## WebHDFS Enabled by Default

► To verify that WebHDFS is enabled, check either the hdfs-site.xml file or Ambari.

![image](https://github.com/user-attachments/assets/5cb1a866-7f5e-4e24-b227-dce115c69e5c)

![image](https://github.com/user-attachments/assets/0f351bb1-6f09-459d-a920-db430b84ba53)

---

## WebHDFS Operations

⬢ The following WebHDFS operations, formatted using the proper URIs, enable
HDFS file access and administration.

There is a method known as HOST, GET, POST, PUT, DELETE and other things. These are methods of HTTP. These are web based operations under HTTP.

Here's the information converted into a Markdown table:

| HTTP GET            | HTTP PUT            | HTTP POST          | HTTP DELETE         |
|---------------------|---------------------|--------------------|---------------------|
| OPEN                | CREATE              | APPEND             | DELETE              |
| GETFILESTATUS       | MKDIRS              |                    |                     |
| LISTSTATUS          | RENAME              |                    |                     |
| GETCONTENTSUMMARY   | SETREPLICATION      |                    |                     |
| GETFILECHECKSUM     | SETOWNER            |                    |                     |
| GETHOMEDIRECTORY    | SETPERMISSION       |                    |                     |
| GETDELEGATIONTOKEN  | SETTIMES            |                    |                     |
|                     | RENEWDELEGATIONTOKEN |                    |                     |
|                     | CANCELDELEGATIONTOKEN|                    |                     |

If we don't specify, the defult command is GET.
---

## WebHDFS Examples (1)

curl stands for c url

⬢ All programs and applications performing WebHDFS operations use the URI syntax:
  ► http://<NameNode>:50070/webhdfs/v1/<path>?op=<operation_and_arguments>
http://<NameNode>:50070/webhdfs/v1/<path>: This is known as WebHDFS API prefix
⬢ The curl command can be used to test WebHDFS operations.
⬢ Creating a directory named mydata:
  ► curl -i -X PUT "http://<NameNode>:50070/webhdfs/v1/web/mydata?op=MKDIRS&user.name=jason”
  This means we are creating a new folder `mydata` and the operation to create is `op=MKDIRS` and the owner of this directory is `jason`
⬢ Listing a directory named mydata:
  ► curl -i "http://<NameNode>:50070/webhdfs/v1/web/mydata?op=LISTSTATUS&user.name=jason”
  The name of the operation is LISTSTATUS. It comes under HTTP method GET. The default method is GET if we do not specify any method.
⬢ Reading a file named webdata:
  ► curl -i -L
"http://<NameNode>:50070/webhdfs/v1/web/mydata/webdata?op=OPEN&user.name=jason”

---

## WebHDFS Examples (2)

⬢ Writing a file is a two-step process.
1. Create a file name on the NameNode.
2. Write the file contents to a DataNode.
►WebHDFS ensures that files larger than an HDFS block are written across multiple
DataNodes.

⬢ Create a file by creating a file name on the NameNode:
► curl -i -X PUT "http://<NameNode>:50070/webhdfs/v1/web/mydata/largefile.json?op=CREATE"
► The output from this command includes the URI used to write data to the file.
⬢ Write to the file by sending data to the DataNodes:
► curl –i –X PUT –T largefile.json
“http://<DataNode>:50075/webhdfs/v1/web/mydata/largefile.json?op=CREATE&user.name=root&n
amenoderpcaddress=node1:8020&overwrite=false”
⬢ Curl can perform a write operation using a single command that performs both steps:
► curl –i –X PUT largefile.json –L
“http://<NameNode>:50070/webhdfs/v1/web/mydata/largefile.json?op=CREATE&user.name=root"

---

## WebHDFS

REST API for accessing all of the HDFS file system interfaces:

• http://host:port/webhdfs/v1/test/mydata.txt?op=OPEN

• http://host:port/webhdfs/v1/user/root/data?op=MKDIRS

• http://host:port/webhdfs/v1/test/mydata.txt?op=APPEND

---

LAB: Using WebHDFS Commands

1) Following HTTP GET request List a Directory /user/cloudera
curl -i "http://quickstart.cloudera:50070/webhdfs/v1/user/cloudera?op=LISTSTATUS"

![image](https://github.com/user-attachments/assets/88f64846-8317-4a2a-9736-34bc18c201cf)

Till Transfer-Encoding part, it is known as Header
From FileStatuses part, it is known as Payload
Important Header parameter: Content-Type: application/json
This means payload is of json type

2) Following HTTP GET request Open and Read a File /user/cloudera/stocks.csv

curl -i -L "http://quickstart.cloudera:50070/webhdfs/v1/user/cloudera/stocks.csv?op=OPEN"

![image](https://github.com/user-attachments/assets/cd898be0-ddef-4ee7-aa62-e886203b9576)
![image](https://github.com/user-attachments/assets/dcf02792-080e-4999-b8d4-0da2d8730d33)
![image](https://github.com/user-attachments/assets/c3dd595b-a7d6-4b54-91b3-b0fe59288bb3)

3) The following PUT request makes a new directory in HDFS named /user/cloudera/data:

curl -i -X PUT "http://quickstart.cloudera:50070/webhdfs/v1/user/cloudera/data?user.name=cloudera&op=MKDIRS"

![image](https://github.com/user-attachments/assets/f419691d-7ba5-45f8-ac8e-7fe48d66a829)

Verify if the folder is created or not using the hadoop client command:

hdfs dfs -ls

![image](https://github.com/user-attachments/assets/f0f1c3af-3685-4d3c-818d-077ff7fc64d8)

4) Below is a command to write the file on hdfs using single curl command instead of 2 commands
   
cd /home/cloudera/labs/demos //Assuming that there is small_blocks.txt

curl -i -X PUT -T small_blocks.txt  "http://quickstart.cloudera:50075/webhdfs/v1/user/cloudera/small_blocks.txt?op=CREATE&user.name=cloudera&namenoderpcaddress=quickstart.cloudera:8020&overwrite=false"

![image](https://github.com/user-attachments/assets/0b7f0a28-ef31-46c7-95fd-bf1b2306a453)

DELETE A SPECIFIC FILE:

![image](https://github.com/user-attachments/assets/3614dd54-c493-459d-bad8-dbe293fcb1c4)

![image](https://github.com/user-attachments/assets/f6c8a584-9dc5-4e33-b0cc-790da6b11eb7)

---

## NOW We will be working on Big Data VM, for that we have to start the Hadoop first.

bash Start-Hadoop-Hive.sh

![image](https://github.com/user-attachments/assets/5b1c881f-f074-497e-a69c-6083c4e6f341)

Now, run the first command:

curl -i "http://talentum-virtual-machine:50070/webhdfs/v1/user/talentum?op=LISTSTATUS"

![image](https://github.com/user-attachments/assets/b63375a2-d71a-4358-a770-4b19ccf34118)

Now, running the second command:

curl -i -L "http://talentum-virtual-machine:50070/webhdfs/v1/user/talentum/shared/stocks.csv?op=OPEN"

The above query was giving error: File not found
It was because the file wasn't present in HDFS system.
Then we executed this command and added that file into hdfs system:

hdfs dfs -put /home/talentum/stocks.csv /user/talentum

Again, while adding the file, we were encountering an issue due to some problem with Datanode. So we stopped Hadoop cluster and started it again and it resolved the issue.

hdfs dfs -put /home/talentum/stocks.csv /user/talentum

Now, the file was added in the HDFS. Then we executed our Step 2 command:

curl -i -L "http://talentum-virtual-machine:50070/webhdfs/v1/user/talentum/shared/stocks.csv?op=OPEN"

![image](https://github.com/user-attachments/assets/2afdd416-0828-4063-aed7-d547205abd8b)

The above command is used to open a specified file present in HDFS using webhdfs client.

Then we wanted to add small_blocks.txt into hdfs using webhdfs client.

Before doing that we ran this command in order to check if the file is present in the correct directory or not. If it wasn't present, then we just copied it to the target directory:

cp /home/talentum/small_blocks.txt /home/talentum

And this is the final command:
curl -i -X PUT -T small_blocks.txt "http://talentum-virtual-machine:50075/webhdfs/v1/user/talentum/small_blocks.txt?op=CREATE&user.name=talentum&namenoderpcaddress=localhost:9000&overwrite=false"

![image](https://github.com/user-attachments/assets/630fc08d-1ca5-4b8a-b138-279b096203ec)


We added small_blocks.txt into hdfs using webhdfs client.

Final Output:
![image](https://github.com/user-attachments/assets/bdc69c46-eeca-4806-a823-39c2782f5a91)


---





---

There is a project going on. Multiple teams are working. one team making request. they ewill be providning data ot next tema. that team is going to use thier own programming language. first tema needs to give the data. collect the output of first command in a file. and that file willb e given as input to the second team. use vim editor.

vim automatelist.sh
![image](https://github.com/user-attachments/assets/c25c72f8-18d9-4e69-889d-4983c8a6330d)

Content of shell file:

#!/bin/bash

curl -i "http://talentum-virtual-machine:50070/webhdfs/v1/user/talentum?op=LISTSTATUS" > automateoutput.txt

bash automatelist.sh
![image](https://github.com/user-attachments/assets/5ba09b76-f794-4158-85df-199cb926bb29)

cat automateoutput.txt
![image](https://github.com/user-attachments/assets/26eb2b2d-0212-4bfc-97d0-159d41d8d135)


SUSPENDED MODE:
Switch off the Virtual Machine by keeping the state intact.
Also known as HIBERNATION.

We can use script shell for running LISTSTATUS from bigdatavm into cloudera vm. 
Just copy-paste the file from Windows File Explorer and make necessary changes.

curl -i "http://$1:50070/webhdfs/v1/user/cloudera?op=LISTSTATUS" > automateoutput.txt

./automatelist.sh quickstart.cloudera

---------

![image](https://github.com/user-attachments/assets/6066b605-08ee-449c-a0e8-f8ddd290441e)

---

## Demo: Putting Files in HDFS with Java

How to build a java MR application to ingest data into Hadoop cluster (HDFS)
Question: What is the meaning of build a java application?
Creating a source file (.java)
Compiling the source file (.class)
Create a library of this application (.jar)

Steps for building a Java MR application using Eclipse as an IDE
1) Create an Eclipse Java Project
2) Create a package(s) in that project based on source code (Look at the package statements)
3) Import the source files (.java) in the respective project and package.
4) Compile the code
5) Compilation errors related to class path issues
6) Solution to above issue is to add the respective libraries in the classpath of the project.
7) Compile it again, if no error indicate that compilation is successful
8) Create a jar file (library)
9) Verify the contents of the jar file
10) If everything is fine then run the jar on Hadoop Cluster.

---

Eclipse is a location on the file system where your code will work.
Project in Eclipse is a folder in worksspace.

Go to files, workspace > switch workspace > others > OK

![image](https://github.com/user-attachments/assets/af78585f-412a-4ec3-b1bd-e89c6beec0b5)

We are going to create our new project.

To extract the rar file

Follow Steps:
Create Project: File > New > Project > Project Name > HDFS_API

![image](https://github.com/user-attachments/assets/4faa3eeb-eb26-4bfd-ae16-a2fc11c5a92b)



### JRE vs JDK
We want to build and then run the application. Therefore, we will be choosing the `Use default jre (currently 'jdk1.7.0_67-cloudera') in jre section while creating project.
Eclipse does not have its own JDK.

Now click Next

bin files in Java means .class files.

Click Finish.

Project has been created.

![image](https://github.com/user-attachments/assets/3f80c255-a11e-4533-a83b-20c42105fcf5)

src will contain .java files.

![image](https://github.com/user-attachments/assets/4f88660b-332b-4a33-8f34-3ad042994a3b)

We are now creating package with name 'hdfs'.

![image](https://github.com/user-attachments/assets/c621691e-ccb7-4b17-9235-3ef191076e4e)

![image](https://github.com/user-attachments/assets/6f2f6941-f702-4f4a-a256-13124064168c)

Right click on project name.
Then create the package.
This hdfs package will help us to work with HDFS.


![image](https://github.com/user-attachments/assets/d898291e-4acf-4f92-a983-4c358a7a5316)

Step 6: To remove erros present in the code file

Right click on Project > Build Path > Configure Build Path > Libraries > Add external jars > File System > usr > lib > hadoop > client 
Then select all jar files
Then press ok two times

Error will be removed from the code file.

Autosave helps in compiling automatically.
Saving the code automatically compiles it on Eclipse.

Step 8: Creating a jar file

Right click on project > Export > Java > Jar Files > Next
Browse jar files > File system > home > cloudera > shared > data > HDFS_API

Rename jar file: inputcounties.jar
Click on ok > next (*2) > Finish

Step 9: Verify the jar file:

Checking if the jar file has been created:

![image](https://github.com/user-attachments/assets/2fb0acbc-6008-4ec9-aa3b-4a0e7caff367)


Step 10: To run on Hadoop cluster, use

Go to the Folder where jar is present i.e., give the absolute path

yarn jar inputcounties.jar

To run java application on Hadoop, we have to use YARN

echo $?

The above command is giving error.

yarn jar inputcounties.jar hdfs.InputCounties

here, inputcounties.jar is the jar file and InputCounties is the class Name present in the Java code

![image](https://github.com/user-attachments/assets/cc65a643-3c26-444b-8d27-0814a04217db)

![image](https://github.com/user-attachments/assets/be98ebd5-626e-42e7-ae8e-1d9051a6d425)

![image](https://github.com/user-attachments/assets/dedb7b56-3f0a-48ac-beeb-db28b24d74de)























