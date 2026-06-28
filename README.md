# E-Commerce Big Data Analytics

A big data project that analyzes e-commerce data using MongoDB, HBase, and Apache Spark — each tool doing its designated task.

---

## The Idea

Instead of putting everything in one database, we split the data smartly:

- **HDFS** stores all raw files (~3.7GB of sessions, transactions, users, products)
- **Spark** reads from HDFS, cleans everything, and runs the analytics
- **MongoDB** stores business data (users, products, transactions) — great for complex queries
- **HBase** stores user sessions — perfect for time-series lookups by user and date
- **Python + Jupyter** ties it all together

---

## What's Inside

| File/Folder | What It Is |
|-------------|-----------|
| `ecommerce_spark_hbase_mongodb.ipynb` | Main notebook — runs everything from data loading to analytics |
| `dataset_generator.py` | Generates the synthetic e-commerce dataset |
| `hbase_schema.md` | HBase table designs and shell commands |
| `docker-compose.yml` | Starts HBase in Docker |
| `requirements.txt` | Python packages needed |
| `visualizations/dashboard.png` | 4-chart analytics dashboard |
| `results/` | CSV outputs from Spark SQL queries |

---

## How to Run It

**1. Install Python packages**
```bash
pip install -r requirements.txt
```

**2. Start everything**
```bash
# HDFS
%HADOOP_HOME%\sbin\start-dfs.cmd

# HBase (Docker)
docker start hbase-local
docker exec -d hbase-local hbase thrift start

# MongoDB
net start MongoDB
```

**3. Generate data**
```bash
python dataset_generator.py
```

**4. Upload to HDFS**
```bash
hdfs dfs -mkdir -p /ecommerce/sessions /ecommerce/transactions /ecommerce/users /ecommerce/products /ecommerce/categories
hdfs dfs -put data/users.json /ecommerce/users/
hdfs dfs -put data/products.json /ecommerce/products/
hdfs dfs -put data/categories.json /ecommerce/categories/
hdfs dfs -put data/transactions.json /ecommerce/transactions/
hdfs dfs -put data/sessions_*.json /ecommerce/sessions/
```

**5. Run the notebook**

Open `ecommerce_spark_hbase_mongodb.ipynb` in Jupyter and run all cells top to bottom.

---

## What the analysis indicates

- Top product made **$343,418** in revenue
- **44.7%** of shopping sessions end in cart abandonment — big recovery opportunity
- Search engine traffic converts best at **20.71%**
- Top customer has an estimated lifetime value of **$92,778**
- May 2026 was the peak month with **$160M** in revenue

---

## Note on Data Files

The `data/` folder is not included — the JSON files are too large for GitHub. Just run `dataset_generator.py` to reproduce them.
