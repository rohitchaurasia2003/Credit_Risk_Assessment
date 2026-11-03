# Credit Risk Assessment Platform

This project demonstrates a practical credit risk assessment workflow that estimates default likelihood from applicant data and presents the result through a secure, user-friendly web interface.

> Sensitive operational details, production thresholds, and internal policy values have been intentionally generalized in this document.

## Overview

Credit Assessment is an end-to-end data science and application project designed to support credit underwriting decisions. The project combines:

- Data preparation and cleaning
- Feature engineering and preprocessing
- Model training and probability calibration
- A production-style API for serving predictions
- A lightweight frontend dashboard for real-time loan assessment

The core objective is to estimate whether a borrower is likely to default on a loan and present that risk in an interpretable, decision-support format. The application is built as a practical demonstration of how predictive intelligence can be translated into a usable tool for risk evaluation.

## The Idea

Loan default prediction is one of the most important problems in financial services. A lender needs to balance:

- approving credit to growth-oriented borrowers
- minimizing losses due to defaults
- creating transparent and explainable decisions

This project addresses that challenge by building a default-risk model from historical loan application data. Instead of simply classifying a borrower as approved or rejected, the system calculates a default probability and compares it with a learned decision threshold, which allows a decision-maker to evaluate risk contextually.

The project aims to demonstrate how modern machine learning can be packaged into a usable application for:

- credit review teams
- fintech prototypes
- data science showcases
- educational ML deployments

## Project Vision and Business Value

This project reflects a realistic financial-services workflow:

1. A loan application is submitted with borrower and loan attributes.
2. The application is transformed into a structured input payload.
3. A trained model predicts the probability of default.
4. A threshold is applied to classify the loan as high or low risk.
5. A front-end dashboard displays the result in a clear underwriting format.

This makes the project useful not only as a modeling exercise but also as a functional demo of how credit-scoring intelligence can be integrated into decision tools.

## Project Journey

The journey of this project follows a standard productized machine learning lifecycle:

### 1. Problem Framing
The project began with a real-world business need: estimate default risk from application-level loan data. The important question was not just whether the model performs well, but whether it can produce a usable probability estimate that supports decision-making.

### 2. Data Acquisition and Exploration
The project uses a loan dataset containing application-level attributes such as:

- age
- income
- home ownership
- employment length
- loan purpose
- loan grade
- loan amount
- interest rate
- ratio of loan to income
- prior default record
- credit history length

The dataset was inspected for missing values, structural inconsistencies, and invalid ranges. Basic cleaning and validation rules were applied to ensure the model learned from realistic, usable data.

### 3. Data Preparation
A structured preprocessing pipeline was built to handle:

- numerical features with imputation and scaling logic
- categorical variables via encoding
- invalid or out-of-range values

The preparation step ensures the model receives a stable, consistent input space regardless of data noise or missing records.

### 4. Modeling Strategy
The project uses an XGBoost classifier as the primary predictive model. XGBoost was chosen because it performs well on structured tabular data and is widely used in production-grade classification problems.

The workflow includes:

- train-test splits
- preprocessing pipeline integration
- probability generation for default risk
- threshold optimization to align model output with the intended classification behavior

### 5. Probability Calibration and Thresholding
A key improvement in the project is the use of model probability output and a tuned threshold. The trained model does not simply predict a hard label; it produces a probability of default. That probability is then measured against a calibrated threshold to determine whether a case should be interpreted as high risk or low risk.

This is especially important in credit contexts where probability estimates are more informative than binary labels alone.

### 6. Application Layer
Once the model was trained and serialized, the project moved into deployment-oriented implementation:

- the model is loaded into the FastAPI backend
- the API receives loan input from the frontend
- a prediction is generated in real time
- the response is returned to the web client

### 7. User Experience and Dashboard Design
A custom frontend dashboard was built to provide an underwriting-like experience. Users can input financial and personal information, submit the record, and instantly see:

- predicted default probability
- decision threshold
- classification result
- visual gauge representation of risk

This transforms an ML model into an interactive product experience.

## Solution Architecture

The project follows a simple and practical architecture:

- Frontend: HTML, CSS, JavaScript
- Backend: FastAPI
- ML Runtime: scikit-learn + XGBoost
- Serialization: joblib
- Data Processing: pandas
- Deployment / runtime: uvicorn

### High-Level Flow

Client Browser
  -> submits application form
  -> POST /predict to FastAPI
  -> model loads and predicts default probability
  -> response returned to UI
  -> dashboard renders risk verdict

## Key Features

