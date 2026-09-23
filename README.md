# 🧠 Mental Health Signal — Student Wellness Analytics & Score Predictor

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100%2B-009688.svg)](https://fastapi.tiangolo.com/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-ML%20Model-F7931E.svg)](https://scikit-learn.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](#license)

**Mental Health Signal** is a full-stack Machine Learning application designed to predict and analyze a student's mental health wellness score (on a 0–10 scale) based on their daily habits, screen usage, academic pressure, lifestyle routines, and perceived stress levels.

The project combines a **FastAPI** machine learning backend with an interactive, responsive **Vanilla HTML/CSS/JS web dashboard** featuring real-time input validation and an animated SVG gauge meter output.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Tech Stack](#-tech-stack)
- [Project Architecture & Directory Structure](#-project-architecture--directory-structure)
- [Machine Learning Model & Input Features](#-machine-learning-model--input-features)
- [Installation & Setup Guide](#-installation--setup-guide)
- [Running the Application](#-running-the-application)
- [API Documentation & Endpoints](#-api-documentation--endpoints)
  - [`GET /`](#get-)
  - [`POST /predict`](#post-predict)
- [Score Interpretation & Signals](#-score-interpretation--signals)
- [Disclaimer](#-disclaimer)

---

## 🔍 Overview

Students face unique challenges balancing academic workloads, digital connectivity, screen time, physical health, and personal well-being. This project leverages empirical data to model how daily behavioral routines impact overall mental wellness.

### How It Works:
1. **User Input**: The student provides demographic, academic, digital usage, and lifestyle details via an intuitive web form.
2. **Preprocessing & Pre-validation**: Inputs are validated client-side and preprocessed on the backend into a structured Pandas DataFrame.
3. **ML Inference**: A pre-trained Machine Learning model (`Mental_Health_Model.pkl`) evaluates the input vector and outputs a predicted mental health score.
4. **Visual Signal**: The web app animates an arc gauge meter and categorizes the result into actionable feedback signals (*Strained*, *Balanced*, or *Strong*).

---

## ✨ Key Features

- ⚡ **Fast & Lightweight Backend**: Powered by FastAPI with asynchronous request handling and CORS middleware enabled.
- 🎨 **Modern & Responsive UI**: Clean layout utilizing CSS Glassmorphism, Google Fonts (*Fraunces*, *Inter*, *JetBrains Mono*), custom segmented controls, and dark accent styling.
- 📊 **Interactive SVG Gauge Meter**: Visual representation of predicted scores from 0.0 to 10.0 with dynamic color gradients and smooth CSS arc offset transitions.
- 🛡️ **Dual-Layer Input Validation**:
  - **Client-Side**: Immediate JavaScript validation with inline field error highlighting.
  - **Server-Side**: Schema enforcement via Pydantic model (`StudentData`) with range checks (`ge`/`le` constraints).
- 🔄 **Automatic Country Grouping**: Intelligently categorizes input countries into top regional clusters or defaults to `"Other"` for consistent model feature mapping.

---

## 🛠️ Tech Stack

### Backend & Machine Learning
- **Python 3.8+**
- **FastAPI**: REST API framework
- **Uvicorn**: ASGI web server implementation
- **Pydantic**: Data validation and setting management
- **Scikit-Learn**: Machine learning model training and inference
- **Joblib**: Model serialization & loading
- **Pandas & NumPy**: Data manipulation and array transformations

### Frontend
- **HTML5**: Semantic document structure
- **CSS3**: Modern layout (Flexbox/Grid), CSS Variables, smooth transitions, custom gauge styling
- **JavaScript (ES6+)**: Fetch API, DOM manipulation, dynamic SVG generation, and event handling

---

## 📁 Project Architecture & Directory Structure

```text
Mental_Health_Score_Predict/
├── index.html                                 # Web Application Interface
├── style.css                                  # Dashboard Stylesheet & UI Design Tokens
├── script.js                                  # Frontend Logic, Validation & API Client
├── main.py                                    # FastAPI Backend & Model Serving Endpoint
├── Mental_Health_Model.pkl                    # Pre-trained Scikit-Learn Model Pipeline
├── ML_Project.ipynb                           # Data Exploration & Model Training Notebook
├── Student Social Media And Mental Health Impact.csv # Dataset used for training
├── requirements.txt                           # Python Dependencies
├── .gitignore                                 # Git Ignore Rules
└── README.md                                  # Project Documentation
```

---

## 🤖 Machine Learning Model & Input Features

The backend model accepts **12 input features** covering 3 core categories:

| Category | Feature Name | Data Type / Enum Values | Validation / Constraints |
| :--- | :--- | :--- | :--- |
| **Profile** | `age` | Integer | `10 <= Age <= 100` |
| | `gender` | Categorical | `'Male'`, `'Female'` |
| | `country` | String | Formatted into top regions or `'Other'` |
| **Academic & Digital** | `academic_level` | Categorical | `'High School'`, `'Undergraduate'`, `'Graduate'` |
| | `most_used_platform` | Categorical | `'Facebook'`, `'LinkedIn'`, `'Instagram'`, `'Snapchat'`, `'Twitter'`, `'YouTube'`, `'TikTok'`, `'LINE'`, `'KakaoTalk'`, `'VKontakte'`, `'WhatsApp'`, `'WeChat'` |
| | `purpose_of_use` | Categorical | `'Networking'`, `'Education'`, `'Entertainment'`, `'News'` |
| | `avg_daily_usage_hours` | Float | `0.0 <= Hours <= 24.0` |
| | `daily_unlocks` | Integer | `Unlocks >= 0` |
| **Lifestyle & Stress** | `study_hours` | Float | `0.0 <= Hours <= 24.0` |
| | `physical_activity_hours` | Float | `0.0 <= Hours <= 24.0` |
| | `sleep_hours_per_night` | Float | `0.0 <= Hours <= 24.0` |
| | `stress_level` | Categorical | `'Low'`, `'Medium'`, `'High'`, `'Very High'` |

---

## 📥 Installation & Setup Guide

### Prerequisites
- Python `3.8` or higher installed on your machine.
- Git installed.

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/Mental_Health_Score_Predict.git
cd Mental_Health_Score_Predict
```

### 2. Create & Activate a Virtual Environment
- **Windows**:
  ```powershell
  python -m venv venv
  .\venv\Scripts\activate
  ```
- **macOS / Linux**:
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

---

## 🚀 Running the Application

### Step 1: Launch the FastAPI Backend Server
Run the backend using Uvicorn:
```bash
uvicorn main:app --reload --port 8000
```
The server will start at `http://127.0.0.1:8000`.

### Step 2: Open the Frontend Interface
You can run the web dashboard by either:
1. Double-clicking `index.html` to open it directly in your browser.
2. Serving it using VS Code **Live Server** extension or Python's HTTP server:
   ```bash
   python -m http.server 5500
   ```
   Then navigate to `http://127.0.0.1:5500` in your web browser.

---

## 📖 API Documentation & Endpoints

FastAPI automatically generates interactive API documentation when the backend is running:
- **Swagger UI**: [`http://127.0.0.1:8000/docs`](http://127.0.0.1:8000/docs)
- **ReDoc**: [`http://127.0.0.1:8000/redoc`](http://127.0.0.1:8000/redoc)

### `GET /`
- **Description**: Health check / Welcome greeting endpoint.
- **Response**:
  ```json
  {
    "message": "Welcome you all Guys"
  }
  ```

### `POST /predict`
- **Description**: Accepts student metrics and returns a predicted mental health score.
- **Request Body (JSON)**:
  ```json
  {
    "age": 21,
    "gender": "Female",
    "country": "India",
    "academic_level": "Undergraduate",
    "most_used_platform": "Instagram",
    "purpose_of_use": "Entertainment",
    "avg_daily_usage_hours": 4.5,
    "daily_unlocks": 50,
    "study_hours": 5.0,
    "physical_activity_hours": 1.5,
    "sleep_hours_per_night": 7.0,
    "stress_level": "Medium"
  }
  ```
- **Response (200 OK)**:
  ```json
  {
    "predicted_mental_health_score": 6.78
  }
  ```

---

## 📊 Score Interpretation & Signals

The system categorizes scores into three signal bands to offer contextual feedback:

| Score Range | Signal Label | Description |
| :--- | :--- | :--- |
| **0.00 – 3.99** | 🔴 **Signal: Strained** | Indicates elevated strain. Adjustments in sleep, screen time, or stress management may help restore balance. |
| **4.00 – 6.99** | 🟡 **Signal: Balanced** | Indicates a steady rhythm with room for optimization and better rest habits. |
| **7.00 – 10.00** | 🟢 **Signal: Strong** | Indicates habits aligned with a well-supported, resilient wellness baseline. |

---

## ⚠️ Disclaimer

> **Built for educational and informational purposes only.**  
> This application uses machine learning to estimate a signal score based on self-reported daily habits. **It is not a medical or clinical diagnostic tool.** If you or someone you know is experiencing mental health challenges, please consult a qualified healthcare professional or reach out to a trusted counselor.

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
