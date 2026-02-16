# Quick Reference Guide - IBM Data Engineering

> **Purpose**: Fast lookup for key concepts, commands, and patterns across all modules. Perfect for interview prep and daily work.

---

## 📋 Table of Contents

- [Module 01: Data Engineering Ecosystem](#module-01-data-engineering-ecosystem)
- [Module 02: Python for Data Engineering](#module-02-python-for-data-engineering)
- [Module 03: SQL & Relational Databases](#module-03-sql--relational-databases)
- [Module 04: NoSQL Databases](#module-04-nosql-databases)
- [Module 05: ETL & Data Pipelines](#module-05-etl--data-pipelines)
- [Module 06: Data Warehousing](#module-06-data-warehousing)
- [Module 07: Big Data Fundamentals](#module-07-big-data-fundamentals)
- [Module 08: Apache Spark](#module-08-apache-spark)
- [Module 09: Apache Airflow](#module-09-apache-airflow)
- [Module 10: Kafka & Stream Processing](#module-10-kafka--stream-processing)
- [Essential Commands Cheat Sheet](#essential-commands-cheat-sheet)
- [Common Patterns & Best Practices](#common-patterns--best-practices)

---

## Module 01: Data Engineering Ecosystem

### Key Concepts

**Data Engineering Definition**  
> Converting raw data into usable, analytics-ready data that is accurate, reliable, compliant, and accessible.

**Modern Data Ecosystem - 3 Stages**
1. **Data Acquisition** → Extract from diverse sources (structured, unstructured, streaming)
2. **Data Organization** → Clean, transform, comply with standards
3. **Data Consumption** → Deliver via APIs, dashboards, applications

**Data Roles Hierarchy**
```
Raw Data → [Data Engineer] → Usable Data
         → [Data Analyst] → Insights
         → [Data Scientist] → Predictions
         → [Business Analyst] → Decisions
```

### Critical Skills (Priority Order)
1. **SQL** - Absolutely essential
2. **Python** - Primary programming language
3. **Data Modeling** - Schema design, normalization
4. **ETL/ELT** - Pipeline design and orchestration
5. **Communication** - Technical & non-technical stakeholders

### Specialized Roles

| Role | Focus | Key Deliverable |
|------|-------|-----------------|
| **Data Warehouse Engineer** | Build & maintain data warehouses | ETL pipelines, DWH design |
| **Data Architect** | Overall architecture design | Scalable data systems |
| **Data Manager** | Governance & strategy | Policies, compliance |
| **Database Administrator** | Database operations | Reliability, security |

### Quick Wins
- ✅ Master SQL first - it's non-negotiable
- ✅ Soft skills matter more than you think
- ✅ Embrace continuous learning
- ✅ Choose 1-2 specializations, understand all areas

---

## Module 02: Python for Data Engineering

### Essential Libraries
```python
# Data Processing
import pandas as pd
import numpy as np

# Database Connectivity
import psycopg2          # PostgreSQL
import pymongo           # MongoDB
import sqlalchemy        # ORM

# ETL & Workflow
import apache_beam
import prefect
import luigi

# File I/O
import json
import csv
import pickle
```

### Common Data Operations
```python
# Read CSV
df = pd.read_csv('data.csv')

# Data Cleaning
df.dropna()                    # Remove nulls
df.drop_duplicates()           # Remove duplicates
df.fillna(0)                   # Fill nulls

# Data Transformation
df['new_col'] = df['col'].apply(lambda x: x * 2)
df.groupby('category').agg({'value': 'sum'})

# Write to Database
df.to_sql('table_name', engine, if_exists='replace')
```

### File Operations
```python
# Read JSON
with open('data.json', 'r') as f:
    data = json.load(f)

# Write CSV
with open('output.csv', 'w') as f:
    writer = csv.writer(f)
    writer.writerows(data)
```

---

## Module 03: SQL & Relational Databases

### Essential SQL Commands

**Data Definition Language (DDL)**
```sql
-- Create table
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    dept_id INTEGER,
    salary DECIMAL(10,2),
    hire_date DATE
);

-- Add index
CREATE INDEX idx_dept ON employees(dept_id);

-- Add constraint
ALTER TABLE employees 
ADD CONSTRAINT fk_dept 
FOREIGN KEY (dept_id) REFERENCES departments(id);
```

**Data Manipulation Language (DML)**
```sql
-- Insert
INSERT INTO employees (name, dept_id, salary) 
VALUES ('John Doe', 1, 75000);

-- Update
UPDATE employees 
SET salary = salary * 1.1 
WHERE dept_id = 1;

-- Delete
DELETE FROM employees 
WHERE hire_date < '2020-01-01';
```

**Queries**
```sql
-- Basic SELECT with JOIN
SELECT e.name, d.dept_name, e.salary
FROM employees e
JOIN departments d ON e.dept_id = d.id
WHERE e.salary > 50000
ORDER BY e.salary DESC;

-- Aggregations
SELECT dept_id, 
       COUNT(*) as emp_count,
       AVG(salary) as avg_salary,
       MAX(salary) as max_salary
FROM employees
GROUP BY dept_id
HAVING COUNT(*) > 5;

-- Window Functions
SELECT name, salary,
       AVG(salary) OVER (PARTITION BY dept_id) as dept_avg,
       RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) as rank
FROM employees;

-- CTEs (Common Table Expressions)
WITH high_earners AS (
    SELECT * FROM employees WHERE salary > 100000
)
SELECT dept_id, COUNT(*) 
FROM high_earners 
GROUP BY dept_id;
```

### Database Design Principles
- **1NF**: No repeating groups, atomic values
- **2NF**: No partial dependencies on composite keys
- **3NF**: No transitive dependencies
- **Indexing**: Add indexes on foreign keys and frequently queried columns
- **Constraints**: Use NOT NULL, UNIQUE, CHECK, FOREIGN KEY

---

## Module 04: NoSQL Databases

### Database Types & Use Cases

| Type | Examples | Use Case | Key Feature |
|------|----------|----------|-------------|
| **Document** | MongoDB, CouchDB | Flexible schemas, JSON data | Nested documents |
| **Key-Value** | Redis, DynamoDB | Caching, sessions | Fast lookups |
| **Column-Family** | Cassandra, HBase | Time-series, analytics | Wide rows |
| **Graph** | Neo4J, ArangoDB | Social networks, recommendations | Relationships |

### MongoDB Basics
```javascript
// Insert
db.users.insertOne({
    name: "John Doe",
    email: "john@example.com",
    tags: ["developer", "data"]
})

// Query
db.users.find({ "tags": "developer" })

// Update
db.users.updateOne(
    { email: "john@example.com" },
    { $set: { status: "active" } }
)

// Aggregation
db.users.aggregate([
    { $match: { status: "active" } },
    { $group: { _id: "$department", count: { $sum: 1 } } }
])
```

### Redis Basics
```python
import redis
r = redis.Redis(host='localhost', port=6379)

# Set/Get
r.set('key', 'value')
r.get('key')

# Hash
r.hset('user:1000', 'name', 'John')
r.hgetall('user:1000')

# List
r.lpush('queue', 'task1')
r.rpop('queue')
```

---

## Module 05: ETL & Data Pipelines

### ETL vs ELT

**ETL (Extract-Transform-Load)**
```
Source → Extract → Transform → Load → Data Warehouse
```
- Transform before loading
- Good for structured, predictable transformations
- Traditional data warehousing

**ELT (Extract-Load-Transform)**
```
Source → Extract → Load → Data Lake → Transform → Analytics
```
- Transform after loading
- Leverages cloud compute power
- Modern cloud data warehouses

### Pipeline Design Principles
1. **Idempotency** - Same input = same output (rerunnable)
2. **Incrementality** - Process only new/changed data
3. **Error Handling** - Graceful failures, retries
4. **Monitoring** - Logs, alerts, metrics
5. **Data Quality** - Validation at each stage

### Common ETL Pattern
```python
def extract():
    """Pull data from source"""
    return source_db.query("SELECT * FROM orders")

def transform(data):
    """Clean and enrich data"""
    data = clean_nulls(data)
    data = add_calculated_fields(data)
    return data

def load(data):
    """Write to destination"""
    target_db.bulk_insert("orders", data)

# Execute pipeline
raw_data = extract()
transformed = transform(raw_data)
load(transformed)
```

---

## Module 06: Data Warehousing

### Star Schema
```
        [Time Dimension]
               |
[Product] ← [Fact Table] → [Customer]
               |
        [Location Dimension]
```

**Fact Table**: Metrics/measures (sales, quantity, revenue)  
**Dimension Tables**: Descriptive attributes (who, what, when, where)

### Snowflake Schema
```
[Product] → [Category] → [Department]
    ↓
[Fact Table]
    ↓
[Customer] → [City] → [State]
```

**Normalized dimensions** - Dimensions broken into sub-dimensions

### Slowly Changing Dimensions (SCD)

**Type 1** - Overwrite (no history)
```sql
UPDATE customer SET address = 'New Address' WHERE id = 123;
```

**Type 2** - Add row (full history)
```sql
-- Old row
id | name | address    | valid_from | valid_to   | is_current
1  | John | Old Addr   | 2020-01-01 | 2024-12-31 | false

-- New row
2  | John | New Addr   | 2025-01-01 | NULL       | true
```

**Type 3** - Add column (limited history)
```sql
id | name | current_address | previous_address
1  | John | New Addr       | Old Addr
```

---

## Module 07: Big Data Fundamentals

### The 5 V's of Big Data
1. **Volume** - Massive scale (TB, PB)
2. **Velocity** - High speed generation/processing
3. **Variety** - Diverse data types
4. **Veracity** - Data quality/trustworthiness
5. **Value** - Actionable insights

### Hadoop Ecosystem
```
HDFS (Storage)
    ↓
MapReduce (Processing)
    ↓
YARN (Resource Management)
    ↓
Hive/Pig (Query Layers)
```

### MapReduce Concept
```python
# Map phase
def map(document):
    for word in document.split():
        emit(word, 1)

# Reduce phase
def reduce(word, counts):
    emit(word, sum(counts))
```

---

## Module 08: Apache Spark

### Spark Basics
```python
from pyspark.sql import SparkSession

# Initialize
spark = SparkSession.builder \
    .appName("MyApp") \
    .getOrCreate()

# Read data
df = spark.read.csv("data.csv", header=True, inferSchema=True)

# Transformations (lazy)
df_filtered = df.filter(df['age'] > 25)
df_grouped = df.groupBy('department').count()

# Actions (eager)
df_filtered.show()
df_grouped.collect()
result = df.count()
```

### Common Operations
```python
# Select columns
df.select('name', 'age')

# Filter
df.filter(df['salary'] > 50000)
df.where(df['dept'] == 'Engineering')

# Aggregations
df.groupBy('dept').agg({'salary': 'avg', 'id': 'count'})

# Join
df1.join(df2, df1['id'] == df2['user_id'], 'inner')

# SQL
df.createOrReplaceTempView("employees")
spark.sql("SELECT * FROM employees WHERE salary > 50000")
```

---

## Module 09: Apache Airflow

### DAG (Directed Acyclic Graph)
```python
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime

default_args = {
    'owner': 'data-team',
    'retries': 3,
    'retry_delay': timedelta(minutes=5)
}

dag = DAG(
    'etl_pipeline',
    default_args=default_args,
    schedule_interval='@daily',
    start_date=datetime(2025, 1, 1),
    catchup=False
)

def extract():
    # Extract logic
    pass

def transform():
    # Transform logic
    pass

def load():
    # Load logic
    pass

# Define tasks
extract_task = PythonOperator(task_id='extract', python_callable=extract, dag=dag)
transform_task = PythonOperator(task_id='transform', python_callable=transform, dag=dag)
load_task = PythonOperator(task_id='load', python_callable=load, dag=dag)

# Set dependencies
extract_task >> transform_task >> load_task
```

### Common Operators
- `PythonOperator` - Execute Python functions
- `BashOperator` - Execute bash commands
- `EmailOperator` - Send emails
- `SqlOperator` - Execute SQL
- `S3ToRedshiftOperator` - Cloud data movement

---

## Module 10: Kafka & Stream Processing

### Kafka Concepts
- **Producer** - Sends messages to topics
- **Consumer** - Reads messages from topics
- **Topic** - Category/feed of messages
- **Partition** - Ordered sequence within topic
- **Broker** - Kafka server

### Producer Example
```python
from kafka import KafkaProducer
import json

producer = KafkaProducer(
    bootstrap_servers=['localhost:9092'],
    value_serializer=lambda v: json.dumps(v).encode('utf-8')
)

producer.send('orders', {'order_id': 123, 'amount': 99.99})
producer.flush()
```

### Consumer Example
```python
from kafka import KafkaConsumer

consumer = KafkaConsumer(
    'orders',
    bootstrap_servers=['localhost:9092'],
    auto_offset_reset='earliest',
    value_deserializer=lambda m: json.loads(m.decode('utf-8'))
)

for message in consumer:
    print(message.value)
```

---

## Essential Commands Cheat Sheet

### Git
```bash
git clone <repo>
git add .
git commit -m "message"
git push origin main
git pull
git status
```

### Docker
```bash
docker build -t image-name .
docker run -p 5432:5432 postgres
docker ps
docker stop container-id
docker-compose up -d
```

### Linux/Bash
```bash
# File operations
ls -la
cd /path/to/dir
mkdir new-folder
rm -rf folder
cp source dest

# Process management
ps aux | grep python
kill -9 PID
top

# Networking
curl https://api.example.com
wget https://file.com/data.csv
netstat -tuln
```

---

## Common Patterns & Best Practices

### Data Pipeline Best Practices
✅ **DO**:
- Make pipelines idempotent
- Process incrementally when possible
- Add comprehensive logging
- Implement data quality checks
- Use version control for all code
- Document data lineage
- Set up monitoring and alerts

❌ **DON'T**:
- Hard-code credentials
- Skip error handling
- Process full datasets unnecessarily
- Ignore data quality issues
- Deploy without testing
- Skip documentation

### Performance Optimization
1. **Indexing** - Add indexes on frequently queried columns
2. **Partitioning** - Split large tables by date/region
3. **Caching** - Cache frequently accessed data
4. **Batch Processing** - Process in batches vs row-by-row
5. **Parallel Processing** - Use Spark for large datasets
6. **Query Optimization** - Use EXPLAIN PLAN, avoid SELECT *

### Data Quality Checks
```python
def validate_data(df):
    # Check nulls
    assert df['id'].notnull().all(), "ID column has nulls"
    
    # Check duplicates
    assert df['id'].is_unique, "Duplicate IDs found"
    
    # Check data types
    assert df['amount'].dtype == 'float64', "Amount not numeric"
    
    # Check ranges
    assert (df['age'] >= 0).all(), "Negative ages found"
    
    return True
```

---

## Interview Prep - Key Questions

### Conceptual
- What's the difference between ETL and ELT?
- Explain star schema vs snowflake schema
- What are the CAP theorem tradeoffs?
- How do you handle slowly changing dimensions?

### Technical
- Write a SQL query with window functions
- Design a data pipeline for [specific use case]
- Optimize a slow-running query
- Explain Spark's lazy evaluation

### Behavioral
- Describe a time you optimized a data pipeline
- How do you ensure data quality?
- How do you communicate technical concepts to non-technical stakeholders?

---

**Last Updated**: February 15, 2025  
**Status**: In Progress (Module 1 Complete)

*This quick reference will be updated as new modules are completed.*