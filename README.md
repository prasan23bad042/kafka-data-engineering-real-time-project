# Kafka Real-Time Stock Market Data Pipeline

## Overview
This project demonstrates a **real-time data pipeline** that streams stock market data using **Apache Kafka**, processes the data with **Python**, and stores the streaming output in **Amazon S3** for further analytics using services such as **AWS Glue** and **Amazon Athena**.

The pipeline simulates real-time stock market data by continuously sending records from a dataset into a Kafka topic. A Kafka consumer then reads the streamed data and writes it into an S3 bucket in JSON format.

This project showcases the integration of distributed streaming platforms with cloud storage and analytics services.

---

## Architecture
```
Data Source 
     ↓
Kafka Producer 
     ↓
Kafka Topic 
     ↓
Kafka Consumer 
     ↓
Amazon S3 Storage
     ↓
AWS Glue Catalog
     ↓
Amazon Athena (SQL Queries)
```

---

## Workflow

1. Load stock market dataset using Python.
2. Send streaming data to Kafka topic using Kafka Producer.
3. Kafka Consumer subscribes to the topic.
4. Consumer reads each message in real time.
5. Messages are converted into JSON format.
6. JSON records are stored inside an Amazon S3 bucket.
7. AWS Glue catalogs the data.
8. Amazon Athena performs SQL queries on the stored data.

---

## Technologies Used

| Technology | Purpose |
|------------|---------|
| Python | Streaming scripts |
| Apache Kafka | Real-time streaming |
| kafka-python | Kafka Producer and Consumer |
| Amazon S3 | Data storage |
| AWS Glue | Data catalog |
| Amazon Athena | Query engine |
| Pandas | Data processing |

---

## Project Structure

```
kafka-stock-market-project
│
├── KafkaProducer.ipynb
├── KafkaConsumer.ipynb
│
├── data
│   └── indexProcessed.csv
│
└── README.md
```

---

## Kafka Producer

The **Kafka Producer** reads stock market data from a dataset and continuously publishes records to a Kafka topic.

### Producer Logic

```
1. Read CSV dataset using pandas
2. Randomly sample stock records
3. Convert records to JSON
4. Send records to Kafka topic
5. Repeat every second
```

---

## Kafka Consumer

The **Kafka Consumer** subscribes to the Kafka topic and processes incoming messages.

### Consumer Logic

```
1. Subscribe to Kafka topic
2. Receive streamed messages
3. Convert messages to JSON
4. Write JSON files to Amazon S3
5. Continue consuming data
```

---

## Required Python Libraries

Install dependencies before running the project.

```
pip install kafka-python
pip install pandas
pip install s3fs
```

---

## Kafka Topic Configuration

Example topic used in the project:

```
demo_testing2
```

---

## Running the Project

### Step 1 — Start Zookeeper

```
zookeeper-server-start.sh config/zookeeper.properties
```

### Step 2 — Start Kafka Server

```
kafka-server-start.sh config/server.properties
```

### Step 3 — Run Kafka Producer

```
python KafkaProducer.py
```

### Step 4 — Run Kafka Consumer

```
python KafkaConsumer.py
```

---

## S3 Storage Structure

```
s3://kafka-real-time-stock-market-project-prasanna/

stock_market_0.json
stock_market_1.json
stock_market_2.json
stock_market_3.json
...
```

Each file contains a single JSON record from the Kafka stream.

---

## Sample Output JSON

```
{
  "index": "NASDAQ",
  "open": 14532.21,
  "high": 14601.43,
  "low": 14487.12,
  "close": 14590.12,
  "volume": 1203400
}
```

---

## Data Analytics Layer

Data stored in S3 can be analyzed using:

- AWS Glue Data Catalog
- Amazon Athena
- Amazon QuickSight

SQL queries can be executed directly on the stored data.

Example Athena Query:

```
SELECT * 
FROM stock_market_table
LIMIT 10;
```

---

## Use Cases

```
Real-time financial analytics
IoT streaming pipelines
Application log monitoring
Fraud detection systems
Event-driven architectures
```

---

## Future Improvements

```
Use Kafka Connect for automated S3 ingestion
Store data in Parquet format
Integrate Apache Spark Streaming
Build dashboards using Amazon QuickSight
Implement schema registry for data validation
```

---

## Author

```
Prasanna Venkataraman S
```

---

## License

```
This project is intended for educational and learning purposes.
```
