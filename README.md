# ride-sharing-spark-streaming
Spark structured streaming example
# 🚖 Ride-Sharing Platform Analytics Using Apache Spark Structured Streaming

This project analyzes real-time ride-sharing data using **Apache Spark Structured Streaming**. It simulates a ride-sharing platform where trip data is ingested over a socket stream and processed in real time to perform analytics such as total fare computation and driver-wise aggregations.

---

## 📁 Project Structure

ride-sharing-analytics-spark-streaming/ ├── task1_ingest_json.py # Ingest JSON data from socket and print to console ├── task2_driver_aggregates.py # Real-time aggregation by driver_id ├── task3_windowed.py # Windowed aggregation for fare totals ├── output/ │ └── task1/ # Output from Task 1 (console) │ └── task2/ # Output from Task 2 (CSV) │ └── task3/ # Output from Task 3 (CSV) ├── README.md

yaml
Copy
Edit

---

## 🚀 Technologies Used

- Apache Spark 3.5.0
- PySpark
- Structured Streaming
- Python 3.8+
- Netcat (`nc`) for socket input
- Docker (optional for Spark cluster setup)
- Git & GitHub

---

## 📝 Dataset Schema (Example Input)

Each line ingested over the socket should be a JSON string with the following fields:

```json
{
  "trip_id": "t001",
  "driver_id": "d1",
  "distance_km": 4.5,
  "fare_amount": 8.0,
  "timestamp": "2025-04-02T19:54:00"
}
📌 Task Descriptions
✅ Task 1: Real-Time JSON Ingestion
Reads JSON lines from socket (port 9999).

Parses and prints the streaming data to the console.

Useful for testing the socket source and schema validation.

✅ Task 2: Driver-wise Aggregation
Groups by driver_id in real time.

Calculates total distance and total fare for each driver.

Writes output to CSV files in output/task2/.

✅ Task 3: Window-Based Fare Aggregation
Performs sliding window aggregations on fare_amount.

Uses a 5-minute window with 2-minute sliding interval.

Computes total fare across time windows.

Writes results to output/task3/.

🔧 How to Run
Step 1: Start the Socket Server
Open a terminal and run:

bash
Copy
Edit
nc -lk 9999
You can now paste JSON records line-by-line (or stream from a script).

Step 2: Submit Spark Jobs
In a separate terminal, run any task like so:

bash
Copy
Edit
spark-submit task1_ingest_json.py
spark-submit task2_driver_aggregates.py
spark-submit task3_windowed.py
💡 Ensure that the timestamp field is in ISO 8601 format (yyyy-MM-ddTHH:mm:ss).

📂 Output Files
CSV files will be created under:

output/task2/ → For driver-wise aggregates

output/task3/ → For windowed fare totals

Use cat output/task2/part-*.csv to view results.

🧪 Sample Input for Testing
json
Copy
Edit
{"trip_id":"t001", "driver_id":"d1", "distance_km":4.5, "fare_amount":8.0, "timestamp":"2025-04-02T19:54:00"}
{"trip_id":"t002", "driver_id":"d2", "distance_km":5.2, "fare_amount":9.5, "timestamp":"2025-04-02T19:54:30"}