- Credit default probability estimation
- Real-time prediction API
- Modern risk dashboard UI
- Threshold-based classification
- ML model persistence using joblib
- CORS-enabled API for frontend integration
- Static file serving for a complete single-service deployment
- Easy local execution with Python

## Dataset

The project uses a credit-risk dataset containing loan application data and a target variable indicating whether a borrower defaulted.

Representative fields include:

- `person_age`
- `person_income`
- `person_home_ownership`
- `person_emp_length`
- `loan_intent`
- `loan_grade`
- `loan_amnt`
- `loan_int_rate`
- `loan_percent_income`
- `cb_person_default_on_file`
- `cb_person_cred_hist_length`
- `loan_status` (target indicator used in the model training workflow)

This dataset is suitable for binary classification and risk modeling tasks in the credit domain.

## Model Details

The model pipeline was designed to handle mixed data types and preserve the predictive signal from both numeric and categorical inputs.

### Modeling approach

- Numeric variables processed with imputation and feature handling
- Categorical variables encoded using one-hot style preprocessing
- XGBoost classifier used as the final estimator
- Probability output used as the default-risk score
- Threshold tuned to convert probability into a decision outcome

The project produces both:

- continuous probability scores
- binary risk verdicts

This is useful because binary classification alone can hide nuance, while probability estimates communicate the strength of the risk signal.

## API Design

The project exposes a FastAPI endpoint for inference.

### Endpoint

- `POST /predict`

### Request Example

```json
{
  "person_age": 30,
  "person_income": 600000,
  "person_home_ownership": "RENT",
  "person_emp_length": 5,
  "loan_intent": "PERSONAL",
  "loan_grade": "B",
  "loan_amnt": 100000,
  "loan_int_rate": 11.5,
  "loan_percent_income": 0.17,
  "cb_person_default_on_file": "N",
  "cb_person_cred_hist_length": 6
}
```

### Example Response

```json
{
  "default_probability": 0.0,
  "default_prediction": 0,
  "threshold": 0.0,
  "Result": "Low Risk"
}
```

The response includes a probability score, model decision, threshold information, and a human-readable verdict.


- probability of default
- model prediction label
- threshold used for decisioning
- human-readable verdict

## Project Structure

```text
project-root/
├── main.py                     # API entry point
├── requirements.txt            # project dependencies
├── data/                      # training and validation data
├── models/                    # serialized model artifacts
├── notebooks/                 # exploratory analysis and training work
├── static/                    # frontend assets
│   ├── index.html
│   ├── style.css
│   └── script.js
├── README.md                  # project documentation
└── deployment/                # hosting configuration
```

## Tech Stack

### Machine Learning
- Python
- pandas
- scikit-learn
- XGBoost
- joblib

### Backend
- FastAPI
- uvicorn
- Pydantic

### Frontend
- HTML
- CSS
- JavaScript

## Getting Started

### Prerequisites

- Python 3.11+
- pip
- virtual environment recommended

### Installation

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### Run the Application

```bash
python main.py
```

The app will run locally and serve the frontend and API from:

- `http://localhost:8000/`

Alternatively, you can run:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

## Deployment Notes

This project is designed to be deployable in a standard cloud hosting environment with minimal configuration.

Typical deployment steps include:

- installing the Python dependencies
- starting the FastAPI application with uvicorn
- serving the frontend and backend from a single runtime
- configuring environment variables and hosting settings according to the platform

## Why This Project Matters

This project demonstrates how machine learning can move beyond notebooks and into decision-support tools. It shows the full loop from:

- raw data
- feature processing
- model training
- inference API
- interactive user interface

It is especially valuable for learning because it covers both the technical and product-facing sides of an AI-enabled business application.

## Current Scope and Limitations

This project is intended for:

- learning
- demonstration
- internal evaluation
- prototype workflows

It is not a production credit decision engine and should not be used as a final lending decision system without regulatory review, business validation, and risk governance processes.

## Future Enhancements

Possible next steps include:

- explainability features for model decisions
- SHAP or feature importance analysis
- improved threshold tuning with business cost analysis
- user authentication and role-based access
- database integration for historical scoring
- production deployment with environment variables and monitoring
- support for additional risk scenarios and underwriting policies

## Conclusion

Credit Ledger is a practical end-to-end project that blends machine learning, API development, and user-facing design. It captures the core idea of using data to estimate borrowing risk and turn that estimate into a usable decision-support product.

The project reflects a realistic data science journey: from raw data exploration and model development to API integration and dashboard presentation. It is a strong demonstration of how analytical intelligence can be transformed into an application that is understandable, actionable, and relevant to real-world financial decision-making.

## License

This project is intended for educational and demonstration purposes. Please review the repository usage context before applying it in a production or regulated environment.
