# 🎯 Customer Data Platform (CDP) - Deployment Guide

A production-ready Customer Data Platform for predicting customer churn and lifetime value using machine learning.

## 📋 Table of Contents
- [Features](#features)
- [Project Structure](#project-structure)
- [Local Setup](#local-setup)
- [Docker Deployment](#docker-deployment)
- [Cloud Deployment Options](#cloud-deployment-options)
- [Usage](#usage)
- [Tech Stack](#tech-stack)

---

## ✨ Features

- **Churn Prediction**: Predict customer churn using ML models (Logistic Regression, Random Forest, SVC)
- **CLV Prediction**: Estimate Customer Lifetime Value using Gamma-Gamma model
- **Interactive Dashboard**: User-friendly Streamlit interface
- **Data Visualization**: Real-time charts and analytics
- **Docker Support**: Containerized for easy deployment
- **Scalable**: Ready for cloud deployment

---

## 📁 Project Structure

```
customer-data-platform/
│
├── app.py                          # Main Streamlit application
├── part2_feature_engineering_model_training.ipynb  # Model training notebook
│
├── Models & Data Files:
├── best_churn_model.pkl           # Trained churn prediction model
├── scaler_churn.pkl               # Scaler for churn features
├── gamma_gamma_model.pkl          # Gamma-Gamma CLV model
├── feature_names.pkl              # Feature column names
├── customer_level_data.csv        # Customer dataset
│
├── Docker Files:
├── Dockerfile                     # Docker image configuration
├── docker-compose.yml             # Docker Compose setup
├── .dockerignore                  # Files to exclude from image
├── requirements.txt               # Python dependencies
│
└── README.md                      # This file
```

---

## 🚀 Local Setup (Without Docker)

### Prerequisites
- Python 3.10 or higher
- pip package manager

### Installation Steps

1. **Clone or download the project**
```bash
cd /path/to/your/project
```

2. **Create virtual environment** (recommended)
```bash
python -m venv venv

# Activate virtual environment:
# On macOS/Linux:
source venv/bin/activate

# On Windows:
venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Run the app**
```bash
streamlit run app.py
```

5. **Access the app**
Open your browser and go to: `http://localhost:8501`

---

## 🐳 Docker Deployment

### Prerequisites
- Docker Desktop installed ([Download here](https://www.docker.com/products/docker-desktop))
- Docker Compose (included with Docker Desktop)

### Option 1: Using Docker Compose (Recommended)

1. **Navigate to project directory**
```bash
cd /path/to/your/project
```

2. **Build and run the container**
```bash
docker-compose up --build
```

3. **Access the app**
Open your browser and go to: `http://localhost:8501`

4. **Stop the container**
```bash
# Press Ctrl+C, then:
docker-compose down
```

### Option 2: Using Docker directly

1. **Build the Docker image**
```bash
docker build -t customer-data-platform .
```

2. **Run the container**
```bash
docker run -p 8501:8501 customer-data-platform
```

3. **Access the app**
Open your browser and go to: `http://localhost:8501`

4. **Stop the container**
```bash
# Find container ID:
docker ps

# Stop container:
docker stop <container-id>
```

---

## ☁️ Cloud Deployment Options

### 1. **Streamlit Community Cloud** (FREE & EASIEST)

Perfect for sharing your app publicly!

**Steps:**
1. Push your project to GitHub (create a new repository)
2. Go to [share.streamlit.io](https://share.streamlit.io)
3. Sign in with GitHub
4. Click "New app"
5. Select your repository, branch, and `app.py`
6. Click "Deploy"
7. Your app will be live at: `https://your-app-name.streamlit.app`

**Required files in GitHub:**
- `app.py`
- `requirements.txt`
- All `.pkl` model files
- `customer_level_data.csv`

**Note**: Make sure to add all model files (`.pkl`) to your GitHub repository!


## 📖 Usage Guide

### Making Predictions

1. **Navigate to "Predictions" tab**
2. **Enter customer data:**
   - Purchase behavior (invoices, revenue, amounts)
   - Timeline (recency, tenure)
   - Categories (product, payment, segment, region)
3. **Click "Generate Predictions"**
4. **View results:**
   - Churn risk score and recommendations
   - Customer Lifetime Value estimate
   - Customer insights

### Viewing Analytics

1. **Navigate to "Data Analysis" tab**
2. **Explore visualizations:**
   - Churn distribution
   - CLV distribution
   - Revenue vs Recency scatter plot
   - Purchase frequency histogram
3. **Review customer data table**

---

## 🛠️ Tech Stack

**Frontend:**
- Streamlit 1.31.0

**Machine Learning:**
- scikit-learn 1.4.0
- Lifetimes 0.11.3 (Gamma-Gamma model)

**Data Processing:**
- Pandas 2.1.4
- NumPy 1.26.3

**Visualization:**
- Plotly 5.18.0

**Deployment:**
- Docker
- Docker Compose

---

## 🔧 Customization

### Updating Models

1. Retrain models using Part 2 notebook
2. Replace `.pkl` files in project directory
3. Rebuild Docker image if using Docker

### Modifying UI

Edit `app.py` to:
- Change color schemes
- Add new visualizations
- Modify input fields
- Update recommendations logic

---

## 📊 Model Performance

**Churn Prediction:**
- Models tested: Logistic Regression, Random Forest, SVC
- Best model automatically selected based on accuracy

**CLV Prediction:**
- Gamma-Gamma Fitter for monetary value prediction
- Accounts for purchase frequency and recency

---

## 🐛 Troubleshooting

### Issue: Port already in use
```bash
# Kill process on port 8501:
# macOS/Linux:
lsof -ti:8501 | xargs kill -9

# Windows:
netstat -ano | findstr :8501
taskkill /PID <PID> /F
```

### Issue: Missing model files
- Ensure all `.pkl` files are in the same directory as `app.py`
- Run Part 2 notebook to generate missing files

### Issue: Docker build fails
- Check Docker Desktop is running
- Ensure `requirements.txt` is present
- Try: `docker system prune -a` to clean up

---

## 📝 Environment Variables

Optional environment variables you can set:

```bash
# For custom port
export STREAMLIT_SERVER_PORT=8080

# For headless mode
export STREAMLIT_SERVER_HEADLESS=true
```

---

## 🔒 Security Considerations

**For Production Deployment:**

1. **Environment Variables**: Store sensitive data in environment variables
2. **Authentication**: Add user authentication (Streamlit supports this)
3. **HTTPS**: Use SSL certificates for encrypted connections
4. **Rate Limiting**: Implement API rate limiting
5. **Data Privacy**: Ensure customer data is anonymized
6. **Backup**: Regular backup of models and data

---

## 📈 Scaling Tips

1. **Database Integration**: Replace CSV with PostgreSQL/MongoDB
2. **Caching**: Use `@st.cache_resource` and `@st.cache_data`
3. **Load Balancing**: Deploy multiple containers behind a load balancer
4. **CDN**: Use CDN for static assets
5. **Monitoring**: Implement logging and monitoring (e.g., Datadog, New Relic)

---

## 🤝 Contributing

To contribute to this project:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## 📄 License

This project is for educational/commercial use.

---

## 💬 Support

For issues or questions:
- Create an issue on GitHub
- Contact development team
- Check documentation

---

## 🎉 Acknowledgments

- **Streamlit** for the amazing framework
- **scikit-learn** for ML capabilities
- **Lifetimes** library for CLV modeling

---

**Version**: 1.0  
**Last Updated**: February 2026

---

## 🚀 Quick Start Commands

```bash
# Local development
streamlit run app.py

# Docker (quick)
docker-compose up

# Docker (build from scratch)
docker-compose up --build

# Stop Docker
docker-compose down

# View Docker logs
docker-compose logs -f
```

---

**Happy Deploying! 🎊**
