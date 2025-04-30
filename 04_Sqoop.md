How is the below code working:

// Abstract class Animal
abstract class Animal {
    // Abstract method for making sound
    abstract void makeSound();
}

// Dog class extending Animal
class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Woof");
    }
}

// Cat class extending Animal
class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Meow");
    }
}

// Cow class extending Animal
class Cow extends Animal {
    @Override
    void makeSound() {
        System.out.println("Moo");
    }
}

// Main class
public class AnimalSound {
    public static void main(String[] args) {
        // Creating instances of different animals
        Animal dog = new Dog();
        Animal cat = new Cat();
        Animal cow = new Cow();

        // Calling makeSound method for each animal
        dog.makeSound(); // Output: Woof
        cat.makeSound(); // Output: Meow
        cow.makeSound(); // Output: Moo
    }
}

Animal dog = new Dog()

Super class reference points to sub class object.

---

## Sqoop:

Import RDBMS Data into Hadoop.

Our requirement is to process the data present in rdbms into hdfs.
Hadoop can only analyse the data if it is in hdfs.
Then how to pull that data from rdbms into hdfs?

1. Client executes a
sqoop command
2. Sqoop executes the
command as a MapReduce
job on the cluster (using
Map-only tasks)
3. Plugins provide connectivity to
various data sources

