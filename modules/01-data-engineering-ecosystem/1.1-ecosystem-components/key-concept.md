# Module 1.1: Key Concepts - Quick Reference

> **Purpose**: Fast lookup for Module 1.1 ecosystem components. Perfect for interview prep and daily work.

---

## 🎯 The Essentials (Must Know)

### Critical Statistics
- **80% of data is unstructured**
- **2.5 quintillion bytes** generated daily
- **Spark is 100x faster** than Hadoop (in-memory vs disk)
- **YouTube**: Hours of footage uploaded every 60 seconds

---

## 🗂️ Data Classification

### Three Types Quick Comparison

| Type | Structure | Examples | Storage |
|------|-----------|----------|---------|
| **Structured** | Rigid rows/columns | Databases, spreadsheets, GPS data | RDBMS, Data Warehouse |
| **Semi-Structured** | Tags/metadata, hierarchical | JSON, XML, emails | NoSQL, Document stores |
| **Unstructured** | No structure | Images, videos, PDFs, social media | Data Lakes, NoSQL |

### Memory Aid: "SSU"
- **S**tructured = **S**preadsheet-like
- **S**emi = **S**ome organization (tags)
- **U**nstructured = **U**norganized

---

## 📄 File Formats Cheat Sheet

### Quick Selection Guide

| Format | Best For | Avoid For |
|--------|----------|-----------|
| **CSV** | Simple data exchange, cross-platform | Complex relationships, large files |
| **JSON** | APIs, web services, hierarchical data | Human readability, very large files |
| **XML** | Data exchange, hierarchical, platform-independent | Performance-critical apps |
| **XLSX** | Complex calculations, multiple sheets, business users | Automation, large datasets |
| **PDF** | Documents, forms, consistent formatting | Data extraction, processing |

### One-Liner Each
- **CSV**: Simplest format, comma-separated values
- **JSON**: Modern API standard, key-value pairs
- **XML**: Self-descriptive tags, platform-independent
- **XLSX**: Excel workbooks with formulas and formatting
- **PDF**: Platform-independent document format

---

## 🌐 Data Sources

### Quick Reference Table

| Source Type | Examples | Use Case | Tools |
|-------------|----------|----------|-------|
| **Internal RDBMS** | SQL Server, MySQL, Oracle | Transactional data | SQL, ODBC |
| **APIs** | Twitter API, Financial APIs | Real-time data | Python requests, REST |
| **Web Scraping** | Product prices, forum posts | Public web data | BeautifulSoup, Scrapy |
| **Streaming** | IoT sensors, social media | Real-time events | Kafka, Spark Streaming |
| **Flat Files** | CSV, Excel exports | Batch data loads | Pandas, SQL Loader |
| **RSS Feeds** | News sites, blogs | Content updates | Feed readers |

### Popular API Use Cases
1. **Social Media**: Twitter/Facebook → Sentiment analysis
2. **Financial**: Stock APIs → Trading analysis
3. **Validation**: ZIP code APIs → Data cleaning
4. **Government**: Census data → Demographics

---

## 💻 Programming Languages

### Essential Language Map

```
Task → Language
├── Database Queries → SQL ⭐ (MUST KNOW)
├── Data Processing → Python ⭐ (PRIMARY)
├── Statistical Analysis → R
├── Big Data → Java, Scala
├── Automation → Bash, PowerShell
├── Web Scraping → Python
└── Visualization → R, Python
```

### SQL (Non-Negotiable!)
```sql
-- The 5 Essential Operations
SELECT * FROM table WHERE condition;      -- Query
INSERT INTO table VALUES (...);           -- Insert
UPDATE table SET col = value WHERE ...;   -- Update
DELETE FROM table WHERE condition;        -- Delete
CREATE TABLE table (...);                 -- Define
```

### Python (Swiss Army Knife)
```python
# Essential Libraries
import pandas as pd        # Data manipulation
import numpy as np         # Numerical operations
import sqlalchemy          # Database connectivity
from bs4 import BeautifulSoup  # Web scraping
import json, csv           # File formats
```

