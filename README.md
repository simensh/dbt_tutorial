# dbt_tutorial

DBT Fundamentals with DBT Core & DuckDB
Introduction
This repository contains most of the necessary files and resources for the DBT Fundamentals Course, originally designed for DBT Cloud, now implemented using DBT Core. The course is designed to provide learners with a thorough understanding of DBT (Data Build Tool) and its applications in data transformation, modeling, testing, and documentation.

The warehouse used in this project is DuckDB

# Prerequisites
Before starting with this course, you should have a basic understanding of SQL and data warehousing concepts. Familiarity with Git for version control is also recommended.

# Software Requirements
Git
Python 3.7 or higher
DBT Core

# Installation
Follow the instructions in development.md file, and you will download and install everything needed to run dbt on DuckDB locally.

# Loading of data
Load data into dbt:

```bash
dbt seed
```

# Running the transformation of the data

```bash
dbt run --select stg_customerd.ql
```

# Usage
After installation, you can start using the repository to work through the DBT Fundamentals course. The course is divided into modules. The concepts from all modules were implemented in this repository

# Acknowledgments
DBT Labs for providing the fundamentals course content.

The DBT community for invaluable resources and support.
This repository is a student-led initiative and is not directly affiliated with DBT Labs

Reference:
Dbt Fundamentals: https://courses.getdbt.com/courses/fundamentals

Quickstart Guide for dbt Cloud and BigQuery: https://docs.getdbt.com/guides/bigquery?step=1

Dbt Core Installation: https://www.youtube.com/watch?v=TVuLrOMvVco