![image](https://github.com/user-attachments/assets/943fe696-4f41-40dd-aa19-964e7be220e2)

---

## The Sqoop Import Tool

The import command has the following requirements:
• Must specify a connect string using the --connect argument

• Credentials can be included in the connect string, so use the -
-username and --password arguments
Using JDBC give the credentials to authenticate if the user is a valid user

• Must specify either a table to import using --table (for complete import) or the
result of an SQL query using --query

---

## Importing a Table

sqoop import

--connect jdbc:mysql://host/nyse
Here, jdbc url, jdbc is a protocol, mysql is the connectivity, mysql is running on host, nyse is the database

--table StockPrices
StockPrices is the tablename

--target-dir /data/stockprice/
After importing the table, where do we want to exactly store this table.
so, target specifies the path of HDFS
The path here will be data
Here, absolute path is given

--as-textfile
In which format, the data should be stored, so here, we are specifying the format of the file as textfile

When this query is executed
This will launch a mapreduce job
it has by default 4 map tasks
This 4 tasks are run parallely
why parallely? because map reduce runs parallely

---

## Importing Specific Columns

I don't want data from whole column, I just want projection

sqoop import

--connect jdbc:mysql://host/nyse

--table StockPrices

--columns StockSymbol,Volume,
High,ClosingPrice
This is known as projection

--target-dir /data/dailyhighs/

--as-textfile

--split-by StockSymbol
This can be said equal distribution of load across the workers (map tasks).
Map Task is a Java Program whose task is to execute Map Reduce.
Here, Default column is primary key column if not specified.
Pulling the data by 10 tasks and that too equally so which column will help me to split the data equally,
so here comes the StockSymbol in this table.
Let's assume StockSymbol is a unique column. Remember, we are not saying it primary column.
Equal Distribution will be based on the formulation such as:
No. of rows in that column / No. of map tasks
There will be no overlapping
If there is no equal distribution, performance hit may occur.

-m 10
Specifies how many map tasks to be launched and then those tasks will start pulling out the data
Then why wasn't it included in the earlier query of Importing a Table section.
By default -m (map tasks) is 4

---

## Importing from a Query

sqoop import

--connect jdbc:mysql://host/nyse

--query "SELECT * FROM StockPrices s
split function is mandatory for --query to work

WHERE s.Volume >= 1000000

AND \$CONDITIONS"

--target-dir /data/highvolume/

--as-textfile

--split-by StockSymbol

---

Copy and paste salaries.txt from staging area into LABS_HOME
and counting the lines present in the salaries.txt

![image](https://github.com/user-attachments/assets/6378aba5-6161-45c5-9d93-9d7b1e681de1)

We are currently in Lab3.1
![image](https://github.com/user-attachments/assets/38fd515f-d743-403e-95e2-379a7475d2b9)


Copy the file in /tmp
![image](https://github.com/user-attachments/assets/eb511973-a879-4597-a9fa-e793e68a74d4)


Verify if the file is present or not
![image](https://github.com/user-attachments/assets/dd2098e7-c86e-4f3e-94e0-f342e6e10e7a)


Connecting database
![image](https://github.com/user-attachments/assets/f87e86f3-91aa-40dd-8818-180e6b1a7ee3)

Enter password:
Password is `cloudera`

You should see a mysql prompt

![image](https://github.com/user-attachments/assets/1bc137c6-b772-404a-8a46-82c077164613)

Now, we are creating a Database test;
CREATE DATABASE test;
![image](https://github.com/user-attachments/assets/cf8d2aa9-ea11-4773-a034-4f6b47818673)

The table has been created successfully..!!

Now, we are looking for the databases present in mysql:
SHOW DATABASES;
![image](https://github.com/user-attachments/assets/6a86aa99-9095-4f7d-b5ff-0fae5073929b)

Now, switch to test database:
USE test;
![image](https://github.com/user-attachments/assets/c7238cd0-e422-4003-b155-8badcbf65808)

Now creating a table:

CREATE TABLE salaries (
gender varchar(1),
age int,
salary double,
zipcode int);

![image](https://github.com/user-attachments/assets/d2491f82-e154-4b8c-9aac-b00903e0ea9e)

Showing Tables present in the database:
show tables;

![image](https://github.com/user-attachments/assets/a71f47ce-44fa-4509-85c1-e45bebeb2d70)

Describing Table:
desc salaries
![image](https://github.com/user-attachments/assets/65ddef56-5ee1-4942-9e84-124082e02170)

load data local infile '/tmp/salaries.txt' into table salaries fields terminated by ',';

![image](https://github.com/user-attachments/assets/18948897-6790-4e4d-9573-9e1d438ad89b)

Verify:
select count(*) from salaries;
![image](https://github.com/user-attachments/assets/c046383c-398e-4f48-9153-9f7f3ef9eb83)

ALTER TABLE:
alter table salaries add column `id` int(10) unsigned primary KEY AUTO_INCREMENT;

![image](https://github.com/user-attachments/assets/b9593375-976f-4ed3-8233-b1e369af15b0)

DESCRIBE TABLE now:
![image](https://github.com/user-attachments/assets/e3835905-2204-4e60-93bf-3d8f958f5a6a)

Display Table:
select * from salaries;
![image](https://github.com/user-attachments/assets/377384a6-2b1f-4a43-82ac-49b1d5ea129a)

---

At this point of time our DB is ready to import into hadoop cluster

1) Import the Table into HDFS
sqoop import --connect jdbc:mysql://quickstart.cloudera:3306/test --driver com.mysql.jdbc.Driver --username root -password cloudera --table salaries

![image](https://github.com/user-attachments/assets/f84b567f-36ac-456c-b2d4-4c6e4c215809)
![image](https://github.com/user-attachments/assets/91073306-8e84-4328-95dd-0e77124b093c)

This is output of mapreduce program

localhost:19888 on cloudera website
![image](https://github.com/user-attachments/assets/d22209da-2f7c-4794-b800-bd724646955f)

http port 8088 is of resource manager
yarn calls it application 19888
mapreduce calls it job 8088

Verify if salaries folder has been added in hdfs:

hdfs dfs -ls

hdfs dfs -ls salaries

![image](https://github.com/user-attachments/assets/48ceb853-bd81-4e71-9261-0439990f65f7)

Size of data in each map tasks:
0, 272, 241, 238, 272 (bytes)
Almost equally distributed
We hadn't specified split column, then it selected which column for split?

All these map tasks are executed parallely and not sequentially (i.e., starts after the earlier process execution ends).

Mapreduce job through 

![image](https://github.com/user-attachments/assets/2f04843e-c795-4cda-83ef-360c1368e859)

Take application_Id from localhost:8088
![image](https://github.com/user-attachments/assets/e8faf031-4f5a-4cfb-9ba8-0144f05ba208)


yarn logs -applicationId application_1745983395808_0001
![image](https://github.com/user-attachments/assets/a3e5ff01-6564-4e83-b574-f14992ae3921)

yarn logs -applicationId application_1745983395808_0001 | grep "query:"
To show only the query part from the logs
![image](https://github.com/user-attachments/assets/278b2691-80b6-413d-8b75-42d4d79fa7ae)

---

2) Specify Columns to Import
sqoop import --connect jdbc:mysql://quickstart.cloudera:3306/test --driver com.mysql.jdbc.Driver --username root -password cloudera --table salaries --columns salary,age -m 1 --target-dir salaries2

Also checking:

hdfs dfs -ls

![image](https://github.com/user-attachments/assets/0fe99409-a8b0-43d4-9bf5-4315cb931869)

Now, checking logs with applicationId for salaries2

![image](https://github.com/user-attachments/assets/dbcd755f-b506-4ecc-b658-9c15ae544360)


3) Importing from a Query
sqoop import --connect jdbc:mysql://quickstart.cloudera:3306/test --driver com.mysql.jdbc.Driver --username root --password cloudera --query "select * from salaries s where s.salary > 90000.00 and \$CONDITIONS" --split-by gender -m 2 --target-dir salaries3

![image](https://github.com/user-attachments/assets/60a7bc28-403a-4396-904d-b54959a40070)

Checking hdfs dfs -ls salaries3

![image](https://github.com/user-attachments/assets/55eab0ef-625c-4dc8-976a-f0cef40631c1)

applicaton id for salaries3
![image](https://github.com/user-attachments/assets/c694bb4d-cf9d-43f1-a7ea-b829bff3889a)

removing condition, we get error:
![image](https://github.com/user-attachments/assets/8f97b6a4-5b85-423a-91f7-48cb16f7f845)

removing split function
we get error
![image](https://github.com/user-attachments/assets/268efaed-4f35-49ec-9fb3-92347461f68d)

So, the takeaway is that both \$CONDITIONS and --split-by is important for a query to run.

Now, automate.sh:

#!/bin/bash

$(hdfs dfs -test -e $1)

if [[ $? -eq 0 ]]; then
        hdfs dfs -rm -R salaries
fi

sqoop import --connect jdbc:mysql://talentum-virtual-machine:3306/test?useSSL=false --driver com.mysql.jdbc.Driver --username bigdata -password Bigdata@123 --table salaries

---

## DistCp

## DistCp Recommendations

Default 20 mappers.





