### Language Strengths Quick Summary
- **SQL**: Querying, RDBMS operations → Everyone needs it
- **Python**: Versatile, easy, vast libraries → Most popular
- **R**: Statistical analysis, visualization → Academic/stats
- **Java**: Big Data (Hadoop, Spark) → Enterprise scale
- **Bash**: Unix automation → DevOps, scheduling
- **PowerShell**: Windows automation → Microsoft stack

---

## 🗄️ Data Repositories

### Database Type Selector

```
Question Flow:
├─ Need ACID compliance? → YES → RDBMS
├─ Flexible schema needed? → YES → NoSQL
├─ Historical analytics? → YES → Data Warehouse
├─ Department-specific? → YES → Data Mart
├─ Store everything raw? → YES → Data Lake
└─ Modern BI + ML? → YES → Lakehouse
```

### RDBMS (Relational)

**When to Use**:
- ✅ Structured data
- ✅ ACID compliance needed
- ✅ Complex relationships (JOINs)
- ✅ Transaction processing (OLTP)

**Popular**: MySQL, PostgreSQL, Oracle, SQL Server

**Example Use Cases**:
- Banking transactions
- E-commerce orders
- Customer records
- HR systems

---

### NoSQL (Four Types)

#### 1. Key-Value
**Structure**: `{key: value}`  
**Example**: Redis, DynamoDB  
**Use**: Caching, sessions, preferences  
**Speed**: ⚡⚡⚡ (Fastest)

#### 2. Document
**Structure**: JSON-like documents  
**Example**: MongoDB, CouchDB  
**Use**: Content management, catalogs, user profiles  
**Flexibility**: ⭐⭐⭐ (Most flexible)

#### 3. Column-Family
**Structure**: Columns grouped together  
**Example**: Cassandra, HBase  
**Use**: Time-series, IoT, heavy writes  
**Scale**: 📊📊📊 (Best for writes)

#### 4. Graph
**Structure**: Nodes + relationships  
**Example**: Neo4J, CosmosDB  
**Use**: Social networks, fraud detection  
**Relationships**: 🔗🔗🔗 (Best for connected data)

---

### Data Warehouses

**Definition**: Central repository for analytics

**3-Tier Architecture**:
```
Top: Client Tools (BI, Reporting)
     ↑
Middle: OLAP Server (Analytics)
     ↑
Bottom: Database Servers (Storage)
```

**Popular**: Snowflake, RedShift, BigQuery, Teradata

**Use Cases**:
- Business intelligence
- Historical analysis
- Complex reporting
- OLAP queries

---

### Data Lakes vs Data Warehouses

| Aspect | Data Lake | Data Warehouse |
|--------|-----------|----------------|
| **Data** | Raw, all types | Processed, structured |
| **Schema** | Schema-on-read | Schema-on-write |
| **Users** | Data scientists | Business analysts |
| **Agility** | High (flexible) | Lower (rigid) |
| **Cost** | Low (cheap storage) | High (compute + storage) |
| **Processing** | ELT | ETL |

---

### Data Lakehouse (Modern Hybrid)

**Restaurant Analogy**:
```
Loading Dock = Data Lake (raw ingredients)
Pantry/Freezer = Data Warehouse (organized, ready)
Lakehouse = Efficient system combining both
```

**Benefits**:
- ✅ Flexibility of lake
- ✅ Performance of warehouse
- ✅ Support BI + ML workloads
- ✅ Built-in governance
- ✅ Cost-effective

---

## 🔄 ETL vs ELT

### Side-by-Side Comparison

| Aspect | ETL (Traditional) | ELT (Modern) |
|--------|-------------------|--------------|
| **Process** | Extract → Transform → Load | Extract → Load → Transform |
| **Transform Where** | Staging area | Target system |
| **Best For** | Structured data | All data types |
| **Destination** | Data Warehouse | Data Lake |
| **Technology** | On-premise | Cloud-native |
| **Speed** | Slower (transform first) | Faster (load immediately) |
| **Flexibility** | Less (predefined transformations) | More (transform as needed) |
| **Use Case** | Traditional BI | Big Data, ML |

### When to Use What

**Use ETL When**:
- Structured data only
- Predefined transformations
- On-premise infrastructure
- Traditional data warehouse
- Compliance requires clean data before loading

