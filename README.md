
---

# 🎬 IMDB Sentiment Classification — MLOps Capstone Project

This project leverages the **IMDB Movie Review dataset (\~40k reviews)** to build a **production-ready, end-to-end Sentiment Analysis system**. The aim is to apply **MLOps best practices** to create a **reliable, automated, and scalable pipeline** from data ingestion to deployment on Kubernetes — complete with CI/CD, monitoring, and model retraining.

---

## 🧠 Project Objective

* ✨ End-to-end **ML pipeline** (ingestion ➝ preprocessing ➝ modeling ➝ evaluation ➝ registry ➝ retraining)
* 📦 **Code & data versioning** using Git + DVC
* ☁️ **Data ingestion to AWS S3**
* ⚙️ **ML experiment tracking** with MLflow via Dagshub
* 🧪 **Model retraining & promotion**
* 🚀 **CI/CD** pipeline with GitHub Actions
* 🐳 **Containerized deployment** with Docker → ECR → EKS (Kubernetes)
* 📊 **Monitoring & alerting** using Prometheus & Grafana

---

## 📁 Project Structure

```
yt_mlops_capstone_project/
│
├── .github/workflows/         # CI/CD pipelines
├── data_s3/                   # Versioned raw/interim/processed datasets
├── flask_app/                 # REST API with Prometheus instrumentation
├── src/                       # All pipeline stages (modular)
│   ├── data_ingestion.py
│   ├── data_preprocessing.py
│   ├── feature_engineering.py
│   ├── model_building.py
│   ├── model_evaluation.py
│   ├── register_model.py
├── tests/                     # Unit tests
├── scripts/                   # Model promotion scripts
├── dvc.yaml                   # DVC pipeline definition
├── params.yaml                # Parameter config
├── Dockerfile
└── requirements.txt
```

---

## 🚀 ML Pipeline Stages

> Built using Python modules with **DVC** for orchestration.

1. **Data Ingestion**

   * Load from local or AWS S3
   * Train-test split
2. **Data Preprocessing**

   * Clean text: URLs, punctuation, lowercase, lemmatization, stopwords
3. **Feature Engineering**

   * Vectorization using BoW/TF-IDF/Word2Vec/Sentence-BERT
   * Save vectorizer
4. **Model Building**

   * Trained various classifiers (Logistic Regression, NB, XGBoost, RF, GB)
   * Best model: **TF-IDF + Logistic Regression**
5. **Model Evaluation**

   * Metrics: Accuracy, Precision, Recall, F1, ROC-AUC
   * Tracked on MLflow via Dagshub
6. **Model Registry**

   * Register best models in **MLflow Registry**
7. **Model Retraining**

   * Triggered based on performance thresholds
8. **Model Serving**

   * Flask API (Dockerized)
   * Deployable on EKS
   * Metrics exposed to Prometheus

---

## 📊 Model Experiments

| Experiment | Vectorizer        | Model              | ROC-AUC  | F1 Score |
| ---------- | ----------------- | ------------------ | -------- | -------- |
| Exp 1      | CountVectorizer   | LogisticRegression | 0.70     | 0.65     |
| Exp 2      | TF-IDF            | LogisticRegression | **0.80** | **0.78** |
| Exp 3      | TF-IDF + HPTuning | LogisticRegression | 0.82     | 0.80     |
| Exp 4      | Word2Vec/SBERT    | LogisticRegression | 0.76     | 0.74     |

✅ Final Model: **TF-IDF + Logistic Regression (10k max features)**

---

## 🧪 CI/CD Pipeline

> CI/CD implemented with **GitHub Actions**, broken into **multi-job stages**.

* 🧼 Code linting & testing
* 🧪 Unit test (including Flask & model thresholds)
* 🛠️ Build & push Docker image to **AWS ECR**
* 🚀 Deploy app to **EKS (via Kubernetes YAML)**
* 🔁 Automatically promote better models from *staging* ➝ *production*

---

## ☁️ Cloud Architecture

* 🧊 **AWS S3**: Data storage & DVC remote
* 🔐 **IAM User**: For programmatic access
* 🐳 **Docker**: App containerization
* 🧰 **ECR**: Docker image repository
* ☸️ **EKS**: App deployment via Kubernetes
* 📈 **Prometheus**: Monitors app metrics
* 📊 **Grafana**: Dashboards for real-time alerts

---

## 🔬 Monitoring Setup

**Prometheus**

* Deployed on separate EC2
* Scrapes metrics from Flask API (via `/metrics`)
* Tracks latency, request count, prediction count

**Grafana**

* Visual dashboards from Prometheus datasource
* Real-time monitoring of app performance

---

## 🧪 Testing Suite

| Test Module         | Description                                             |
| ------------------- | ------------------------------------------------------- |
| `test_model.py`     | Validate model metrics vs current production threshold  |
| `test_flask_app.py` | Check API endpoints and prediction logic                |
| `promote_model.py`  | Promote new model to production if performance improves |

---

## 💻 Deployment Modes

| Mode       | Command                                                            |
| ---------- | ------------------------------------------------------------------ |
| Local      | `python app.py`                                                    |
| Docker     | `docker run -p 8888:5000 -e CAPSTONE_TEST=xyz capstone-app:latest` |
| ECR + EKS  | GitHub Actions CI/CD auto-deploy via `deployment.yaml`             |
| Prometheus | Hosted on EC2, port `9090`                                         |
| Grafana    | Hosted on EC2, port `3000`                                         |

---

## 🧰 Tools & Technologies Used

* **ML Frameworks**: scikit-learn, XGBoost
* **Pipeline Automation**: DVC, GitHub Actions
* **Experiment Tracking**: MLflow + Dagshub
* **Data Storage**: AWS S3
* **Model Registry**: MLflow
* **Containerization**: Docker
* **Cloud Deployment**: AWS ECR, EKS
* **Monitoring**: Prometheus, Grafana
* **CI/CD**: GitHub Actions, DockerHub (optional)

---
