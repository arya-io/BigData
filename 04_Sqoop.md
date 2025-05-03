# 🐾 **Understanding the Code: Abstract Class & Polymorphism in Java**

## 🔥 **Key Concept: Abstraction & Polymorphism**

* **Abstraction**: Hiding internal details and showing only necessary features.
* **Polymorphism**: "Many forms" — the same method behaves differently based on the object.

> **`Animal dog = new Dog();`**
> This is called **dynamic polymorphism**:
> Super class **reference** → points to sub class **object**.

---

## 🐕 **Code Breakdown: Step by Step**

### 1️⃣ **Abstract Class: Animal**

```java
abstract class Animal {
    abstract void makeSound();
}
```

* `abstract` means **cannot create object** of `Animal` directly.
* **Abstract method** `makeSound()` has **no body** here.
  → Subclasses **must** override this method.

---

### 2️⃣ **Dog, Cat, Cow — Subclasses**

Each class **extends** `Animal` and **overrides** `makeSound()` method.

```java
class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Woof");
    }
}
```

Similarly, `Cat` says `"Meow"` and `Cow` says `"Moo"`.

---

### 3️⃣ **Main Class Execution**

```java
public class AnimalSound {
    public static void main(String[] args) {
        Animal dog = new Dog();
        Animal cat = new Cat();
        Animal cow = new Cow();

        dog.makeSound(); // Woof
        cat.makeSound(); // Meow
        cow.makeSound(); // Moo
    }
}
```

#### 💡 What's Happening Here?

* `Animal dog = new Dog();` → Superclass reference holding subclass object.
* When you call `dog.makeSound()`, **Dog's** version runs, not Animal's (because Animal is abstract).
* This is called **Runtime Polymorphism** (or **Dynamic Method Dispatch**).

---

## 🎯 **Important Points to Remember**

* An **abstract class** can have abstract and non-abstract methods.
* You **cannot instantiate** an abstract class directly.
* **`@Override`** ensures you are correctly overriding the method from superclass.
* Using `Animal dog = new Dog();` allows **flexibility** — you can change object types (Dog, Cat, Cow) but call them using `Animal`.

---

## 📊 **Visual Concept**

*(Keep your existing images linked here — e.g., class hierarchy diagram)*

* Abstract `Animal` ➡️  Subclasses: `Dog`, `Cat`, `Cow`
* Each subclass **defines** its own `makeSound()`.

---

## 🧠 **Think Like This**

| Code                      | What It Means                     |
| ------------------------- | --------------------------------- |
| `Animal dog = new Dog();` | Superclass ref → Subclass object  |
| `dog.makeSound();`        | Runs Dog's `makeSound()` → `Woof` |
| `Animal cat = new Cat();` | Runs Cat's `makeSound()` → `Meow` |

---

## 🌱 **Beginner Tip: Why Use This?**

* If you have **many animals**, you don’t write separate code for each.
* You can just say:

```java
Animal a = new Lion(); 
a.makeSound();
```

And it will call Lion's version.
➡️ Makes code **flexible** and **easy to extend**!

---

# 🐘 **Sqoop: Importing RDBMS Data into Hadoop HDFS**

## 🎯 **Why Sqoop?**

* Our data is in **RDBMS** (like MySQL, Oracle, etc.).
* But **Hadoop** processes data only when it's in **HDFS**.

> **Goal:** Pull (import) data from **RDBMS** ➡️ **HDFS** for big data processing.

---

## 🚀 **How Sqoop Works: Step by Step**

1. ✅ **Client executes** a Sqoop command.
2. 🔄 **Sqoop converts** the command into a **MapReduce** job.
3. 🔌 **Plugins** connect Sqoop to different RDBMS databases (like MySQL, Oracle, etc.).
4. 📦 Data is **imported** into HDFS.

> 💡 Sqoop uses **Map-only tasks** in MapReduce for importing.