**Use ELT When**:
- Big Data (TB/PB scale)
- Cloud data warehouse/lake
- Exploratory analysis needed
- Multiple use cases for same data
- Want to keep raw data

---

### Data Pipelines (Broader Concept)

**Definition**: Complete journey from source → destination

**Types**:
```
Data Pipeline
├── Batch: Scheduled, large chunks
├── Streaming: Real-time, continuous
└── Hybrid: Both batch + streaming
```

**Popular Tools**:
- **Apache Airflow** (orchestration)
- **Apache Beam** (unified batch/stream)
- **Google DataFlow** (managed service)

**Streaming Tools**:
- **Apache Kafka** (message queue)
- **Apache Spark Streaming** (processing)
- **Apache Storm** (real-time computation)

---

## 📊 Big Data Fundamentals

### The 5 V's (Know These Cold!)

#### 1. **Velocity** - Speed of Data
> **Example**: Hours of YouTube footage uploaded every 60 seconds

**Key Points**:
- Data generated extremely fast
- Real-time streaming
- Continuous process

#### 2. **Volume** - Scale of Data
> **Example**: 2.5 quintillion bytes daily = 10 million Blu-ray DVDs

**Key Points**:
- Massive amounts
- Continuous growth
- Scalable infrastructure needed

#### 3. **Variety** - Diversity of Data
> **Example**: Text, images, video, sensor data, social media

**Key Points**:
- Structured + semi + unstructured
- Multiple sources
- Different formats

#### 4. **Veracity** - Quality of Data
> **Challenge**: 80% is unstructured, must produce reliable insights

**Key Points**:
- Consistency, completeness, integrity
- Is it real or false?
- Must be validated

#### 5. **Value** - Insights from Data
> **Goal**: Turn data into business value

**Key Points**:
- Business profit
- Medical/social benefits
- Customer satisfaction

---

### Hadoop Ecosystem Quick Guide

```
Apache Hadoop
├── HDFS (Storage)
│   ├── Splits files across nodes
│   ├── Replicates 3x (fault-tolerant)
│   └── Data locality (move compute to data)
├── MapReduce (Processing)
│   ├── Map: Split & process in parallel
│   └── Reduce: Aggregate results
└── YARN (Resource Management)
    ├── Manage cluster resources
    └── Schedule jobs
```

**HDFS Phone Book Example**:
```
Phone Book (All US)
├── Server 1: Last names A-D (+ 2 replicas)
├── Server 2: Last names E-H (+ 2 replicas)
├── Server 3: Last names I-L (+ 2 replicas)
└── Server 4: Last names M-P (+ 2 replicas)
```

---

### Apache Hive

**One-Liner**: SQL-like data warehouse on top of Hadoop

**Characteristics**:
- High latency (slow queries)
- Read-based (not for writes)
- Long sequential scans

**Best For**:
✅ ETL operations  
✅ Data warehousing  
✅ Reporting  
✅ Batch analytics

**Not Good For**:
❌ Real-time queries  
❌ Transaction processing  
❌ High write operations

---

### Apache Spark

**One-Liner**: In-memory distributed processing engine (100x faster than Hadoop)

**Key Feature**: **In-Memory Processing**
- Keeps data in RAM
- Spills to disk only when needed
- Dramatically faster than disk-based

**Languages Supported**:
- Java, Scala
- Python (PySpark) ⭐
- R
- SQL

**Applications**:
- Interactive analytics
- Stream processing
- Machine learning
- Data integration
- ETL

**Data Sources**:
- HDFS, Hive
- Cassandra, HBase
- S3, Cloud storage
- JDBC databases

---

### Hadoop vs Spark

| Aspect | Hadoop MapReduce | Apache Spark |
|--------|------------------|--------------|
| **Processing** | Disk-based | In-memory |
| **Speed** | Slower | 100x faster |
| **Best For** | Large batch jobs | Interactive + real-time |
| **Complexity** | More complex | Easier (Python API) |
| **Use Case** | ETL, data preparation | Analytics, ML, streaming |

---

## 🎯 Quick Decision Trees

### "What Database Should I Use?"

