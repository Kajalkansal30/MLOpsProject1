# Vehicle Data MLOps Project

A comprehensive MLOps project for vehicle data analysis, prediction, and deployment using MongoDB, AWS, and CI/CD pipeline.

## 🎯 Project Overview

This project implements a complete machine learning pipeline for vehicle data processing, including:
- Data ingestion from MongoDB
- Data validation and transformation
- Model training and evaluation
- Model deployment with AWS S3 integration
- CI/CD pipeline with Docker and GitHub Actions
- Web application for predictions

## 🏗️ Architecture

```
├── src/
│   ├── components/          # ML pipeline components
│   ├── configuration/       # AWS & MongoDB connections
│   ├── entity/             # Configuration & artifact entities
│   ├── cloud_storage/      # AWS S3 operations
│   ├── pipeline/           # Training & prediction pipelines
│   └── utils/              # Utility functions
├── config/                 # Configuration files
├── notebook/              # Jupyter notebooks for EDA
├── static/                # Web assets
├── templates/             # HTML templates
└── .github/workflows/     # CI/CD configuration
```

## 🚀 Quick Start

### 1. Project Setup

```bash
# Create project structure
python template.py

# Setup local package installation
pip install -e .

# Install dependencies
pip install -r requirements.txt
```

### 2. MongoDB Setup

1. Sign up at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new project and cluster (M0 free tier)
3. Create database user and set network access to `0.0.0.0/0`
4. Get connection string and set environment variable:

**Linux/Mac:**
```bash
export MONGODB_URL="mongodb+srv://<username>:<password>@cluster.mongodb.net/"
```

**Windows (PowerShell):**
```powershell
$env:MONGODB_URL = "mongodb+srv://<username>:<password>@cluster.mongodb.net/"
```

**Windows (Command):**
```cmd
set MONGODB_URL=mongodb+srv://<username>:<password>@cluster.mongodb.net/
```

### 3. Data Setup

1. Add your dataset to the `notebook/` directory
2. Use `mongoDB_demo.ipynb` to push data to MongoDB
3. Verify data in MongoDB Atlas: Database → Browse Collections

### 4. Environment Configuration

Create a `.env` file or set environment variables:

```bash
# MongoDB
MONGODB_URL=mongodb+srv://<username>:<password>@cluster.mongodb.net/

# AWS (for model storage)
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_DEFAULT_REGION=us-east-1
```

## 🔧 Development Workflow

### Phase 1: Core Components

1. **Logging & Exception Handling**
   - Logger setup in `src/logger/`
   - Exception handling in `src/exception/`
   - Test with `demo.py`

2. **Data Ingestion**
   - Configure MongoDB connection
   - Setup data validation schema
   - Implement data ingestion pipeline

3. **Data Validation**
   - Define schema in `config/schema.yaml`
   - Implement validation component
   - Generate validation reports

4. **Data Transformation**
   - Feature engineering pipeline
   - Data preprocessing utilities
   - Train-test split implementation

5. **Model Training**
   - Model selection and training
   - Hyperparameter tuning
   - Model evaluation metrics

### Phase 2: AWS Integration

1. **AWS Setup**
   - Create AWS account and IAM user
   - Set up S3 bucket for model storage
   - Configure AWS credentials

2. **Model Storage**
   - Implement S3 storage operations
   - Model versioning system
   - Automated model pushing

### Phase 3: Deployment

1. **Web Application**
   - Flask app setup (`app.py`)
   - Frontend templates (`templates/`)
   - Static assets (`static/`)

2. **Docker Configuration**
   ```bash
   # Build Docker image
   docker build -t vehicle-prediction-app .

   # Run container
   docker run -p 5000:5000 vehicle-prediction-app
   ```

3. **CI/CD Pipeline**
   - GitHub Actions workflow
   - Automated testing and deployment
   - AWS EC2 integration

## 📊 Usage

### Training Pipeline
```bash
# Run complete training pipeline
python -m src.pipeline.training_pipeline

# Or run specific components
python src/components/data_ingestion.py
python src/components/data_validation.py
python src/components/model_trainer.py
```

### Prediction Pipeline
```bash
# Start web application
python app.py

# Access application
# Open browser: http://localhost:5000
```

### API Endpoints
- `GET /` - Home page with prediction form
- `POST /predict` - Get predictions
- `GET /training` - Trigger model training

## 🧪 Testing

```bash
# Run tests
python test.py

# Check model performance
python src/components/model_evaluation.py
```

## 📁 Project Structure

```
vehicle-mlops-project/
├── src/
│   ├── components/
│   │   ├── __init__.py
│   │   ├── data_ingestion.py
│   │   ├── data_validation.py
│   │   ├── data_transformation.py
│   │   ├── model_trainer.py
│   │   └── model_evaluation.py
│   ├── configuration/
│   │   ├── __init__.py
│   │   └── aws_connection.py
│   ├── entity/
│   │   ├── __init__.py
│   │   ├── config_entity.py
│   │   ├── artifact_entity.py
│   │   ├── estimator.py
│   │   └── s3_estimator.py
│   ├── cloud_storage/
│   │   ├── __init__.py
│   │   └── aws_storage.py
│   ├── pipeline/
│   │   ├── __init__.py
│   │   ├── training_pipeline.py
│   │   └── prediction_pipeline.py
│   ├── utils/
│   │   ├── __init__.py
│   │   └── main_utils.py
│   ├── logger/
│   │   └── __init__.py
│   └── exception/
│       └── __init__.py
├── config/
│   ├── model.yaml
│   └── schema.yaml
├── notebook/
│   ├── data.csv
│   ├── exp-notebook.ipynb
│   └── mongoDB_demo.ipynb
├── templates/
│   └── vehicledata.html
├── static/
│   ├── style.css
├── .github/
│   └── workflows/
│       └── aws.yaml
├── Dockerfile
├── requirements.txt
├── setup.py
└── README.md
```

## 🔧 Configuration Files

### config/model.yaml
Model configuration including:
- Model parameters
- Training hyperparameters
- Evaluation metrics

### config/schema.yaml
Data schema definition:
- Column names and data types
- Validation rules
- Required fields

## 🚀 Deployment

### AWS EC2 Deployment

1. **Launch EC2 Instance**
   - AMI: Ubuntu Server 24.04
   - Instance Type: t2.medium
   - Security Group: Allow HTTP (80), HTTPS (443), Custom TCP (5000)

2. **Connect to EC2**
   ```bash
   ssh -i "your-key.pem" ubuntu@ec2-public-ip
   ```

3. **Install Docker**
   ```bash
   sudo apt-get update -y
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh get-docker.sh
   sudo usermod -aG docker ubuntu
   newgrp docker
   ```

4. **Run Application**
   ```bash
   docker pull your-ecr-repo/vehicleproj:latest
   docker run -d -p 80:5000 your-ecr-repo/vehicleproj:latest
   ```

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For support, email support@vehiclemlops.com or create an issue in the GitHub repository.

## 🙏 Acknowledgments

- MongoDB Atlas for database hosting
- AWS for cloud infrastructure
- Open source ML libraries and frameworks
- Contributors and maintainers
