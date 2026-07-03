# Enterprise NLP Pipeline: Multi-Cloud Chatbot & Sentiment Architecture

## 1. Project Overview & Business Impact
This project focuses on resolving critical customer support scalability bottlenecks. By engineering an end-to-end NLP automation pipeline, the system safely deflects high-volume, repetitive inquiries while maintaining an intelligent, real-time fallback mechanism for human agents.

### Key Business Results
* **Annual Cost Savings:** $5.1M
* **Average Response Time:** Reduced from **9.4 minutes** to **2.8 minutes**
* **Customer Satisfaction (CSAT):** Increased from **71%** to **93%**
* **Ticket Escalation Rate:** Dropped from **42%** to **14%**
* **Human Agent Utilization:** Shifted from an overworked **100%** down to a sustainable **54%**

---

## 2. Data Strategy & Preprocessing
The model architecture is built upon a multimodal training corpus consisting of **9.36 million total records**:
* **Chat Transcripts:** 5.8 Million
* **Email Support Logs:** 2.1 Million
* **CRM Database Entries:** 1.4 Million
* **Product Catalog Items:** 68,000
* **Knowledge Base Articles:** 14,300

### Data Pipeline Architecture
To prepare text bodies safely and uniformly for transformer ingestion, data passes through the following pipeline:

[Raw Data Ingestion]
│
▼
[Drop Duplicates] ──► df.drop_duplicates()
│
▼
[PII Masking & Language Detection]
│
▼
[Tokenization, Stop-Word Removal, Lemmatization] ──► df["text"] = preprocess(df["text"])
│
▼
[Data Splitting] ──► train, test = train_test_split(df, test_size=0.20)

---

## 3. Feature Engineering & Model Selection
Beyond the raw text bodies, the feature matrix incorporates structured behavioral and contextual attributes to optimize classification performance:
* **Text Signatures:** Message length, Product category, Previous sentiment score.
* **Metadata & Context:** Customer tenure, Purchase history, Previous ticket counts, Time of day, Device type.

### Model Evaluation Matrix
Multiple classification architectures were tested on core intent recognition accuracy. A fine-tuned **BERT Transformer** yielded the highest accuracy and was selected for production:

| Model Hierarchy | Intent Classification Accuracy | Status |
| :--- | :--- | :--- |
| **BERT Transformer** | **96.4%** | **Selected / Deployed** |
| DistilBERT | 95.9% | Evaluated |
| XGBoost | 92.8% | Evaluated |
| Random Forest | 89.1% | Evaluated |
| Logistic Regression | 82.4% | Baseline |

---

## 4. Production Workflow & Multitask Inference
The live production runtime utilizes a dual-engine workflow: an execution block handles intent and entity parsing, while a secondary head processes a **5-class sentiment analyzer** (Positive, Neutral, Negative, Frustrated, Escalation Risk).
[Customer Input Message]
│
▼
[Intent & Entity Recognition]
│
▼
[Knowledge Search & Base Response]
│
▼
[Real-Time Sentiment Analysis]
│
▼
Is Confidence > 95%?
├── YES ──► Automatically Dispatch Reply
└── NO  ──► Hot-Route to Human Agent

---

## 5. Enterprise Cloud Architecture
The system relies on a high-availability, multi-cloud strategy designed for sub-second inference latencies and deep executive visualization:

* **Inference Engine:** Handled via **Azure App Service** and **Azure ML**, deploying the frozen **TensorFlow** model graph inside optimized container runtimes.
* **Analytics Backend:** Downstream execution telemetry is fed into **Google Vertex AI** and streamed directly into a **BigQuery** warehouse.
* **Executive Visualization:** A live **Power BI Dashboard** queries BigQuery to reflect operational KPIs, model drift, and CSAT metrics dynamically.

---

## 6. Model Evaluation Profile
Evaluated against the 20% validation split, the final model achieved exceptional generalization characteristics:

* **Precision:** 96.8%
* **Recall:** 95.9%
* **F1-Score:** 96.3%
* **ROC AUC:** 0.991

---

## 7. Production Deployment & MLOps Checklist
The system is built on modern cloud-native standards to ensure reliability, zero-downtime updates, and automated lifecycle management:

* [x] **Core Stack:** Python, TensorFlow, Azure Machine Learning, Google Vertex AI
* [x] **Containerization & Orchestration:** Docker, Kubernetes
* [x] **CI/CD & Governance:** Enterprise Git Pipelines, MLflow Model Registry
* [x] **Monitoring & Reliability:** Prometheus Metrics, Grafana Dashboards, Automated Drift Detection, Regular Retraining Loops
* [x] **Deployment Strategies:** Canary Deployments, Automated Rollbacks, Real-Time A/B Testing Frameworks
* [ ] 