```
Start
├─ Is data structured (rows/columns)? 
│  └─ YES → Need ACID compliance?
│     ├─ YES → RDBMS (PostgreSQL, MySQL)
│     └─ NO → Could use NoSQL if scale needed
└─ NO → What type of data?
   ├─ Key-value pairs → Redis, DynamoDB
   ├─ Documents (JSON) → MongoDB, CouchDB
   ├─ Time-series/IoT → Cassandra, HBase
   └─ Relationships → Neo4J, graph DB
```

### "ETL or ELT?"

```
Start
├─ Is data structured and transformations known?
│  └─ YES → ETL (traditional)
└─ NO → Is it Big Data or cloud-native?
   ├─ YES → ELT (modern)
   └─ Maybe → Consider:
      ├─ Data volume (TB+) → ELT
      ├─ Multiple use cases → ELT
      ├─ Cloud warehouse → ELT
      └─ On-premise DWH → ETL
```

### "Batch or Streaming?"

```
Start
├─ Need real-time insights (seconds)?
│  └─ YES → Streaming (Kafka + Spark)
└─ NO → Can process hourly/daily?
   ├─ YES → Batch (Airflow + Spark)
   └─ BOTH → Hybrid (Lambda architecture)
```

---

## 💡 Interview Q&A

### Q1: "Explain the difference between structured, semi-structured, and unstructured data."

**Perfect Answer**:
> "Structured data fits neatly into rows and columns, like a database table—think customer records with fixed fields. Semi-structured has some organization through tags or metadata, like JSON or XML, where the structure is flexible. Unstructured data has no predefined format—images, videos, PDFs, social media posts. About 80% of data today is unstructured, which is why NoSQL databases and data lakes are so important."

---

### Q2: "When would you use ETL vs ELT?"

**Perfect Answer**:
> "ETL is traditional—you transform data before loading into a data warehouse. Use it when you have structured data with known transformations and an on-premise data warehouse. ELT is modern—you load raw data first, then transform in the target system. Use it for Big Data, cloud environments, when you have multiple use cases for the same data, or when you want to preserve raw data for future analysis. ELT is better for data lakes and cloud data warehouses like Snowflake or BigQuery."

---

### Q3: "What are the 5 V's of Big Data?"

**Perfect Answer**:
> "The 5 V's are: **Velocity** (speed of data generation—YouTube gets hours of footage every minute), **Volume** (scale—2.5 quintillion bytes daily), **Variety** (structured, semi-structured, and unstructured from many sources), **Veracity** (quality and accuracy—80% is unstructured so we must validate), and **Value** (the ultimate goal—turning data into business insights). These define why we need specialized Big Data tools like Hadoop and Spark."

---

### Q4: "Explain the difference between Hadoop and Spark."

**Perfect Answer**:
> "Hadoop uses MapReduce with disk-based processing—it writes intermediate results to disk, which is slower but handles massive batch jobs well. Spark uses in-memory processing, keeping data in RAM, which makes it about 100x faster. Spark is better for interactive analytics, real-time processing, and machine learning. Hadoop is still good for large ETL jobs where cost matters more than speed. In practice, Spark often runs on top of Hadoop's HDFS storage."

---

### Q5: "What's the difference between a data lake and a data warehouse?"

**Perfect Answer**:
> "A data warehouse stores structured, processed data optimized for analytics—think schema-on-write. It's expensive but performant for known queries. A data lake stores raw data in any format—schema-on-read. It's cheaper and more flexible but requires more work to analyze. Data warehouses are for business analysts running SQL queries. Data lakes are for data scientists doing exploratory analysis and ML. Modern lakehouses combine both—giving you the flexibility of a lake with the performance of a warehouse."

---

### Q6: "Why is SQL still relevant in the age of Big Data?"

**Perfect Answer**:
> "SQL is the universal language of data. Even Big Data tools like Spark and Hive have SQL interfaces because it's what everyone knows. It's declarative—you say what you want, not how to get it. It works across systems—from SQLite to Snowflake. And it's proven over 50 years. NoSQL doesn't mean 'no SQL'—it means 'not only SQL.' Most data engineers use SQL daily, regardless of whether they're working with traditional databases or Big Data systems."

