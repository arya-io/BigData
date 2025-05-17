Why airflow, why you need it?
Let me show you this.
Let's imagine that you have the following data pipeline with three
tasks extract, load and transform, and it runs every day at 10:00 PM.
Very simple.

![image](https://github.com/user-attachments/assets/9c94cc48-f4c5-4c78-88e2-a770c0a4a7b2)

Obviously at every step you are going to interact with an external
tool or an external system, for example, an API for extract.
Snowflake for load, and DBT for transform.

![image](https://github.com/user-attachments/assets/912f4ec4-22b7-428b-8043-d5ba7fc663c2)

Now, what if the API is not available anymore?
Or what if you have a error in Snowflake or what if you made a mistake
in your transformations with DBT.

![image](https://github.com/user-attachments/assets/7fad8fa9-707f-464a-a025-54f5d32d7be2)

As you can see at every step, you can end up with a failure and you need
to have a tool that manages this.
Also,what if instead of having one data pipeline, you have 
hundreds of data pipelines.

![image](https://github.com/user-attachments/assets/a466bc9d-2bae-4782-9ae0-4fbdfaa0f86b)

As you can imagine, it's gonna be a nightmare for you, and 
this is why you need Airflow.
With Airflow you are able to manage failures automatically,
even if you have hundreds of data pipelines and millions of tasks.
So if you want to make your life easier, well, you are at the right place.

---

# What is Airflow? 
Think of Airflow as a cook, following a recipe where the 
recipe is your data pipeline. 
You have to follow this recipe by putting the right ingredients with 
the right quantity in the right order. 
And that's exactly what Airflow allows you. 
Instead of having your recipe, you have your data pipeline and your ingredients 
are your tasks, and you want to make sure that they are executed in the right order. 
That being said, let me give you some technical terms to 
explain exactly what is Airflow. 
First thing first, Airflow is an open source platform, an open source 
project to programmatically, author, schedule and monitor workflows. 
The workflows are your data pipelines. 
There are some benefits of using Airflow and the first one is, everything is 
coded in Python or everything is dynamic. 
Okay. 
You don't have to use a static language like XML, if you used Oozie in the past. 
With Airflow everything is coded in Python and so you can benefit from that language. 
It is also very easy to use. 
Next, it is very scalable. 
Indeed, you can execute as many tasks as you want with Airflow. 
Also, you have access to a beautiful user interface, which 
is nice to have to monitor your tasks and your data pipelines. 
Then last but not least, Airflow is truly extensible. 
So you can add your own plugins, your own functionalities to Airflow.

You don't have to wait for anyone to add anything on Airflow. 
You can do it by yourself. 
So keep in mind that Airflow is an orchestrator. 
It allows you to execute your tasks in the right way, in the 
right order at the right time.

## Core Components 
Airflow brings core components, and it's always good to know what they are. 
And the first core component is the web server. 
The web server is a flask Python web server that allows you to 
access the user interface. 
Also, you have the scheduler. 
The scheduler is very critical because it is in charge of scheduling your tasks, 
your data pipelines. 
So you want to make sure that your scheduler works otherwise, nothing work. 
Then you have the metadatabase or the metastore. 
The metadatabase is nothing more than a database that is 
compatible with SQL alchemy. 
For example, Postgres, MySQL, Oracle DB, SQL server, and so on. 
In this database, you will have metadata related to your data 
pipelines, your tasks, airflow users, and so on, that will be stored. 
In addition to those components, you have another one, which is the triggerer. 
I won't dive into the details here, but the triggerer allows you to run 
a specific kind of tasks that we are going to see later in the course. 
That being said, those four core components are the components 
that you will see as soon as you run Airflow for the first time. 
In addition, you have a concept called executor and an executor defines how and 
on which support your tasks are executed. 
For example, if you have a Kubernetes cluster, you want to execute your 
tasks on this Kubernetes cluster, you will use the KubernetesExecutor. 
If you want to execute your tasks in a Celery cluster, Celery is 
a Python framework to execute multiple tasks on multiple machines, 
you will use the CeleryExecutor. 
Keep in mind that the executor doesn't execute any tasks. 
Now, if you use the CeleryExecutor for example, you will have two additional 
core components, a queue, and a worker. 
In a queue your tasks will be pushed in it in order to execute them in the 
right order, and the worker is where your tasks are effectively executed. 
Now, keep in mind that with any executor, you always have a queue in order to 
execute your tasks in the correct order. 
And if you don't have a worker, you have some sub processes 
where your tasks are executed or some PODs if you use Kubernetes. 
So that's all the core components that you need to remember.

---

8. Core Concepts 
Let me give you the core concepts of Airflow that you need to know. 
And the first one is the concept of DAG.
What is a DAG? 
A DAG means directed acyclic graph, and it's nothing more than a graph with 
nodes, directed edges and no cycles. 
For example, here you have a DAG. 
T4, T1, T2, T3 are the nodes, the tasks. 
You also have directed dependencies or edges. 
T4 depends on T1, T2, and T3. 
Then last but not least, you don't have any cycle. 
That's what you can see here. 
This, is not a DAG. 
Why? 
Because there is a cycle. 
That's what you can see with T4 depends on T1 and T1 depends on T
