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