---

## 🔧 Practical Examples

### Example 1: E-Commerce Data Pipeline

**Scenario**: Process orders from website

**Solution**:
```
1. Source: PostgreSQL (OLTP)
2. Extract: Python script (scheduled hourly)
3. Transform: Clean, enrich with product data
4. Load: Snowflake (data warehouse)
5. Consume: Tableau dashboards
```

**Technologies**: Python, SQL, Snowflake, Airflow, Tableau

---

### Example 2: Real-Time Fraud Detection

**Scenario**: Detect fraudulent transactions instantly

**Solution**:
```
1. Source: Transaction stream
2. Ingest: Kafka (message queue)
3. Process: Spark Streaming (real-time)
4. Score: ML model (fraud probability)
5. Alert: Flag suspicious transactions
6. Store: Cassandra (fast writes)
```

**Technologies**: Kafka, Spark, Cassandra, Python

---

### Example 3: Social Media Sentiment Analysis

**Scenario**: Analyze brand mentions on Twitter

**Solution**:
```
1. Source: Twitter API
2. Ingest: Kafka (streaming)
3. Store Raw: S3 Data Lake (JSON)
4. Process: Spark (sentiment scoring)
5. Aggregate: Daily sentiment scores
6. Store: PostgreSQL (structured results)
7. Visualize: Grafana dashboards
```

**Technologies**: Python, Kafka, Spark, S3, PostgreSQL

---

## 📝 Cheat Sheets

### File Format Selection

**Need to choose between CSV and JSON?**
- CSV: Tabular data, simple, Excel-compatible
- JSON: Hierarchical data, APIs, nested structures

**XML vs JSON?**
- XML: Enterprise systems, SOAP APIs, legacy
- JSON: Modern APIs, web services, JavaScript

**When to use Parquet?**
- Big Data processing (Spark, Hive)
- Columnar storage for analytics
- Much smaller than CSV for large datasets

---

### NoSQL Database Selection

**Use Redis when**: Caching, sessions, real-time leaderboards  
**Use MongoDB when**: Flexible schemas, rapid development, content management  
**Use Cassandra when**: High write throughput, time-series, IoT  
**Use Neo4J when**: Social networks, recommendations, fraud detection

---

### Python Libraries Quick Reference

```python
# Data Manipulation
import pandas as pd           # DataFrames, CSV/Excel
import numpy as np            # Arrays, math operations

# Databases
import sqlalchemy             # RDBMS connections
import pymongo                # MongoDB
import redis                  # Redis

# Web & APIs
import requests               # HTTP requests
from bs4 import BeautifulSoup # Web scraping
import json                   # JSON parsing

# Big Data
import pyspark                # Spark in Python
from pyspark.sql import SparkSession

# Visualization
import matplotlib.pyplot as plt
import seaborn as sns
```

---

## ✅ Self-Check Questions

**Before moving on, can you answer these?**

1. What percentage of data is unstructured? (Answer: 80%)
2. Name the 5 V's of Big Data (Answer: Velocity, Volume, Variety, Veracity, Value)
3. Which is faster, Hadoop or Spark? Why? (Answer: Spark, 100x due to in-memory)
4. ETL or ELT for a cloud data lake? (Answer: ELT)
5. Which NoSQL type for social networks? (Answer: Graph database)
6. HDFS replicates data how many times? (Answer: 3x by default)
7. What does ACID stand for? (Answer: Atomicity, Consistency, Isolation, Durability)
8. Best language for data engineering? (Answer: Python, but SQL is essential)

---

## 🚀 Next Steps

1. **Practice SQL** - LeetCode, HackerRank, Mode Analytics
2. **Learn Python** - Pandas, NumPy, data manipulation
3. **Explore Big Data** - Databricks Community Edition (free Spark)
4. **Build a pipeline** - End-to-end project on GitHub
5. **Read documentation** - Spark, Airflow, Kafka official docs

---

**Last Updated**: February 15, 2025  
**Module**: 1.1 - Data Engineering Ecosystem Components  
**Status**: Complete

---

[📘 Full Notes](./notes.md) | [📋 Module README](./README.md) | [📚 Back to Course](../../README.md)