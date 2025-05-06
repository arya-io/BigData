# 🐷 Introduction to Pig

## 📌 Topics Covered
- About Pig
- Pig Latin
- The Grunt Shell
- Demo: Understanding Pig
- Pig Latin Relation Names and Field Names
- Pig Data Types
- Defining a Schema
- Lab: Getting Started with Pig
- The GROUP Operator
- Lab: Exploring Data with Pig

---

## 🏗️ About Pig
Pig is a **data-processing engine** designed to work on **top of Hadoop**. It helps process **large datasets** efficiently using a special scripting language called **Pig Latin**.

### 🔹 Why Use Pig?
- It simplifies the process of writing complex **Hadoop jobs**.
- You **don’t need** to write Java-based MapReduce programs manually.
- It provides **intuitive commands** for managing data.

💡 **Example:**
Think of Pig as a **chef** who takes raw ingredients (data) and prepares a well-cooked dish (processed output). Hadoop is the **kitchen**, and Pig uses its own recipe book (**Pig Latin**) to cook the data!

---

## 💬 Pig Latin: The Language of Pig
Pig Latin is a **high-level scripting language** used to process data in **Hadoop**.

### 🛠️ How Pig Executes Commands:
1️⃣ Each command is **processed** by the **Pig interpreter**.
2️⃣ If the command is valid, Pig adds it to a **logical plan**.
3️⃣ The commands **don’t run immediately**—execution happens only when you use:
   - `DUMP` (to display results)
   - `STORE` (to save results)

💡 **Example:**
Imagine Pig as a **shopping list manager**. You add items to the shopping list (logical plan), but you **don’t actually buy** anything until you go to the store (`STORE`) or check what’s in the cart (`DUMP`).

---

## 🔍 The Grunt Shell: Pig's Playground
The **Grunt Shell** is a **command-line interface** where you can type and execute **Pig Latin statements**.

### 🏗️ How to Start Grunt Shell:
Run the following command in your terminal to enter the interactive mode:

```bash
pig
```

Once inside the Grunt Shell, you can begin writing Pig scripts.

💡 **Example:**
Think of the Grunt Shell as a **chat window** where you **type instructions**, and Pig listens and executes them.

---

# 🐷 Pig Latin Essentials

## 🔹 Pig Latin Relation Names
A **relation** in Pig is the **result of a processing step**, similar to a **table** in databases.

### 🏷️ Alias: Naming Your Relations
- Every relation has a **name**, called an **alias**.
- This alias is used to **refer to the relation** in further steps.

💡 **Example:**
```pig
stocks = LOAD 'mydata.txt' USING TextLoader();
```
Here, `stocks` is the **alias**, meaning that any future operations on `stocks` will be applied to the **data loaded from `mydata.txt`**.

Think of it like naming a **saved search**—instead of typing the entire path again, you can simply refer to **"stocks"**.

---

## 🏷️ Pig Latin Field Names
- **Fields** are **individual attributes** within a relation.
- You can **name** fields explicitly when loading data, making queries easier.

💡 **Example:**
```pig
salaries = LOAD 'salary.data' USING PigStorage(',')
AS (gender, age, income, zip);
highsalaries = FILTER salaries BY income > 1000000;
```
In the above example:
- `gender`, `age`, `income`, and `zip` are **field names** for the `salaries` relation.
- The `FILTER` command selects **high earners** where `income > 1000000`.

🚀 **Analogy:** Field names are like **column headers** in a spreadsheet—they help identify data better!

---

## 🏗️ Pig Data Types
Pig supports different **data types**, just like traditional programming languages.

### 🔹 Primitive Data Types:
| Data Type  | Description |
|------------|------------|
| `int`      | Whole number (e.g., `25`) |
| `long`     | Large whole number |
| `float`    | Decimal number (e.g., `3.14`) |
| `double`   | Large decimal number |
| `chararray`| String of characters (e.g., `"Hello"`) |
| `bytearray`| Binary data representation |
| `boolean`  | True/False values |
| `datetime` | Date and time representation |
| `bigdecimal` | High-precision decimal values |
| `biginteger` | High-precision integer values |

