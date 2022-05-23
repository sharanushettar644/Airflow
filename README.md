# Apache Airflow 
---
## Introduction

In this project we need to create S3 Bucket , Airflow , private vpc.
Write Python code and Shellscript

## Project Plan
In this project we used some tools:
- Aws Airflow
- S3 Bucket
- slack

## Phase-1
## Infrastructure
---
Amazon Managed Workflows for Apache Airflow (MWAA) is a managed orchestration service for Apache Airflow that makes it easier to setup and operate end-to-end data pipelines in the cloud at scale. Apache Airflow is an open-source tool used to programmatically author, schedule, and monitor sequences of processes and tasks referred to as "workflows." With Amazon MWAA, you can use Airflow and Python to create workflows without having to manage the underlying infrastructure for scalability, availability, and security. 

![image alt text](https://docs.aws.amazon.com/mwaa/latest/userguide/images/mwaa-architecture.png?raw=)

## Working of Apache Airflow 
Apache Airflow accomplishes the tasks by taking DAG(Directed Acyclic Graphs) as an array of the workers, some of these workers have particularized contingencies. It results in the formation of DAG in Python itself which make these DAGs used easily further for the other processes. This results in the changing of a workflow into a well-defined code which further makes a workflow testable, maintainable, Co-operative.



## Airflow Components
In addition to DAGs, Operators and Tasks, the Airflow offers the following components:
- User interface —lets you view DAGs, Tasks and logs, trigger runs and debug DAGs. This is the easiest way to keep track of your overall Airflow installation and dive into specific DAGs to check the status of tasks.

- Hooks—Airflow uses Hooks to interface with third-party systems, enabling connection to external APIs and databases (e.g. Hive, S3, GCS, MySQL, Postgres). Hooks should not contain sensitive information such as authentication credentials.

- Providers—packages containing the core Operators and Hooks for a particular service. They are maintained by the community and can be directly installed on an Airflow environment.
Plugins—a variety of Hooks and Operators to help perform certain tasks, such as sending data from SalesForce to Amazon Redshift.

- Connections—these contain information that enable a connection to an external system. This includes authentication credentials and API tokens. You can manage connections directly from the UI, and the sensitive data will be encrypted and stored in PostgreSQL or MySQL.


## Core components
Airflow primary consists of the following components -

- Scheduler
- Webserver
- Executor
- Backend
- Scheduler

It is responsible for scheduling your tasks according to the frequency mentioned. It looks for all the eligible DAGs and then puts them in the queue. If a DAG failed and retry is enabled, the scheduler will automatically put that DAG up for retry. The number of retries can be limited on a DAG level.

#### Webserver
The webserver is the frontend for Airflow. Users can enable/disable, retry, and see logs for a DAG all from the UI. Users can also drill down in a DAG to see which tasks have failed, what caused the failure, how long did the task run for, and when was the task last retried.

This UI makes Airflow superior to its competitors. e.g., In Apache Oozie, seeing logs for non-MR (map-reduce) jobs is a pain.

#### Executor
It is responsible for actually running a task. Executor controls on which worker to run a task, how many tasks to run in parallel, and update the status of the task as it progress.

You can run your task on multiple workers managed by Celery or Dask or Kubernetes.

The tasks are pulled from a queue, which can be either Redis or RabbitMQ.

By default, Airflow uses SerialExecutor, which only runs one task at a time on a local machine. This is not advised to be done in production.

#### Backend
Airflow uses MySQL or PostgreSQL to store the configuration as well as the state of all the DAG and task runs. By default, Airflow uses SQLite as a backend by default, so no external setup is required. The SQLite backend is not recommended for production since data loss is probable.

## DAG 
DAGs can be run multiple times, and multiple DAG runs can happen in parallel. DAGs can have multiple parameters indicating how they should operate, but all DAGs have the mandatory parameter execution_date.

You can indicate dependencies for Tasks in the DAG using the characters >> and << :

> first_task >> [second_task, third_task]

> third_task << fourth_task

By default, tasks have to wait for all upstream tasks to succeed before they can run, but you can customize how tasks are executed with features such as LatestOnly, Branching, and Trigger Rules.

To manage complex DAGs, you can use SubDAGs to embed "reusable" DAGs into others. You can also visually group tasks in the UI using TaskGroups

![image alt text](https://assets-global.website-files.com/61e95e54543a7c0a5967ffd1/61fd443d0cc67c714baeae7a_61e95e54543a7cf4d46803a5_Airflow-diagram-3.png?raw=)




## Phase-2
### S3 Bucket & Python code
---
- Create S3 Bucket , in that Bucket create one folder and name it as DAG.
- Write Python code which import DAG from airflow.
- Python or Shellscript which need to be executed in airflow that need to be kept in DAG folder in S3.
- If we want to run shellscript in airflow . In the Python code you need to specify the shellscript name.
- Schedule the job should be written in the script itself.

### Airflow
- To create airflow we need private VPC.
- While creating airflow we need to connect with S3 bucket and specify DAG folder in S3.
- Create IAM role , Security Group and assign to it.
- After creating airflow you can able to see job's in Airflow UI , you need to turn-on  manually the job's.
- You can able to see log's , Graph view , Task Duration and Tree structure.
- We have integrate Airflow to slack. So that if any job failed we will get notification to slack. 

![image alt text](https://github.com/sharanushettar644/Airflow/blob/main/airflow.drawio.png?raw=)
