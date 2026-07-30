# 🏥 Healthcare Premium Prediction

A machine learning application that predicts annual healthcare insurance premiums using a **segmented modeling approach**.

Instead of using a single model for every customer, this project divides customers into two age groups:

- **Young customers (Under 25 years)**
- **Adults (25 years and above)**

Separate machine learning models were trained for each group to improve prediction accuracy. The trained models are deployed in a **Streamlit web application**, which automatically selects the appropriate model based on the user's age.

---

## 🚀 Live Demo

🔗 **https://hanad-ml-healthcare-insurance-prediction-app.streamlit.app/**

---

# 📌 Features

- Interactive Streamlit web application
- Automatic age-based model selection
- Separate preprocessing pipelines for each customer segment
- Real-time healthcare premium prediction
- Trained models exported with Joblib for deployment

---

# 🧠 Project Motivation

Initial experiments using a single regression model revealed significantly higher prediction errors for younger customers.

To address this issue, the dataset was segmented into two age groups:

- Under 25 years
- 25 years and above

Each segment was trained independently, allowing the models to learn patterns specific to their customer group and improve prediction performance.

---

# 📂 Dataset

The project uses separate datasets for each customer segment.

- `premiums_young.xlsx`
- `premiums_rest.xlsx`

Each dataset contains customer demographic, financial, and health-related information used to predict annual healthcare insurance premiums.

---

# ⚙️ Machine Learning Pipeline

## 1. Data Preparation

- Data cleaning
- Missing value handling
- Outlier removal
- Standardization of categorical values

## 2. Data Segmentation

Customers were divided into two age groups:

- Young (Under 25)
- Rest (25+)

## 3. Feature Engineering

- Categorical encoding
- Numerical scaling
- Medical risk feature engineering

## 4. Model Training

Final training notebooks:

- `ml_premium_prediction_young_with_gr.ipynb`
- `ml_premium_prediction_rest_with_gr.ipynb`

Each notebook trains a dedicated model for its respective customer segment.

## 5. Deployment

The trained models and preprocessing pipelines were exported as Joblib artifacts and integrated into a Streamlit application.

During prediction:

1. User enters customer information.
2. Age determines the customer segment.
3. The corresponding scaler and model are loaded.
4. The predicted annual premium is displayed.

---

# 🗂 Project Structure

```text
Healthcare_Premium_Prediction/
│
├── app/
│   ├── artifacts/
│   ├── main.py
│   └── prediction_helper.py
│
├── artifacts/
│   ├── model_young.joblib
│   ├── model_rest.joblib
│   ├── scaler_young.joblib
│   └── scaler_rest.joblib
│
├── data_segmentation.ipynb
├── ml_premium_prediction_young_with_gr.ipynb
├── ml_premium_prediction_rest_with_gr.ipynb
│
├── premiums_young.xlsx
├── premiums_rest.xlsx
│
├── requirements.txt
├── runtime.txt
└── README.md
```

---

# 🛠 Tech Stack

- Python
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- Joblib
- Streamlit
- Matplotlib
- Seaborn

---

# ▶️ Running Locally

Clone the repository

```bash
git clone https://github.com/HanadIsmail/Healthcare_Premium_Prediction.git
```

Move into the project directory

```bash
cd Healthcare_Premium_Prediction
```

Install dependencies

```bash
pip install -r requirements.txt
```

Run the application

```bash
streamlit run app/main.py
```

---

# 💡 How the Prediction Works

The deployed application follows these steps:

- Collects customer information through the Streamlit interface.
- Determines whether the customer belongs to the **Young** or **Adult** segment based on age.
- Loads the corresponding scaler and trained model.
- Generates the annual healthcare premium prediction instantly.

---

# 🚀 Future Improvements

- Add SHAP model explainability
- Confidence intervals for predictions
- Docker containerization
- Automated model retraining pipeline
- Model monitoring and drift detection

---

## License

This project is for educational and portfolio purposes.

---

## 👤 Author

**Hanad Ismail**

GitHub: https://github.com/HanadIsmail

If you found this project useful, consider giving it a ⭐ on GitHub.