💡 **Example:**
```pig
data = LOAD 'example.txt' AS (id:int, name:chararray, salary:double);
```
Here, `id` is an **integer**, `name` is a **string**, and `salary` is a **decimal number**.

---

## 🏗️ Pig Complex Types
Pig also supports **complex data structures**, useful for handling nested and grouped data.

### 🌀 Tuple: Ordered Set of Values
A **tuple** is like a **single row** in a table.

💡 **Example:**
```pig
(OH, Mark, Twain, 31225)
```
Each value **follows an order**: **state, name, surname, zip code**.

---

### 📦 Bag: Unordered Collection of Tuples
A **bag** contains **multiple tuples**, similar to a **table** with multiple rows.

💡 **Example:**
```pig
{
(OH, Mark, Twain, 31225),
(UK, Charles, Dickens, 42207),
(ME, Robert, Frost, 11496)
}
```
Think of a **bag** as a **list of entries** grouped together!

---

### 🔑 Map: Key/Value Pair Collection
A **map** is like a **dictionary**—each **key** is associated with a **value**.

💡 **Example:**
```pig
[state#OH, name#Mark Twain, zip#31225]
```
Here:
- `state` is the **key**, and `OH` is its **value**.
- `name` is the **key**, and `Mark Twain` is its **value**.

🚀 **Analogy:** Maps are like **address books**—you look up a name and get their contact details.

---

## 🏗️ Defining a Schema in Pig
Schemas allow you to **define the structure of the data explicitly**.

### 📌 Example 1: Simple Schema
```pig
customers = LOAD 'customer_data' AS (
firstname: chararray,
lastname: chararray,
house_number: int,
street: chararray,
phone: long,
payment: double);
```
This defines the **data structure** for the `customers` relation.

---

### 📌 Example 2: Complex Schema with Bags
```pig
salaries = LOAD 'salaries.txt' AS (
gender: chararray,
details: bag {
(age: int, salary: double, zip: long)
});
```
Here:
- `gender` is a **simple field**.
- `details` is a **bag** containing multiple nested values like `age`, `salary`, and `zip`.

🚀 **Why Schema?**
Schemas make Pig processing **faster and clearer**, allowing structured operations on data.

---

### 📊 The GROUP Operator in Apache Pig

