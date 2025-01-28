# dbt_tutorial

DBT Fundamentals with DBT Core & DuckDB
Introduction
This repository contains most of the necessary files and resources for the DBT Fundamentals Course, originally designed for DBT Cloud, now implemented using DBT Core. The course is designed to provide learners with a thorough understanding of DBT (Data Build Tool) and its applications in data transformation, modeling, testing, and documentation.

The warehouse used in this project is DuckDB

# Prerequisites
Before starting with this course, you should have a basic understanding of SQL and data warehousing concepts. Familiarity with Git for version control is also recommended.

# Software Requirements
Git
Python 3.8 or higher
DBT Core

# Installation
Follow the instructions in th [development.md] file, and you will download and install everything needed to run dbt on DuckDB locally.
Make sure that ``` dbt debug ``` runc successfully before you continue to start loading data.

# Loading of data
Load data into dbt:

```bash
dbt seed
```
This has to be done first to be able to build all the models.

# Running the transformation of the data

Run each specific model by specifying the file name after ``` dbt run --select ```.

```bash
dbt run --select stg_customers
```
Continue with the other files (stg_orders, stg_payments) before you can build the orders and customers tables.
After building all the models, you can run ``` dbt test ``` to verify that the data tests alse succeed.

# Creating the documentation

After building all the tables in the project, run the following code to see all the details about the tables, and the lineage of the data mode.

```bash
dbt docs generate 
dbt docs serve
```

# Querying the data

To be able to query the data, we can use the DuckDB database which has been installed through the requirements.txt file. 
Launch a DuckDB command-line interface (CLI):
```bash
duckcli dbt_tutorial.duckdb
```

Run a query at the prompt and exit:

```bash
select * from customers where customer_id = 42;
exit;
```

# Acknowledgments
DBT Labs for providing the fundamentals course content.

The DBT community for invaluable resources and support.
This repository is a student-led initiative and is not directly affiliated with DBT Labs

Reference:
Dbt Fundamentals: https://courses.getdbt.com/courses/fundamentals

Dbt Core Installation: https://www.youtube.com/watch?v=TVuLrOMvVco
