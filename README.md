

# 🚗 Vehicle Detection MLOps Project

Welcome to the **Vehicle Detection MLOps Project**, a full-stack, end-to-end machine learning project architected with MLOps best practices. This project showcases the integration of robust data pipelines, MongoDB, AWS services, CI/CD, Docker, and deployment on EC2—all production-ready and optimized for scaling.

---

## 📁 Project Structure

```
vehicle-mlops-project/
│
├── src/                        # Core ML codebase
├── notebook/                   # EDA and MongoDB notebooks
├── templates/                  # Frontend HTML files
├── static/                     # CSS, JS files for UI
├── .github/workflows/          # GitHub Actions for CI/CD
├── setup.py                    # Local package setup
├── pyproject.toml              # Build system config
├── requirements.txt            # Python dependencies
├── dockerfile                  # Docker image build file
├── app.py                      # FastAPI/Flask app entrypoint
├── README.md                   # You’re here!
└── ...
```

---

## 🚀 Project Highlights

### ✅ Local Setup & Development

1. **Create Project Template**:  
   Run `template.py` to auto-generate the folder structure.

2. **Package Configuration**:  
   `setup.py` and `pyproject.toml` enable importing local modules across components.

3. **Environment Setup**:
   ```bash
   conda create -n vehicle python=3.10 -y
   conda activate vehicle
   pip install -r requirements.txt
   pip list  # Verify local packages
   ```

---

## ☁️ MongoDB Atlas Integration

1. Set up MongoDB Atlas, create cluster & user, and whitelist IP `0.0.0.0/0`.
2. Obtain your **connection string** and set environment variable:
   ```bash
   export MONGODB_URL="mongodb+srv://<username>:<password>@cluster.mongodb.net"
   ```

3. Ingest data from notebook into MongoDB Atlas and verify from MongoDB UI.

---

## 🧠 ML Pipeline Components

Each module follows a clean separation of concerns and is fully testable.

- **Logging & Exception Handling**  
  - Centralized logging with `logger.py` and custom error classes in `exception.py`.

- **Data Ingestion**  
  - Pulls structured data from MongoDB and stores it as a DataFrame.
  - Defined via `DataIngestionConfig` and `DataIngestionArtifact`.

- **Data Validation**  
  - Utilizes schema from `config/schema.yaml` for robust checks.

- **Data Transformation**  
  - Feature engineering and transformation pipelines using custom estimators.

- **Model Training**  
  - Encapsulated in `ModelTrainerConfig` and `ModelTrainerArtifact`.

---

## ☁️ AWS Integration

- **IAM Setup**  
  Created users with `AdministratorAccess`, managed via secure environment variables.

- **S3 Buckets**  
  Used to store model artifacts:
  - `MODEL_BUCKET_NAME = "my-model-mlopsproj"`
  - `MODEL_PUSHER_S3_KEY = "model-registry"`

- **AWS S3 Access**  
  Fully integrated using `boto3` in `aws_connection.py` and `s3_estimator.py`.

---

## 🧪 Model Evaluation & Deployment

- Model evaluation checks if performance improvement > `0.02`
- Model is pushed to S3 if evaluation passes
- Supports retraining and pushing updated versions

---

## 🌐 Prediction Pipeline

- `app.py` serves as the main API using Flask/FastAPI
- Routes:
  - `/` – UI to upload image/data
  - `/predict` – Returns prediction
  - `/train` – Triggers model training

---

## 🔁 CI/CD with GitHub Actions & AWS

### Setup

- **Dockerized Project**
- **Self-hosted GitHub Runner on EC2**
- **CI/CD Pipeline**
  - On every commit: Docker image is built → pushed to ECR → deployed to EC2

### GitHub Secrets
| Key | Purpose |
|-----|---------|
| `AWS_ACCESS_KEY_ID` | IAM user key |
| `AWS_SECRET_ACCESS_KEY` | IAM secret |
| `AWS_DEFAULT_REGION` | AWS region (us-east-1) |
| `ECR_REPO` | ECR repo URI |

---

## 🌍 EC2 Deployment

1. **Instance Setup**
   - Ubuntu 24.04 | T2 Medium | 30 GB storage
   - Docker installed
   - Port 5080 opened for traffic

2. **App Access**  
   Visit:
   ```
   http://<EC2_PUBLIC_IP>:5080
   ```

---

## 🛠️ Tools & Technologies

| Category | Stack |
|---------|-------|
| Language | Python |
| ML Framework | Scikit-learn |
| DB | MongoDB Atlas |
| Cloud | AWS (S3, IAM, EC2, ECR) |
| Orchestration | GitHub Actions |
| Containerization | Docker |
| Deployment | EC2 |
| Web | Flask/FastAPI |
| DevOps | CI/CD, Self-hosted runner |

---

## 💡 Future Enhancements

- Model versioning with MLflow
- Automated monitoring with Prometheus + Grafana
- Drift detection and scheduled retraining

---

## 👏 Contributing

Pull requests are welcome. For major changes, please open an issue first.

---