![image](https://github.com/user-attachments/assets/97abce11-3f37-4361-84f9-e7fe01796130)

The **GROUP** operator in **Apache Pig** is used to group records together based on a specific column. It helps organize data so you can perform operations on groups of records instead of individual ones.

#### 🏗 How GROUP Works

Imagine a table named **salaries**, where each row represents a person’s details:

| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| F      | 17  | 41000.00 | 95103   |
| M      | 19  | 76000.00 | 95102   |
| F      | 22  | 95000.00 | 95103   |
| F      | 19  | 60000.00 | 95105   |
| M      | 19  | 14000.00 | 95102   |
| M      | 17  | 35000.00 | 95103   |

Now, if we apply the **GROUP** operator on the **age** column, it will create groups where all people with the same age are clustered together.

#### ✨ Example Transformation

We apply:
```plaintext
salariesbyage = GROUP salaries BY age;
```

Now, the transformed table **salariesbyage** groups all people by age:

| Age (Group) | Salaries |
|------------|---------|
| 17         | { (F,17,41000.0,95103), (M,17,35000.0,95103) } |
| 19         | { (M,19,76000.0,95102), (F,19,60000.0,95105), (M,19,14000.0,95102) } |
| 22         | { (F,22,95000.0,95103) } |

#### 📌 Understanding the Output

- The **group** column represents the value we grouped by (age).
- The **salaries** column holds all rows with the same age, inside **curly brackets `{}`**.

#### 🔍 Checking the Data Structure

You can describe the new grouped data:
```plaintext
grunt> DESCRIBE salariesbyage;
salariesbyage: {group:int, salaries: {(gender: chararray, age: int, salary: double, zip: int)}}
```

---

🛠 **Why is GROUP Useful?**  
Grouping data allows us to apply aggregate functions, such as:
- Finding the **average salary** per age group.
- Counting the **number of employees** in each age group.
- Filtering groups that meet specific criteria.

💡 **Think of GROUP Like Sorting Books in a Library**  
If you walk into a library and find books scattered everywhere, it’s hard to locate a specific one. But if you **group books by genre**, suddenly everything is more organized! That’s exactly what the GROUP operator does—it arranges data logically.

---

### 🌍 GROUP ALL in Apache Pig

![image](https://github.com/user-attachments/assets/a2f73645-d00b-4efe-84f9-f5e7abbdf9a5)

The **GROUP ALL** operator in **Apache Pig** is used when we want to group all records of a dataset into a single collection. Unlike **GROUP BY**, which groups based on column values, **GROUP ALL** creates just one big group.

#### 🏗 How GROUP ALL Works

Imagine you have the same **salaries** table:

| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| F      | 17  | 41000.00 | 95103   |
| M      | 19  | 76000.00 | 95102   |
| F      | 22  | 95000.00 | 95103   |
| F      | 19  | 60000.00 | 95105   |
| M      | 19  | 14000.00 | 95102   |
| M      | 17  | 35000.00 | 95103   |

Now, using **GROUP ALL**, we group everything into one collection.

#### ✨ Example Transformation

We apply:
```plaintext
allsalaries = GROUP salaries ALL;
```

Now, the transformed table **allsalaries** looks like:

| Group | Salaries |
|------|---------|
| all  | { (F,17,41000.0,95103), (M,19,76000.0,95102), (F,22,95000.0,95103), (F,19,60000.0,95105), (M,19,14000.0,95102), (M,17,35000.0,95103) } |

#### 📌 Understanding the Output

- The **group** column is simply labeled `"all"`, meaning everything belongs to the same group.
- The **salaries** column holds all rows inside **curly brackets `{}`**, essentially treating the whole dataset as one unit.

#### 🔍 Checking the Data Structure

You can describe the new grouped data:
```plaintext
grunt> DESCRIBE allsalaries;
allsalaries: {group: chararray, salaries: {(gender: chararray, age: int, salary: double, zip: int)}}
```

---

🛠 **Why is GROUP ALL Useful?**  
Grouping everything into a single collection can be helpful when:
- Performing **aggregate calculations** on an entire dataset, such as computing the **total salary of all employees**.
- **Applying functions** that require the entire dataset to be processed as one entity.
- **Counting the number of rows** in a dataset.

💡 **Think of GROUP ALL Like a Shopping Cart**  
Imagine buying items from different sections in a store. Normally, they’re organized in different categories (fruits, electronics, books, etc.). But when you **add everything to the shopping cart**, all items belong to a single group. That’s exactly what GROUP ALL does—it puts all records into one logical container for processing.

---

### 🔗 Relations Without a Schema in Apache Pig

![image](https://github.com/user-attachments/assets/b7e731a9-4f8e-4b43-99a4-aa032f012820)

In **Apache Pig**, data relations can exist **without a predefined schema**. This means the dataset doesn't need explicit column names, allowing for **flexible processing** when the structure of the data isn't strictly defined.

#### 🏗 How Does This Work?

Consider a dataset named **salaries**, structured like this:

| Column Index ($) | Data Type  | Example Values      |
|----------------|------------|-------------------|
| **$0**        | Gender      | F, M             |
| **$1**        | Age         | 17, 19, 22       |
| **$2**        | Salary      | 41000, 76000, 95000 |
| **$3**        | Zip Code    | 95103, 95102, 95105 |

Because this relation has **no explicit schema**, columns are referenced using **positional notation** (like `$0`, `$1`, `$2`, `$3`), instead of named attributes.

---

### ✨ Grouping Without a Schema

If we want to group **salaries** by Zip Code (`$3`), we use:

```plaintext
salariesgroup = GROUP salaries BY $3;
```

This **groups** all employees with the same Zip Code into logical collections.

| Group (Zip Code) | Salaries |
|----------------|---------|
| 95103         | { (F,17,41000,95103), (M,17,35000,95103), (F,22,95000,95103) } |
| 95102         | { (M,19,76000,95102), (M,19,14000,95102) } |
| 95105         | { (F,19,60000,95105) } |

---

### 📌 Understanding the Grouped Structure

To inspect the transformed relation, we run:
```plaintext
grunt> DESCRIBE salariesgroup;
```

Output:
```plaintext
salariesgroup: {group:bytearray, salaries:{()}}
```
- The **group** column contains the grouped value (`Zip Code`).
- The **salaries** column holds **nested tuples**, grouping multiple records together.

---

🛠 **Why Use Schema-Free Relations?**
- **Flexible** processing when exact attribute names are unknown.
- Supports **semi-structured** and **unstructured** data.
- Easily references columns using **position-based notation** (`$0`, `$1`, etc.).
- Useful for **quick transformations and aggregations**.

💡 **Think of Schema-Free Relations Like a Grab Bag**
Imagine you have an assorted bag of items, but instead of labeling each item explicitly, you reference them by **position**—like "the first item" or "the second item." Apache Pig follows the same idea in schema-less relations!

---

### 🔄 FOREACH…GENERATE in Apache Pig

![image](https://github.com/user-attachments/assets/1aab7e1e-a26e-4865-8c16-00524cd1ad30)

The **FOREACH** operator in **Apache Pig** is used to **process each tuple** in a dataset and extract or modify specific fields. It works alongside **GENERATE**, which defines what fields should be retrieved or transformed.

#### 🏗 How FOREACH…GENERATE Works

Consider the dataset **salaries**:

| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| F      | 17  | 41000.00 | 95103   |
| M      | 19  | 76000.00 | 95102   |
| F      | 22  | 95000.00 | 95103   |
| F      | 19  | 60000.00 | 95105   |
| M      | 19  | 14000.00 | 95102   |
| M      | 17  | 35000.00 | 95103   |

---

### ✨ Extracting Specific Fields

Let’s say we only want **Age and Salary**, ignoring the rest. We use:

```plaintext
short_salaries = FOREACH salaries GENERATE age, salary;
```

Now, the output will contain only the selected columns:

| Age | Salary  |
|-----|---------|
| 17  | 41000.00 |
| 19  | 76000.00 |
| 22  | 95000.00 |
| 19  | 60000.00 |
| 19  | 14000.00 |
| 17  | 35000.00 |

---

### 🔄 Applying Transformations

We can also apply **functions** within FOREACH…GENERATE. For instance, if we want to increase every salary by **10%**, we use:

```plaintext
updated_salaries = FOREACH salaries GENERATE age, salary * 1.1;
```

Now, the salaries are **adjusted**:

| Age | New Salary  |
|-----|------------|
| 17  | 45100.00   |
| 19  | 83600.00   |
| 22  | 104500.00  |
| 19  | 66000.00   |
| 19  | 15400.00   |
| 17  | 38500.00   |

---

### 📌 Checking the Structure

To inspect the new data format:
```plaintext
grunt> DESCRIBE updated_salaries;
updated_salaries: {(age:int, salary:double)}
```
Since we only extracted **age and modified salary**, other fields are no longer present.

---

🛠 **Why is FOREACH…GENERATE Useful?**
- Extracts **specific columns** from a dataset.
- Allows **modifications**, including **mathematical operations**.
- Simplifies data for further processing.

💡 **Think of FOREACH Like Filtering a Playlist**
Imagine you have a full music library, but you want to create a playlist containing only **rock songs**. **FOREACH…GENERATE** helps extract only the needed parts from a large collection, making it more focused.

---

### 📊 Specifying Ranges in FOREACH (Apache Pig)

The **FOREACH…GENERATE** statement in **Apache Pig** allows us to select specific columns from a dataset using **range notation**. This provides a convenient way to extract multiple columns **without listing each one manually**.

---

### 🏗 How Ranges Work in FOREACH

Imagine we have a dataset **salaries.txt**, structured as:

| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| F      | 17  | 41000.00 | 95103   |
| M      | 19  | 76000.00 | 95102   |
| F      | 22  | 95000.00 | 95103   |
| F      | 19  | 60000.00 | 95105   |
| M      | 19  | 14000.00 | 95102   |
| M      | 17  | 35000.00 | 95103   |

Now, we **load the data**:
```plaintext
salaries = LOAD 'salaries.txt' USING PigStorage(',') AS (gender:chararray, age:int, salary:double, zip:int);
```

---

### ✨ Using Range-Based Selection

Apache Pig provides **three ways** to select column ranges:

| Expression            | Meaning |
|----------------------|------------------------------------------------|
| `age..zip`          | Selects all columns **between age and zip**. |
| `age..`             | Selects **age and all following columns**. |
| `..salary`          | Selects **salary and all preceding columns**. |

#### 🚀 Example Queries

```plaintext
C = FOREACH salaries GENERATE age..zip;
D = FOREACH salaries GENERATE age..;
E = FOREACH salaries GENERATE ..salary;
```

---

### 📌 Another Example with Positional Indexing

For datasets **without a schema**, you can use **positional notation** (`$index`):

```plaintext
customer = LOAD 'data/customers';
F = FOREACH customer GENERATE $12..$23;
```

Here, **Pig extracts all columns from position `$12` to `$23`**, assuming the dataset has more than 23 columns.

---

🛠 **Why Use Ranges in FOREACH?**
- Reduces **manual column selection** effort.
- Speeds up **query writing** for large datasets.
- Supports both **schema-based and index-based selection**.

💡 **Think of FOREACH Ranges Like Choosing Pages in a Book**
If you want to **read a section from pages 50 to 100**, you don’t list every page—you just specify the range. Apache Pig follows the same logic!

---

### 🏷️ Field Names in FOREACH (Apache Pig)

In **Apache Pig**, the **FOREACH…GENERATE** operator can reference fields using their **names** (when a schema is defined) or **positional notation** (when no schema exists). Understanding both methods helps ensure flexibility when processing data.

---

### 🏗 Using Named Fields

Consider a dataset **salaries.txt**, structured as:

| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| F      | 17  | 41000.00 | 95103   |
| M      | 19  | 76000.00 | 95102   |
| F      | 22  | 95000.00 | 95103   |
| F      | 19  | 60000.00 | 95105   |
| M      | 19  | 14000.00 | 95102   |
| M      | 17  | 35000.00 | 95103   |

To load the data while **assigning field names**, we use:

```plaintext
salaries = LOAD 'salaries.txt' USING PigStorage(',') AS (gender:chararray, age:int, salary:double, zip:int);
```

Now, we can select specific fields using their **names**:

```plaintext
C = FOREACH salaries GENERATE age, salary;
```

**Output:**
| Age | Salary  |
|-----|---------|
| 17  | 41000.00 |
| 19  | 76000.00 |
| 22  | 95000.00 |
| 19  | 60000.00 |
| 19  | 14000.00 |
| 17  | 35000.00 |

---

### ✨ Using Positional Notation

If the dataset is **loaded without a schema**, field names won’t exist. Instead, fields are referenced by their **position index**:

| Column Index ($) | Data Type  | Example Values |
|----------------|------------|---------------|
| **$0**        | Gender      | F, M         |
| **$1**        | Age         | 17, 19, 22   |
| **$2**        | Salary      | 41000, 76000, 95000 |
| **$3**        | Zip Code    | 95103, 95102, 95105 |

In this case, we extract **age and salary** using:

```plaintext
D = FOREACH salaries GENERATE $1, $2;
```

**Output remains the same**, but fields are accessed via **positional notation**.

---

### 🔍 Checking the Structure

To inspect the schema:
```plaintext
grunt> DESCRIBE salaries;
```
**Schema-Based Output:**  
```plaintext
salaries: {gender:chararray, age:int, salary:double, zip:int}
```

**Schema-Free Output:**  
```plaintext
salaries: {(bytearray)}
```
- **With Schema:** Fields are named.
- **Without Schema:** Fields are treated as generic bytearrays.

---

🛠 **Why Use Field Names in FOREACH?**
- **Improves readability** of queries.
- Makes processing **intuitive** when dealing with structured data.
- Provides **flexibility** when switching between named attributes and index-based notation.

💡 **Think of Field Names Like Labels on a Filing Cabinet**
If you have folders labeled **"Invoices," "Contracts," and "Reports,"** it’s easy to find what you need. Using **field names** in Pig works the same way—it helps organize data logically!

---

### 🔄 FOREACH with GROUPS in Apache Pig

![image](https://github.com/user-attachments/assets/9ffc82eb-a51d-4ab7-b519-dc921ba0272a)

In **Apache Pig**, when we use the **GROUP** operator, the resulting dataset contains nested tuples (bags). To process these groups, we use the **FOREACH** statement to extract or manipulate records inside each group.

---

### 🏗 How It Works

Consider a dataset **salaries.txt**, structured as:

| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| F      | 17  | 41000.00 | 95103   |
| M      | 19  | 76000.00 | 95102   |
| F      | 22  | 95000.00 | 95103   |
| F      | 19  | 60000.00 | 95105   |
| M      | 19  | 14000.00 | 95102   |
| M      | 17  | 35000.00 | 95103   |

Now, let's **group salaries by age**:
```plaintext
salariesgroup = GROUP salaries BY age;
```

This creates **nested groups**, where all employees of the same age are collected together.

---

### ✨ Applying FOREACH on Groups

Now, let’s process these **groups** using FOREACH:

```plaintext
summarized = FOREACH salariesgroup GENERATE group AS age, COUNT(salaries) AS num_people;
```

🔍 **What happens here?**
- **group AS age** → Extracts the grouped value (**age**).
- **COUNT(salaries)** → Counts the number of people in each age group.

**Output:**
| Age | Number of People |
|----|----------------|
| 17  | 2             |
| 19  | 3             |
| 22  | 1             |

---

### 📌 Extracting Specific Fields from Groups

Sometimes, we need to extract fields inside grouped records. We can do this like:

```plaintext
extracted = FOREACH salariesgroup GENERATE group AS age, FLATTEN(salaries);
```

This removes **nested brackets `{}`**, making records **flat and readable**.

---

### 🛠 Why Use FOREACH with GROUPS?
- Helps **summarize grouped data** (like counting, averaging).
- Extracts individual records from **nested bags**.
- Improves readability of grouped results.

💡 **Think of FOREACH with GROUPS Like Sorting Students by Grade**  
If we group students based on their grade level, we can then **process each group** to analyze performance or attendance. Apache Pig follows the same logic!

---

### 🔍 The FILTER Operator in Apache Pig

![image](https://github.com/user-attachments/assets/463a1e1b-ff50-42c9-9931-b20a8224498c)

The **FILTER** operator in **Apache Pig** is used to remove unwanted records from a dataset based on specific conditions. It acts like a sieve, letting only records that meet the criteria pass through.

---

### 🏗 How FILTER Works

Imagine you have the dataset **salaries.txt**, structured as:

| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| F      | 17  | 41000.00 | 95103   |
| M      | 19  | 76000.00 | 95102   |
| F      | 22  | 95000.00 | 95103   |
| F      | 19  | 60000.00 | 95105   |
| M      | 19  | 14000.00 | 95102   |
| M      | 17  | 35000.00 | 95103   |

Now, let's **load the data**:
```plaintext
salaries = LOAD 'salaries.txt' USING PigStorage(',') AS (gender:chararray, age:int, salary:double, zip:int);
```

---

### ✨ Applying Filters

Let’s say we **only want records where the salary is above ₹50,000**:
```plaintext
high_salary = FILTER salaries BY salary > 50000;
```

🔍 **Output:**
| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| M      | 19  | 76000.00 | 95102   |
| F      | 22  | 95000.00 | 95103   |
| F      | 19  | 60000.00 | 95105   |

💡 **Notice:** Only records **where salary is greater than ₹50,000** remain.

---

### 🔄 Filtering Based on Multiple Conditions

We can **combine multiple conditions**:
```plaintext
filtered_salaries = FILTER salaries BY age > 18 AND salary > 50000;
```
🔍 **What does this do?**
- Keeps records **only where age is above 18** AND **salary exceeds ₹50,000**.

---

### 🎭 Filtering Using String Comparisons

We can **filter based on text values** too!

```plaintext
females = FILTER salaries BY gender == 'F';
```
🔍 **Output:**  
| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| F      | 17  | 41000.00 | 95103   |
| F      | 22  | 95000.00 | 95103   |
| F      | 19  | 60000.00 | 95105   |

---

### 📌 Checking the Structure

To verify the filtered dataset:
```plaintext
grunt> DESCRIBE high_salary;
```
Output:
```plaintext
high_salary: {gender: chararray, age: int, salary: double, zip: int}
```
The **schema remains unchanged**, but **unwanted records are removed**.

---

🛠 **Why Use FILTER?**
- Helps **clean data** by removing irrelevant records.
- Makes queries **more precise**.
- Enables filtering based on **numeric, string, or conditional logic**.

💡 **Think of FILTER Like a Coffee Filter!**
Just like a coffee filter separates the **ground beans from the liquid**, the FILTER operator separates **irrelevant data from useful insights**.

---

### 📏 The LIMIT Operator in Apache Pig

![image](https://github.com/user-attachments/assets/a5541eed-1706-4dd3-ab19-b50908e3e9f1)

The **LIMIT** operator in **Apache Pig** is used to **restrict the number of rows** returned in the output. It helps manage large datasets by extracting only a **specific number of records** for quick analysis.

---

### 🏗 How LIMIT Works

Imagine we have the dataset **salaries.txt**, structured as:

| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| F      | 17  | 41000.00 | 95103   |
| M      | 19  | 76000.00 | 95102   |
| F      | 22  | 95000.00 | 95103   |
| F      | 19  | 60000.00 | 95105   |
| M      | 19  | 14000.00 | 95102   |
| M      | 17  | 35000.00 | 95103   |

Now, let’s **load the data**:
```plaintext
salaries = LOAD 'salaries.txt' USING PigStorage(',') AS (gender:chararray, age:int, salary:double, zip:int);
```

---

### ✨ Using LIMIT

If we want to **extract only the first 3 records**, we use:

```plaintext
limited_salaries = LIMIT salaries 3;
```

🔍 **Output:**  
| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| F      | 17  | 41000.00 | 95103   |
| M      | 19  | 76000.00 | 95102   |
| F      | 22  | 95000.00 | 95103   |

💡 **Notice:** Only **three** rows appear, regardless of dataset size.

---

### 🔄 LIMIT with Sorting

LIMIT is often used **alongside ORDER BY** to retrieve top results. For example:

```plaintext
top_salaries = ORDER salaries BY salary DESC;
highest_paid = LIMIT top_salaries 2;
```

🔍 **Output:**
| Gender | Age | Salary  | Zip Code |
|--------|-----|---------|---------|
| F      | 22  | 95000.00 | 95103   |
| M      | 19  | 76000.00 | 95102   |

💡 **What happens here?**
- **ORDER BY salary DESC** → Sorts salaries in descending order.
- **LIMIT 2** → Extracts **only the top two records**.

---

### 📌 Checking the Structure

To verify the **LIMITED dataset**:
```plaintext
grunt> DESCRIBE limited_salaries;
```
Output:
```plaintext
limited_salaries: {gender: chararray, age: int, salary: double, zip: int}
```
Since **LIMIT only affects row count**, the **schema remains unchanged**.

---

🛠 **Why Use LIMIT?**
- Helps **sample data** from large datasets.
- Speeds up **testing and debugging**.
- Works well **with sorting** for top-N analysis.

💡 **Think of LIMIT Like Cutting a Cake!**  
If you have a **whole cake**, but only want to serve **three slices**, you cut out just what you need—LIMIT does the same for datasets!

---

### 📚 Review Questions on Apache Pig

### 1️⃣ **List two Pig commands that cause a logical plan to execute.**  

✅ **Answer:**  
Pig executes the logical plan when certain commands are run, including:  
- `DUMP` → Displays the output of a relation directly in the terminal.  
- `STORE` → Saves the output of a relation into a folder in **HDFS** for further use.  

---

### 2️⃣ **Which Pig command stores the output of a relation into a folder in HDFS?**  

✅ **Answer:**  
The `STORE` command is used to write data into **HDFS**.  

Example:
```plaintext
STORE salaries INTO 'hdfs://user/output' USING PigStorage(',');
```
This saves the **salaries** relation into the specified HDFS path.

---

### 📊 Sample Data  

Consider the following dataset:
```plaintext
XFR,2004-05-13,22.90,400
XFR,2004-05-12,22.60,400000
XFR,2004-05-11,22.80,2600
XFR,2004-05-10,23.00,3800
XFR,2004-05-07,23.55,2900
XFR,2004-05-06,24.00,2200
```
Now, let's load this data into Pig:
```plaintext
prices = LOAD 'prices.csv' USING PigStorage(',') 
AS (symbol:chararray, date:chararray, price:double, volume:int);
```

---

### 3️⃣ **What does the following command do?**  

```plaintext
DESCRIBE prices;
```
✅ **Explanation:**  
This command **displays the schema** of the relation **prices**, showing data types for each field.

Example Output:
```plaintext
prices: {symbol: chararray, date: chararray, price: double, volume: int}
```
This confirms that the dataset contains **four fields** with their respective types.

---

### 4️⃣ **What does the following command do?**  

```plaintext
A = GROUP prices BY symbol;
```
✅ **Explanation:**  
This **groups all records** in the dataset by the **symbol (stock identifier)**, forming nested bags.

Example Output:
```plaintext
XFR → { (2004-05-13,22.90,400), (2004-05-12,22.60,400000), ... }
```
Now, all records related to **XFR** are stored inside **one group**.

---

### 5️⃣ **What does the following command do?**  

```plaintext
B = FOREACH prices GENERATE symbol AS x, volume AS y;
```
✅ **Explanation:**  
This **renames and extracts** two fields:  
- **symbol → x**  
- **volume → y**  

Example Output:
```plaintext
(x: chararray, y: int)
XFR, 400
XFR, 400000
XFR, 2600
XFR, 3800
```
Only the **symbol and volume** fields remain.

---

### 6️⃣ **What does the following command do?**  

```plaintext
C = FOREACH A GENERATE group, SUM(prices.volume);
```
✅ **Explanation:**  
This computes **the total volume traded** for each **stock symbol**.

Example Output:
```plaintext
XFR, 409000
```
Now we know the **total traded volume** for each stock.

---

### 7️⃣ **What does the following command do?**  

```plaintext
D = FOREACH prices GENERATE symbol..price;
```
✅ **Explanation:**  
This extracts a **range** of fields from `symbol` to `price`.  

Example Output:
```plaintext
XFR, 2004-05-13, 22.90
XFR, 2004-05-12, 22.60
XFR, 2004-05-11, 22.80
```
Only the **symbol, date, and price** fields are included.

---

### 🚀 Key Takeaways  

- `DESCRIBE` helps inspect the schema.  
- `GROUP` clusters records into logical collections.  
- `FOREACH…GENERATE` helps **extract** and **modify** specific fields.  
- `SUM()` is useful for **aggregating numerical data**.  
- **Range selection (`symbol..price`)** simplifies field extraction.

---

💡 **Think of Apache Pig Like a Spreadsheet Tool!**  
Grouping data in Pig is **similar to pivot tables**, and filtering records works just like **Excel formulas**. You apply **commands to structure and refine** your dataset dynamically!

---