![Sqoop Flow](https://github.com/user-attachments/assets/943fe696-4f41-40dd-aa19-964e7be220e2)

---

## 🛠️ **The Sqoop Import Tool**

### ✅ **Mandatory things to specify in the import command:**

* **Connection string** → `--connect`
* **Username & Password** → `--username` and `--password`

  * Uses **JDBC** to authenticate the user.
* **Data source:**

  * **Table** → `--table` (for full table import)
  * or **Custom SQL query** → `--query` (for selective import)

---

## 📥 **Example: Importing a Table**

```bash
sqoop import \
--connect jdbc:mysql://host/nyse \
--table StockPrices \
--target-dir /data/stockprice/ \
--as-textfile
```

### 🔍 **Explanation:**

| Command Part                       | Meaning                                              |
| ---------------------------------- | ---------------------------------------------------- |
| `--connect jdbc:mysql://host/nyse` | Connect to MySQL DB `nyse` on `host`                 |
| `--table StockPrices`              | Import table `StockPrices`                           |
| `--target-dir /data/stockprice/`   | Store imported data in HDFS path `/data/stockprice/` |
| `--as-textfile`                    | Store data in **textfile** format                    |

---

## ⚙️ **What Happens When We Execute?**

* This command **launches a MapReduce job**.
* By default, it uses **4 map tasks**.
* ✔️ All 4 tasks run **in parallel** (because MapReduce is parallel processing).

### 💡 **Why parallel?**

* MapReduce splits the data and processes chunks **simultaneously** ➡️ making the import faster!

---

## 🌱 **Beginner Tip: Why Use Sqoop?**

* When you want to **move large volumes of structured data** from RDBMS ➡️ HDFS.
* Saves you from writing complex ETL code — Sqoop handles it all for you!
* Supports importing in **various formats**: textfile, Avro, Parquet, etc.

---

## ✅ **Quick Revision Points**

* Sqoop is a **bridge** between RDBMS and Hadoop.
* Uses **MapReduce jobs** under the hood (map-only jobs).
* Supports **parallel imports** using multiple map tasks.
* Uses **JDBC connection** for authentication and data pull.
* You specify:

  * **DB connection**
  * **Table or query**
  * **HDFS target path**
  * **File format**

---

# 🎯 **Sqoop: Importing Specific Columns (Projection)**

## 🌱 **Goal: Get Only Required Columns**

* Sometimes, we don’t want **all columns** from a table — just a few.
* This is called **Projection** in database terms (selecting specific columns).

---

## 📥 **Example: Importing Specific Columns**

```bash
sqoop import \
--connect jdbc:mysql://host/nyse \
--table StockPrices \
--columns StockSymbol,Volume,High,ClosingPrice \
--target-dir /data/dailyhighs/ \
--as-textfile \
--split-by StockSymbol \
-m 10
```

---

## 🔍 **Breaking It Down**

| Command Part                                     | Meaning                                                    |
| ------------------------------------------------ | ---------------------------------------------------------- |
| `--columns StockSymbol,Volume,High,ClosingPrice` | Only these columns will be imported (**projection**)       |
| `--target-dir /data/dailyhighs/`                 | Store in HDFS path `/data/dailyhighs/`                     |
| `--as-textfile`                                  | Save as textfile format                                    |
| `--split-by StockSymbol`                         | Split data across **map tasks** using `StockSymbol` column |
| `-m 10`                                          | Launch **10 map tasks** (parallel workers)                 |

---

## ⚡ **What is `--split-by`? (Load Balancing Explained)**

* Sqoop imports data using multiple **map tasks** (parallel workers).
* `--split-by` decides **how the data is split** among them.
* You should choose a column that:

  * Has **unique** or evenly spread values.
  * Ensures **equal distribution** ➡️ so each map task gets a fair share.

### 📊 **Formula:**

```
No. of rows in split column / No. of map tasks
```

➡️ This ensures **no overlapping** and avoids **performance hit**.

> 💡 If `--split-by` is not specified, **primary key** is used by default.

---

## 🛠️ **About `-m` (Map Tasks Count)**

* `-m` decides **how many parallel map tasks** will be launched.
* In this case: `-m 10` ➡️ launches **10 tasks** pulling data simultaneously.

### 🔥 **Default:**

If `-m` is **not specified**, Sqoop uses **4 map tasks** by default.

> **Earlier table import example** didn’t have `-m`, so it used **4** map tasks.

---

## ✅ **Quick Revision Points**

* **Projection** → Select only specific columns using `--columns`.
* **Load Balancing** → Use `--split-by` for **equal data split** across tasks.
* **Parallelism** → Control number of tasks using `-m` (default is 4).
* Use a **good column** (like `StockSymbol`) for splitting:

  * Unique or evenly spread
  * Not necessarily the primary key

---

## 🚀 **Best Practice Tips**

* Always use `--split-by` for **large imports** to avoid performance issues.
* Use `-m` to **increase parallelism** (e.g., `-m 10` or higher) when you have more cluster capacity.
* Choose **split-by column** carefully to ensure **balanced** load across map tasks.

---

# 🔎 **Sqoop: Importing Data Using a SQL Query**

## 🌱 **Goal: Filter & Import Only Matching Data**

* Instead of importing the whole table ➡️ we import **only rows matching our SQL query**.
* Example: Import **stock prices** where **Volume ≥ 1,000,000**.

---

## 📥 **Example: Importing Using Query**

```bash
sqoop import \
--connect jdbc:mysql://host/nyse \
--query "SELECT * FROM StockPrices WHERE s.Volume >= 1000000 AND \$CONDITIONS" \
--target-dir /data/highvolume/ \
--as-textfile \
--split-by StockSymbol
```

---

## 🔍 **Breaking It Down**

| Command Part                                    | Meaning                                                          |
| ----------------------------------------------- | ---------------------------------------------------------------- |
| `--query "SELECT * FROM StockPrices WHERE ..."` | Import only rows matching the **query**                          |
| `AND \$CONDITIONS`                              | **Mandatory placeholder** — Sqoop replaces this during splitting |
| `--target-dir /data/highvolume/`                | Store imported data in HDFS `/data/highvolume/`                  |
| `--as-textfile`                                 | Save as **textfile** format                                      |
| `--split-by StockSymbol`                        | Split rows using `StockSymbol` column                            |

---

## ⚠️ **Important Rule: When Using `--query`**

* **`--split-by` is mandatory** ➡️ because Sqoop must split query results across tasks.
* **`\$CONDITIONS`** is **required** inside query:

  * Sqoop injects split ranges using this placeholder.
  * Example:

    ```sql
    WHERE s.Volume >= 1000000 AND StockSymbol >= 'A' AND StockSymbol < 'F'
    ```

> 💡 Without `\$CONDITIONS`, **Sqoop query fails**.

---

## 🧠 **Why Use Query Import?**

* Filter data directly **at source** (RDBMS) ➡️ reduces data transfer.
* Useful when:

  * Importing only **recent records**
  * Importing **filtered subset** (like high-volume stocks)

---

# 📂 **Copying and Verifying Files (Lab Task)**

## ✅ **Step 1: Copy `salaries.txt` to LABS\_HOME**

> Copy from **staging area** to your working lab directory.

![Copy Image](https://github.com/user-attachments/assets/6378aba5-6161-45c5-9d93-9d7b1e681de1)

---

## ✅ **Step 2: Confirm Your Lab**

We are currently in:

> **Lab3.1**

![Lab Image](https://github.com/user-attachments/assets/38fd515f-d743-403e-95e2-379a7475d2b9)

---

## ✅ **Step 3: Copy File to `/tmp` Directory**

```bash
cp salaries.txt /tmp/
```

![Copy to tmp](https://github.com/user-attachments/assets/eb511973-a879-4597-a9fa-e793e68a74d4)

---

## ✅ **Step 4: Verify File is Present**

```bash
ls /tmp
```

Look for `salaries.txt` in the list.

![Verify](https://github.com/user-attachments/assets/dd2098e7-c86e-4f3e-94e0-f342e6e10e7a)

---

## ✅ **Step 5: Connecting to Database**

> Connect to your RDBMS to check tables or run queries.

![DB Connect](https://github.com/user-attachments/assets/f87e86f3-91aa-40dd-8818-180e6b1a7ee3)

---

## 🔥 **Quick Revision Points**

* Use **`--query`** when importing filtered/selected rows.
* **`\$CONDITIONS`** placeholder is **mandatory** in query.
* Must specify **`--split-by`** column when using query import.
* Always verify files with `ls` after copying.
* **Lab flow:**

  1. Copy file ➡️
  2. Verify file ➡️
  3. Connect to DB ➡️
  4. Run Sqoop import

---

## 🎯 **Beginner Tip: Remember This!**

* **Table import** is for **full table** ➡️ easy but heavy.
* **Query import** is for **filtered data** ➡️ efficient for big data jobs.

---

# 🐬 **MySQL: Creating Database & Table for Sqoop Practice**

## ✅ **Step 1: Login to MySQL**

```bash
mysql -u root -p
```

* Enter password: `cloudera`

🔐 **Password Prompt Appears**

> Type: `cloudera` (default password)

![MySQL Login](https://github.com/user-attachments/assets/1bc137c6-b772-404a-8a46-82c077164613)

---

## ✅ **Step 2: Create a New Database `test`**

```sql
CREATE DATABASE test;
```

✔️ Database created successfully!

![Create DB](https://github.com/user-attachments/assets/cf8d2aa9-ea11-4773-a034-4f6b47818673)

---

## ✅ **Step 3: Check Existing Databases**

```sql
SHOW DATABASES;
```

* You’ll see a list of databases including your new **`test`** DB.

![Show DBs](https://github.com/user-attachments/assets/6a86aa99-9095-4f7d-b5ff-0fae5073929b)

---

## ✅ **Step 4: Switch to the `test` Database**

```sql
USE test;
```

✔️ Switched to database **`test`**!

![Use DB](https://github.com/user-attachments/assets/c7238cd0-e422-4003-b155-8badcbf65808)

---

## ✅ **Step 5: Create Table `salaries`**

```sql
CREATE TABLE salaries (
  gender varchar(1),
  age int,
  salary double,
  zipcode int
);
```

✔️ Table **`salaries`** created successfully!

![Create Table](https://github.com/user-attachments/assets/d2491f82-e154-4b8c-9aac-b00903e0ea9e)

---

## 📝 **Table Structure Explanation**

| Column    | Data Type  | Meaning                           |
| --------- | ---------- | --------------------------------- |
| `gender`  | varchar(1) | Stores `M` (male) or `F` (female) |
| `age`     | int        | Stores age (number)               |
| `salary`  | double     | Stores salary (decimal values)    |
| `zipcode` | int        | Stores area zip code              |

---

## 🔥 **Quick Revision Points**

* ✅ Login using `mysql -u root -p`
* ✅ Create DB: `CREATE DATABASE test;`
* ✅ See all DBs: `SHOW DATABASES;`
* ✅ Switch DB: `USE test;`
* ✅ Create table: `CREATE TABLE salaries (...)`

---

## 🎯 **Beginner Tip: Remember This!**

* **Databases** ➡️ like folders 🗂️ for storing tables.
* **Tables** ➡️ like spreadsheets 📊 with rows and columns.
* **SQL Commands** ➡️ always end with `;`

---

# 📊 **MySQL: Loading Data & Altering Table**

---

## ✅ **Step 6: Show Tables in Database**

```sql
SHOW TABLES;
```

✔️ Shows all tables present in current DB (like `salaries`)

![Show Tables](https://github.com/user-attachments/assets/a71f47ce-44fa-4509-85c1-e45bebeb2d70)

---

## ✅ **Step 7: Describe Table Structure**

```sql
DESC salaries;
```

✔️ Shows **columns**, their **types**, and if they accept `NULL`.

![Describe Table](https://github.com/user-attachments/assets/65ddef56-5ee1-4942-9e84-124082e02170)

---

## ✅ **Step 8: Load Data from File into Table**

```sql
LOAD DATA LOCAL INFILE '/tmp/salaries.txt' 
INTO TABLE salaries 
FIELDS TERMINATED BY ',';
```

✔️ This **loads data** from file `/tmp/salaries.txt` into `salaries` table.

📦 **File Content Format**:

```
M,25,50000,94107
F,30,60000,94016
...
```

* Data is **comma-separated** (CSV).

![Load Data](https://github.com/user-attachments/assets/18948897-6790-4e4d-9573-9e1d438ad89b)

---

## ✅ **Step 9: Verify Row Count**

```sql
SELECT COUNT(*) FROM salaries;
```

✔️ Confirms how many rows got loaded.

![Count Rows](https://github.com/user-attachments/assets/c046383c-398e-4f48-9153-9f7f3ef9eb83)

---

## ✅ **Step 10: Alter Table — Add Primary Key**

```sql
ALTER TABLE salaries 
ADD COLUMN `id` INT(10) UNSIGNED PRIMARY KEY AUTO_INCREMENT;
```

✔️ Adds new column:

* **`id`** ➡️ becomes unique row number (`1,2,3…`)
* **Primary Key** ➡️ avoids duplicate rows
* **Auto Increment** ➡️ automatically numbers new rows

![Alter Table](https://github.com/user-attachments/assets/b9593375-976f-4ed3-8233-b1e369af15b0)

---

## 📝 **Result: Updated `salaries` Table**

| id  | gender | age | salary  | zipcode |
| --- | ------ | --- | ------- | ------- |
| 1   | M      | 25  | 50000.0 | 94107   |
| 2   | F      | 30  | 60000.0 | 94016   |
| ... | ...    | ... | ...     | ...     |

---

## 🔥 **Quick Revision Points**

* ✅ `SHOW TABLES;` ➡️ lists tables
* ✅ `DESC table;` ➡️ shows structure
* ✅ `LOAD DATA LOCAL INFILE` ➡️ bulk load from CSV
* ✅ `SELECT COUNT(*)` ➡️ verify rows
* ✅ `ALTER TABLE ADD COLUMN id` ➡️ add auto-increment primary key

---

## 🎯 **Beginner Tip: Remember This!**

* `LOAD DATA LOCAL INFILE` ➡️ fastest way to bulk insert from file 📂
* Always **add a Primary Key** (`id`) ➡️ better for querying, indexing & Sqoop split operations!

---

# 🚀 **Import MySQL Table into Hadoop (HDFS) using Sqoop**

---

## ✅ **Step 11: Describe Updated Table**

```sql
DESC salaries;
```

✔️ Now the table shows **`id`** as **Primary Key** and **Auto Increment**.

![Describe Updated Table](https://github.com/user-attachments/assets/e3835905-2204-4e60-93bf-3d8f958f5a6a)

---

## ✅ **Step 12: Display Table Records**

```sql
SELECT * FROM salaries;
```

✔️ Displays **all rows** with newly added **`id`** column.

![Display Table](https://github.com/user-attachments/assets/377384a6-2b1f-4a43-82ac-49b1d5ea129a)

---

## 🌟 **📦 Now the Database is Ready for Hadoop Import!**

---

# 🐘 **Step 13: Import Table into HDFS using Sqoop**

```bash
sqoop import \
--connect jdbc:mysql://quickstart.cloudera:3306/test \
--driver com.mysql.jdbc.Driver \
--username root \
--password cloudera \
--table salaries
```

✔️ This command will:

* Connect to **MySQL DB** at `quickstart.cloudera:3306/test`
* Use user: `root`, password: `cloudera`
* Import the **`salaries`** table
* Store it into **HDFS** (default folder like `/user/cloudera/salaries`)

---

### 🎯 **What Happens Internally?**

* 🚀 **Sqoop launches a MapReduce job** ✅
* 🗂️ Data is **pulled from MySQL** and **written to HDFS**
* ⚙️ By default, 4 parallel tasks (mappers) are launched

---

## 🖥️ **Output of MapReduce Program**

![Sqoop MapReduce](https://github.com/user-attachments/assets/f84b567f-36ac-456c-b2d4-4c6e4c215809)
![Sqoop MapReduce 2](https://github.com/user-attachments/assets/91073306-8e84-4328-95dd-0e77124b093c)

✔️ This shows **tasks running** and **completed** successfully!

---

## 🌐 **Understanding Web UI Ports**

| 🖥️ **Tool**                 | 🌐 **Port** | 🔎 **Purpose**           |
| ---------------------------- | ----------- | ------------------------ |
| **Resource Manager (YARN)**  | `8088`      | Shows **active jobs**    |
| **MapReduce History Server** | `19888`     | Shows **completed jobs** |

### ➡️ Access via Browser:

* Resource Manager: `http://localhost:8088`
* History Server: `http://localhost:19888`

![YARN 19888](https://github.com/user-attachments/assets/d22209da-2f7c-4794-b800-bd724646955f)

---

## 📝 **Quick Revision Points**

* ✅ `DESC salaries;` ➡️ shows table structure
* ✅ `SELECT * FROM salaries;` ➡️ displays rows
* ✅ `sqoop import ...` ➡️ pulls table into HDFS
* ✅ MapReduce job runs to do the actual import

---

## 🎯 **Beginner Tip: Remember This!**

* **Sqoop** bridges 🛣️ between **RDBMS** ➡️ **Hadoop HDFS**
* MapReduce does the import job in **parallel** 🚀
* `8088` ➡️ Active jobs; `19888` ➡️ Completed jobs 🗂️

---

Absolutely! Here's your next polished and complete **notes section**, including **all your images**, keeping the same **clear, beginner-friendly** style with **emojis** 🌟🚀.

---

# 🐘 **Verifying Imported Data in HDFS**

---

## ✅ **Step 14: Verify if the 'salaries' Folder Exists in HDFS**

Check whether the data has been successfully imported by listing the HDFS directories.

```bash
hdfs dfs -ls
hdfs dfs -ls salaries
```

📂 This will list the **salaries** folder and its files inside HDFS.

![Verify HDFS Directory](https://github.com/user-attachments/assets/48ceb853-bd81-4e71-9261-0439990f65f7)

---

## 🔎 **Step 15: Analyze Data Distribution Across Map Tasks**

* The data size for each file (map task output) is approximately:
  **0 bytes, 272 bytes, 241 bytes, 238 bytes, 272 bytes**
* 📊 **Almost equally distributed!**
* **Why?**

  * **Split-by** was not manually specified.
  * **Default behavior:** Sqoop automatically picks the **primary key** (`id` column in our case) for splitting the data among mappers.

---

## 📌 **Important Points About Map Tasks**

* 🛠️ **All map tasks run in parallel**, not sequentially!
* 🏎️ This parallel execution ensures **faster data import**.

---

# 🔥 **Exploring MapReduce Job Details**

---

## 🗺️ **Step 16: View MapReduce Job in Resource Manager UI**

You can see the running/completed applications in YARN Resource Manager (port 8088).

![MapReduce Job View](https://github.com/user-attachments/assets/2f04843e-c795-4cda-83ef-360c1368e859)

---

## 🆔 **Step 17: Find the Application ID**

📍 Copy the **application ID** of your Sqoop import job from the Resource Manager.

Example:
`application_1745983395808_0001`

![Find Application ID](https://github.com/user-attachments/assets/e8faf031-4f5a-4cfb-9ba8-0144f05ba208)

---

## 📜 **Step 18: View Detailed Logs for Application**

Run the following command to fetch the complete logs of your import job:

```bash
yarn logs -applicationId application_1745983395808_0001
```

📋 This will display **all the logs** generated by the job.

![Application Logs](https://github.com/user-attachments/assets/a3e5ff01-6564-4e83-b574-f14992ae3921)

---

## 🔍 **Step 19: Filter Logs to See SQL Query Only**

If you are interested **only in the SQL query executed**, you can filter it using:

```bash
yarn logs -applicationId application_1745983395808_0001 | grep "query:"
```

🔎 This helps you focus on **SQL-related operations** without going through the full log.

![Filtered Query Log](https://github.com/user-attachments/assets/278b2691-80b6-413d-8b75-42d4d79fa7ae)

---

# 🎯 **Quick Revision Points**

| 📝                         | ✨                                        |
| -------------------------- | ---------------------------------------- |
| `hdfs dfs -ls salaries`    | Check imported files                     |
| No split-by?               | Sqoop uses **Primary Key** for splitting |
| Map tasks                  | **Run parallelly** for faster import     |
| `yarn logs -applicationId` | View full job logs                       |
| `grep "query:"`            | Fetch only executed SQL query from logs  |

---

# 📚 **Summary**

* **Data successfully imported** from MySQL ➡️ HDFS 🗂️
* **MapReduce job** handled splitting and importing in parallel 🔥
* We now have full control over **job monitoring** and **debugging** through YARN logs.

---

# 🧑‍💻 **Importing Specific Columns**

---

## 1️⃣ **Specify Columns to Import with Sqoop**

To import only **selected columns** from a table:

```bash
sqoop import --connect jdbc:mysql://quickstart.cloudera:3306/test \
--driver com.mysql.jdbc.Driver --username root --password cloudera \
--table salaries --columns salary,age -m 1 --target-dir salaries2
```

📝 Here’s what each part does:

* **`--columns salary,age`**: Specifies the columns to import (only `salary` and `age`).
* **`-m 1`**: Using **1 map task** for importing the data.
* **`--target-dir salaries2`**: Specifies the **HDFS destination** directory.

---

## ✅ **Check Imported Data in HDFS**

Verify if the data is stored correctly in HDFS:

```bash
hdfs dfs -ls
```

![HDFS Directory](https://github.com/user-attachments/assets/0fe99409-a8b0-43d4-9bf5-4315cb931869)

---

## 📝 **View Logs of MapReduce Job for salaries2**

Check logs using the **application ID**:

![Job Logs](https://github.com/user-attachments/assets/dbcd755f-b506-4ecc-b658-9c15ae544360)

---

# 📑 **Importing Data Using a SQL Query**

---

## 2️⃣ **Import Data Based on Query with Sqoop**

To filter and import data based on a **SQL query**:

```bash
sqoop import --connect jdbc:mysql://quickstart.cloudera:3306/test \
--driver com.mysql.jdbc.Driver --username root --password cloudera \
--query "select * from salaries s where s.salary > 90000.00 and \$CONDITIONS" \
--split-by gender -m 2 --target-dir salaries3
```

📝 Breakdown:

* **`--query`**: Provides the SQL query to filter the data.
* **`--split-by gender`**: Data will be split based on the **gender** column.
* **`-m 2`**: Specifies **2 map tasks**.

---

## ✅ **Check Imported Data in HDFS**

```bash
hdfs dfs -ls salaries3
```

![HDFS Query Import](https://github.com/user-attachments/assets/55eab0ef-625c-4dc8-976a-f0cef40631c1)

---

## 📝 **Logs for Query Import**

To view the logs of the import:

![Query Import Logs](https://github.com/user-attachments/assets/c694bb4d-cf9d-43f1-a7ea-b829bff3889a)

---

## ⚠️ **Error: Missing \$CONDITIONS**

If you try to run the **query without \$CONDITIONS**, you’ll get an error like:

![Missing \$CONDITIONS](https://github.com/user-attachments/assets/8f97b6a4-5b85-423a-91f7-48cb16f7f845)

---

## ⚠️ **Error: Missing Split Function**

If you run the import without the **split function**, you’ll see an error:

![Missing Split Function](https://github.com/user-attachments/assets/268efaed-4f35-49ec-9fb3-92347461f68d)

---

## 🚨 **Key Takeaway:**

* Both **\$CONDITIONS** and **`--split-by`** are **mandatory** for running a query-based import with Sqoop.

---

# 🤖 **Automating the Import with Shell Script**

To **automate** the process, use a **bash script** like this:

```bash
#!/bin/bash

$(hdfs dfs -test -e $1)

if [[ $? -eq 0 ]]; then
        hdfs dfs -rm -R salaries
fi

sqoop import --connect jdbc:mysql://talentum-virtual-machine:3306/test?useSSL=false \
--driver com.mysql.jdbc.Driver --username bigdata -password Bigdata@123 --table salaries
```

📝 What it does:

1. Checks if a directory (`$1`) exists in HDFS.
2. If exists, it **removes** the directory (`salaries`).
3. Imports the **`salaries`** table from MySQL to HDFS.

---

# 🚀 **DistCp**

---

## 🔍 **What is DistCp?**

* **DistCp** (Distributed Copy) is a tool to **copy large datasets** across clusters.
* It uses **MapReduce** to copy data in parallel, making the transfer faster and efficient.

---

## 📝 **DistCp Recommendations**

* By default, **DistCp** uses **20 mappers** for the copy process.
* This parallelism speeds up the data transfer significantly!

---

# 📚 **Summary of Key Concepts**

| 📝 **Command/Concept**        | ✨ **Explanation**                               |
| ----------------------------- | ----------------------------------------------- |
| **`sqoop import --columns`**  | Import only specified columns                   |
| **`--query`**                 | Import data based on a custom SQL query         |
| **`--split-by`**              | Split data across multiple mappers (tasks)      |
| **`DistCp`**                  | Efficiently copy large datasets across clusters |
| **`Automated Import Script`** | Automate data import with bash scripting        |

---
