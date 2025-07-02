# yt_mlops_capstone_project

Here's a beautifully structured and professional-looking `README.md` file based on your project details, aimed at impressing recruiters and technical reviewers:

---

# 🎬 IMDB Sentiment Analysis — End-to-End MLOps Project

🚀 **Production-grade ML pipeline for binary sentiment classification on IMDB reviews dataset**

![CI/CD](https://img.shields.io/github/actions/workflow/status/<your-username>/yt_mlops_capstone_project/ci.yaml?label=CI%2FCD)
![License](https://img.shields.io/github/license/<your-username>/yt_mlops_capstone_project)
![Docker Pulls](https://img.shields.io/docker/pulls/<your-docker-username>/capstone-app)

---

## 🧠 Project Overview

This project tackles the binary **sentiment classification** of movie reviews using the [IMDB dataset](https://ai.stanford.edu/~amaas/data/sentiment/). With **40,000 reviews**, we move from model experimentation to full-fledged **ML production deployment** using the complete **MLOps lifecycle**.

---

## 🧰 Tech Stack & Tools

| Category               | Tools & Frameworks                            |
| ---------------------- | --------------------------------------------- |
| Language & Frameworks  | Python, Flask, FastAPI (TODO)                 |
| Data Science & ML      | Scikit-learn, XGBoost, Word2Vec, SentenceBERT |
| Experiment Tracking    | MLFlow on [DagsHub](https://dagshub.com)      |
| Workflow Orchestration | DVC                                           |
| Deployment             | Docker, AWS ECR, EKS, CI/CD                   |
| Monitoring & Logging   | Prometheus, Grafana                           |
| Infrastructure as Code | eksctl, AWS CloudFormation                    |
| Testing                | Pytest, GitHub Actions                        |

---

## 🗂 Project Structure

```
yt_mlops_capstone_project/
│
├── data/                  # Raw and processed data
├── src/                   # Core modules (ingestion, preprocessing, model, etc.)
├── tests/                 # Test cases
├── scripts/               # CI/CD logic (model promotion, testing, etc.)
├── flask_app/             # API for model serving
├── .github/workflows/     # CI/CD configuration
├── dvc.yaml               # DVC pipeline definition
├── params.yaml            # Model/config parameters
└── Dockerfile             # Docker setup
```

---

## 🔬 Experimentation Highlights

| Experiment | Vectorizer      | Algorithms Tested                                | Outcome                               |
| ---------- | --------------- | ------------------------------------------------ | ------------------------------------- |
| EXP1       | CountVectorizer | Logistic Regression                              | Baseline Accuracy: **66%**            |
| EXP2       | BOW, TF-IDF     | LogisticRegression, MultinomialNB, XGBoost, etc. | Best: **TF-IDF + LogisticRegression** |
| EXP3       | TF-IDF          | Hyperparameter Tuning                            | ROC-AUC: **80%**                      |
| EXP4       | Word2Vec, SBERT | LogisticRegression                               | No better than TF-IDF                 |

> ✅ Final Model: **TF-IDF + LogisticRegression (max\_features=10,000)**
> 🎯 Metric: F1 Score (balanced dataset)

---

## 📦 Model Pipeline with DVC

* Modularized pipeline: `data_ingestion → preprocessing → feature_eng → model_building → evaluation → model_registration`
* Artifacts tracked: models, transformers, train/test splits
* Storage:

  * Local: `local_s3/`
  * Cloud: `AWS S3` with `DVC remote`

---

## 🔄 CI/CD Integration

* **GitHub Actions** triggered on `develop` merges
* Token-based auth with **DagsHub**
* Stages:

  1. Run tests
  2. Evaluate model performance
  3. Promote model if performance improves
  4. Docker build & push to **ECR**

---

## 🐳 Dockerized Flask API

```bash
# Build & run the app
docker build -t capstone-app:latest .
docker run -p 8888:5000 -e CAPSTONE_TEST=<your_key> capstone-app:latest
```

> ✅ Also tested via FastAPI (upcoming)

---

## ☁️ Cloud Deployment on AWS EKS

* **eksctl** used to spin up EKS cluster
* Exposes model via **LoadBalancer**
* CI/CD pipeline auto-deploys updated model containers
* Model can be queried via:

  ```bash
  curl http://<external-ip>:5000
  ```

---

## 📊 Monitoring with Prometheus + Grafana

* **Prometheus** scrapes Flask metrics (on port `5000`)
* **Grafana** visualizes model/server performance
* Deployed on separate EC2 instances

---

## 🧹 AWS Cleanup Checklist

* ✅ Delete EKS cluster
* ✅ Remove services, deployments, secrets
* ✅ Clean up ECR, S3, and CloudFormation stacks

---

## 🏗 Bonus: Understanding the Infrastructure

### How CloudFormation Ties In:

* `eksctl` uses **CloudFormation** to create:

  * EKS Control Plane Stack
  * EKS Node Group Stack
* Entire infra as code → **repeatable, auditable, versioned**

---

## 📦 Persistent Volume Claims (PVCs)

Kubernetes uses PVCs to allocate storage resources dynamically.

* Bound to `EBS` volumes on AWS
* Used when model/data need persistent state

---

## 👀 What's Next?

* ✅ Test FastAPI-based interface
* ✅ Add additional model benchmarking
* 🔜 Extend Grafana dashboard with custom app metrics
* 🔜 Add Prometheus exporters for system monitoring

---

## 🤝 Connect With Me

**Author:** \[Your Name]
**Email:** [your.email@example.com](mailto:your.email@example.com)
**LinkedIn:** [linkedin.com/in/your-profile](https://linkedin.com/in/your-profile)
**GitHub:** [github.com/your-username](https://github.com/your-username)

---

Let me know if you'd like a [**custom badge section**](f), or want the readme in a downloadable `.md` format too.
