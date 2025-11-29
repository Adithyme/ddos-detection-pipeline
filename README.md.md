&nbsp;**A Scalable Big Data Pipeline for DDoS Attack Detection Enhanced with Temporal and Forensic Traffic Analysis**



This project builds a scalable Big Data pipeline using Apache Spark + XGBoost to detect multiple types of DDoS attacks (ICMP Flood, ICMP Fragmentation, ACK Fragmentation, Benign) on very large network traffic logs (3.3M+ rows).

It also includes Forensic Analysis (source IP, destination IP, ports, timestamps, probability scores) and Temporal Analysis (hourly, daily, behavioral attack patterns).



⭐ 1. Project Overview



Modern networks generate massive volumes of traffic that cannot be analyzed using normal tools.

This project introduces a Spark-powered ML pipeline that:



✔ Preprocesses 3.3M+ IoT DDoS flows

✔ Builds a scalable ML workflow

✔ Trains a distributed XGBoost classifier

✔ Extracts forensic insights for analysts

✔ Performs temporal (time-based) attack pattern analysis

✔ Produces interpretable predictions with probability scores



The system is fully containerized using Docker, ensuring easy reproducibility and portability.



⭐ 2. Dataset



Dataset: CIC IoT-DDoS 2024

Source: Canadian Institute for Cybersecurity (CIC)

Size: 3,371,424 rows × 84 columns

Year: 2024



Includes:



Multiple IoT-based attack categories



Rich flow-based features (packet lengths, IATs, flags, header sizes)



Benign vs Malicious traffic



⭐ 3. System Architecture

Raw CSV → Spark Data Preprocessing → Feature Engineering → Distributed XGBoost

&nbsp;           ↓                                         ↓

&nbsp;      Forensic Insights                        Temporal Analysis

&nbsp;           ↓                                         ↓

&nbsp;                    Final Predictions + Visual Reports



⭐ 4. Features of the Pipeline

🔹 Big Data Preprocessing (Spark)



Handles 3.3 million rows efficiently



Normalizes column names



Casts 84 columns into usable numeric formats



Fixes missing values



Balances imbalanced classes using computed class weights



🔹 ML Classification (XGBoost-Spark)



Predicts 4 classes:



Class	Meaning

ICMP Flood	High-volume ping flooding

ICMP Fragmentation	Broken packet fragments

ACK Fragmentation	TCP ACK-based fragmented abuse

Benign	Normal traffic



Performance:

Accuracy: 89.15%

&nbsp;F1-Score: 89.71%



🔹 Forensic Analysis



For each predicted flow, system extracts:



Source IP



Destination IP



Ports



Timestamp



Probability scores (sorted)



Useful for SOC teams to identify attack origin, target, and intensity.



🔹 Temporal Analysis



Finds patterns such as:



Peak attack hours



Day-wise trends



Time-of-day behavior



Burst periods



⭐ 5. Project Folder Structure

📂 ddos-detection-pipeline/

│── 📁 notebooks/

│     ├── preprocessing.ipynb

│     ├── model\_training.ipynb

│     └── forensic\_temporal\_analysis.ipynb

│

│── 📁 src/

│     ├── pipeline.py

│     ├── preprocessing.py

│     ├── temporal\_analysis.py

│     └── forensic\_analysis.py

│

│── 📁 models/

│     └── xgboost\_model/

│

│── 📁 sample\_data/

│     └── sample\_5000\_rows.csv

│

│── Dockerfile

│── requirements.txt

│── README.md

&nbsp;6. Installation \& Running

🔧 1. Clone the repository

git clone https://github.com/Adithyme/ddos-detection-pipeline.git

cd ddos-detection-pipeline



🐳 2. Build Docker Image

docker build -t ddos-pipeline .



▶ 3. Run the Container

docker run -it ddos-pipeline



▶ 4. Launch Jupyter Notebook



Inside the container:



jupyter notebook --ip=0.0.0.0 --allow-root



⭐ 7. Results

✔ Model Performance

Metric	Value

Accuracy	89.15%

Precision	88.9%

Recall	89.4%

F1-Score	89.71%

✔ Insights Obtained



Attackers heavily targeted broadcast address 255.255.255.255



Ports such as 67 (DHCP) were suspiciously hit



Attacks peaked during specific hours—showing clear patterns



Forensic logs helped map attacker strategy



&nbsp;8. Limitations



Works only in batch mode, no real-time detection



Detects only 4 attack types



Depends on pre-engineered dataset features



No integration with real firewalls/SIEM yet



9\. Future Work



Add Spark Streaming / Kafka for real-time detection



Expand to more attack types (SYN Flood, UDP Flood, Slowloris)



Integrate with SOC tools (firewalls, routers, SIEM)



Add hybrid ML models (XGBoost + LSTM)



10\. License



No License



11\. Author



Adithya CH

