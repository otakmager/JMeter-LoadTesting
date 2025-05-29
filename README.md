# 📊 JMeter-LoadTesting

This project implements load and performance testing using **Apache JMeter 5.6.3**, targeting the [`https://jsonplaceholder.typicode.com/posts`](https://jsonplaceholder.typicode.com/posts) API. The scenarios simulate multiple users accessing and submitting data to test system behavior under concurrent load.

> ✅ Target URL: [https://jsonplaceholder.typicode.com/posts](https://jsonplaceholder.typicode.com/posts)  
> 📦 GitHub Repo: [https://github.com/otakmager/JMeter-LoadTesting](https://github.com/otakmager/JMeter-LoadTesting)

---

## 🧱 Project Structure

```
JMeter-LoadTesting/
├── jsonplaceholder_post_test.jmx    # JMX files for test plans
├── data.csv                         # Test datasets
├── results.csv                      # Generated CSV reports
├── html-report/                     # Generated HTML reports
│   └── index.html
└── README.md                        # Project documentation
```

---

## 📋 Test Scenarios

### 🧵 Thread Group 1: TG_GET_All_Posts

**Endpoint:** `GET /posts`

Simulates multiple users retrieving the full list of posts. This mimics homepage or list-view access.

- 👥 10 users
- ⏱ Duration: 1 minute
- 🔁 Loop: Forever (until test ends)

**Assertions:**
- ✅ Status code must be `200`
- ⏱ Response time under **5000 ms**

---

### 🧵 Thread Group 2: TG_GET_Post_By_ID

**Endpoint:** `GET /posts/{id}`

Focuses on retrieving individual post details. Each user accesses a random post.

- 👥 10 users
- ⏱ Duration: 1 minute
- 🔁 Loop: Forever (until test ends)
- 🎲 Random post ID

**Assertions:**
- ✅ Status code must be `200`
- ⏱ Response time under **5000 ms**

---

### 🧵 Thread Group 3: TG_POST_Create_Post

**Endpoint:** `POST /posts`

Tests the performance of post creation using CSV-based test data.

- 👥 10 users
- ⏱ Duration: 1 minute
- 📄 Data file: [`data.csv`](https://github.com/otakmager/JMeter-LoadTesting/blob/main/data.csv)
- 🔁 Each user submits multiple entries from the CSV

**Assertions:**
- ✅ Status code must be `201`
- ⏱ Response time under **5000 ms**

---

## 📦 Test Data & Result Artifacts

| File | Description |
|------|-------------|
| [`data.csv`](https://github.com/otakmager/JMeter-LoadTesting/blob/main/data.csv) | Input for `POST /posts` test |
| [`results.csv`](https://github.com/otakmager/JMeter-LoadTesting/blob/main/results.csv) | Raw CLI test result (from `-l` flag) |
| [`html-report/`](https://github.com/otakmager/JMeter-LoadTesting/tree/main/html-report) | Generated HTML summary report |

---

## 🌐 Test Environment Context

The JMeter test was conducted under the following conditions:

- Time: Around 10:00 AM (local time)
- Location: Rural area, Central Java, Indonesia
- Connection Type:
  - Wi-Fi at home (laptop connected via local router)
  - Provided by a local RT/RW Net (community-based ISP)
  - The router is connected to an antenna that wirelessly receives internet from a remote transmitter (~2–3 km away)
  - No direct fiber or wired connection to the main ISP backbone
- Network Conditions:
  - Ping highly unstable: fluctuated between ~40 ms to >4000 ms
  - Occasional timeouts during the test

> ⚠️ Note: Due to the unstable and wireless nature of the connection, performance test results may vary significantly compared to tests on stable wired networks.

---

## 🚀 How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/otakmager/JMeter-LoadTesting.git
cd JMeter-LoadTesting
```

### 2. Launch JMeter GUI (optional, for editing/viewing the test plan

> 📂 Open the jsonplaceholder_post_test.jmx file from the GUI to view or modify the test plan.

### 3. Run the Test in CLI Mode (recommended)

> ⚠️ Note: Make sure to delete or rename results.csv and html-report/ before re-running the test.
JMeter will fail to execute if these output files/folders already exist.

You can run the test from the JMeter bin folder like this:
```bash
cd pathToJMeter/bin
jmeter -n -t pathToProject/jsonplaceholder_post_test.jmx -l pathToProject/result.csv -e -o pathToProject/html-report
```

Replace:
- pathToJMeter → with the full path to your JMeter installation (e.g., E:/Program/apache-jmeter-5.6.3)
- pathToProject → with the full path to this cloned project folder (e.g., E:/Project/JMeter-LoadTesting)

### 4. View Test Results
> Open the generated html-report/index.html file in your browser to view the visual results.

---

## 📊 Test Result Summary

### 🔹 General Stats

- **Total Requests:** 8419
- **Successful Requests:** 8419 (100%)
- **Failed Requests:** 0
- **Average Response Time:** ~206 ms
- **Min / Max Response Time:** 39 ms / 3911 ms
- **HTTP Response Codes:**
  - `200 OK`: 6803
  - `201 Created`: 1616

### 🔹 By Thread Group (Based on [`statistics.json`](https://github.com/otakmager/JMeter-LoadTesting/blob/main/html-report/statistics.json))

| Transaction        | Requests | Avg Time (ms) | 90th pct (ms) | Max Time (ms) | Errors | Throughput (req/sec) |
|--------------------|----------|----------------|----------------|---------------|--------|-----------------------|
| GET Post List      | 1282     | 464.12         | 815.0          | 2917.0        | 0      | 21.34                 |
| GET Post By ID     | 5521     | 106.43         | 366.0          | 3911.0        | 0      | 92.75                 |
| POST Create Post   | 1616     | 340.31         | 591.0          | 3893.0        | 0      | 27.07                 |
| **Total**          | 8419     | 205.79         | 563.0          | 3911.0        | 0      | 140.17                |

> ✅ All scenarios passed with zero errors and all assertions met successfully.

---

## 🔧 Technologies Used

- Apache JMeter 5.6.3
- Java 17
- JSONPlaceholder API

---
