# 🎫 Customer Support Ticket Resolution Time Prediction

A machine learning regression project developed to predict the **resolution time of customer support tickets** using **Linear Regression and Support Vector Regression (SVR)**.

The project explores how historical customer support data can be prepared and modelled to estimate how long a support ticket may take to resolve. The workflow includes **data cleaning, categorical encoding, feature engineering, feature scaling, regression modelling, hyperparameter tuning, model evaluation, and prediction on new data**.

---

## 🎯 Project Objective

Customer support teams handle large volumes of service requests, and understanding how long a ticket may take to resolve can support better operational planning and resource allocation.

The objective of this project was to:

- Prepare and clean customer support ticket data for machine learning.
- Engineer a continuous target variable representing ticket resolution time.
- Build a Linear Regression baseline model.
- Develop a Support Vector Regression model for non-linear relationships.
- Tune the SVR model using GridSearchCV.
- Compare model performance using R².
- Use the trained models to estimate resolution time for a sample ticket.

---

## 📊 Dataset

The project uses the **Customer Support Ticket Dataset** sourced from Kaggle.

### Original Dataset

- **8,469 records**
- **17 original columns**
- Combination of categorical, textual, numerical, and date/time information.

The dataset includes information relating to:

- Customer characteristics
- Product purchased
- Ticket type
- Ticket status
- Ticket priority
- Ticket channel
- First response time
- Resolution time
- Customer satisfaction

### Target Variable

A new continuous target variable called:

```text
Resolution Hours
```

was derived from the difference between:

```text
Time to Resolution - First Response Time
```

This represents the estimated number of hours required to resolve a customer support ticket.

### Dataset Preview

![Dataset Overview](./screenshots/01-dataset-overview.png)

---

## 🧹 Data Preparation

Several preprocessing steps were performed before model development.

### 1. Missing Value Handling

Missing values were identified in fields including:

- Resolution
- First Response Time
- Time to Resolution
- Customer Satisfaction Rating

Missing values were handled before modelling.

### 2. Removing Unnecessary Features

Columns not required for prediction were removed, including:

- Ticket ID
- Customer Name
- Customer Email
- Ticket Subject
- Ticket Description
- Resolution

### 3. Categorical Encoding

One-hot encoding was applied to categorical features such as:

- Customer Gender
- Product Purchased
- Ticket Type
- Ticket Status
- Ticket Priority
- Ticket Channel

### 4. Date Conversion

Date-related columns were converted into datetime format to enable time-based calculations.

### 5. Feature Engineering

Additional features were extracted from date/time information:

- Purchase Month
- Purchase Day
- First Response Hour
- First Response Minute

The `Resolution Hours` target variable was also created during this stage.

![Data Preprocessing](./screenshots/02-data-preprocessing.png)

---

## ⚖️ Feature Scaling

`StandardScaler` from Scikit-learn was used to standardise the input features.

Scaling is particularly important for Support Vector Regression because the algorithm is sensitive to differences in feature magnitude.

The input features were scaled while the target variable remained in its original unit of **hours**.

---

## ✂️ Train-Test Split

The dataset was divided into:

```text
80% Training Data
20% Testing Data
```

Resulting in approximately:

```text
Training records: 6,775
Testing records: 1,694
```

This allowed the models to be evaluated using data that was not used during training.

---

# 🤖 Machine Learning Models

Two regression approaches were explored.

## 1️⃣ Linear Regression

Linear Regression using **Ordinary Least Squares (OLS)** was used as the baseline model.

The model achieved approximately:

```text
R² = 0.492
```

or:

```text
49.2%
```

This indicates that the Linear Regression model explained approximately 49.2% of the variation in ticket resolution time within the analysis.

![Linear Regression Results](./screenshots/03-linear-regression-results.png)

---

## 2️⃣ Support Vector Regression

Support Vector Regression was used to model potentially non-linear relationships between ticket characteristics and resolution time.

The initial SVR configuration used:

```text
Kernel  = RBF
C       = 10
Epsilon = 0.5
```

The basic SVR model achieved:

```text
R² = 51.35%
```

![SVR Results](./screenshots/04-svr-results.png)

The result improved on the Linear Regression baseline.

---

# 🔧 Hyperparameter Tuning

`GridSearchCV` was used to identify a stronger SVR configuration.

The parameter grid explored:

```text
Kernel  = linear, poly, rbf, sigmoid
C       = 1, 10
Epsilon = 0.1, 1.0
```

with:

```text
3-fold cross-validation
```

The selected parameters were:

```text
Kernel  = RBF
C       = 10
Epsilon = 0.1
```

![GridSearchCV Best Parameters](./screenshots/05-gridsearch-best-parameters.png)

GridSearchCV allowed multiple SVR configurations to be evaluated systematically using cross-validation.

---

# 📈 Model Comparison

The submitted project report summarised the model results as:

| Model | R² Score |
|---|---:|
| Linear Regression (OLS) | 49.20% |
| Basic SVR (RBF) | 51.35% |
| Tuned SVR (GridSearchCV) | 52.47% |

Based on the submitted analysis, the tuned SVR achieved the highest reported R² among the evaluated approaches.

---

## 🔮 Prediction on New Data

A sample observation was used to demonstrate prediction using the trained models.

The reported sample predictions were approximately:

| Model | Predicted Resolution Time |
|---|---:|
| Linear Regression | 7.71 hours |
| Basic SVR | 5.95 hours |
| Tuned SVR | 6.15 hours |

![Model Predictions](./screenshots/06-model-predictions.png)

These predictions demonstrate how the regression workflow can be used to estimate ticket resolution time for a sample input.

---

## 🛡️ Overfitting Considerations

Several techniques were included in the modelling workflow to support model generalisation:

- 80/20 train-test split
- Feature scaling
- Cross-validation
- GridSearchCV
- Hyperparameter tuning
- Evaluation using unseen test data

---

## 💡 Key Findings

The project analysis found that:

- Linear Regression provided a useful baseline.
- SVR achieved a higher reported R² than the Linear Regression baseline.
- The RBF kernel was selected through the tuning process.
- GridSearchCV selected `C = 10` and `epsilon = 0.1`.
- The tuned SVR produced the highest reported R² in the submitted model comparison.
- The moderate R² results also indicate that additional factors may influence ticket resolution time.

Potential additional variables discussed in the project include factors such as agent experience, issue characteristics, and staffing conditions.

---

## ⚠️ Limitations & Future Improvements

The project identified that ticket resolution time is influenced by factors that may not be fully represented in the available dataset.

Potential future improvements include:

- Additional feature engineering
- Agent-level operational variables
- More detailed issue characteristics
- Staffing and workload information
- Random Forest regression
- Gradient Boosting models
- Additional model-evaluation metrics
- More extensive hyperparameter optimisation

---

## 🛠️ Technologies Used

| Area | Technology |
|---|---|
| Programming | Python |
| Data Manipulation | Pandas |
| Numerical Processing | NumPy |
| Machine Learning | Scikit-learn |
| Statistical Modelling | Statsmodels |
| Baseline Model | Linear Regression / OLS |
| Non-Linear Model | Support Vector Regression |
| Hyperparameter Tuning | GridSearchCV |
| Feature Scaling | StandardScaler |
| Development Environment | Google Colab / Jupyter Notebook |

---

## 👩‍💻 My Contribution

This was completed as a **group academic project**.

My individual contribution focused primarily on:

- Building the Support Vector Regression model
- Evaluating SVR performance
- Performing hyperparameter tuning using GridSearchCV
- Selecting and evaluating the tuned SVR configuration
- Completing the prediction section
- Contributing to the overall report structure
- Contributing to the model evaluation discussion

This work provided practical experience in **regression modelling, model optimisation, cross-validation, prediction, and interpretation of machine-learning results**.

---

## 📁 Repository Structure

```text
customer-support-ticket-resolution-prediction/
│
├── code/
│   ├── customer-support-resolution-model.ipynb
│   └── customer-support-resolution-model.py
│
├── data/
│   └── customer-support-tickets.csv
│
├── report/
│   └── customer-support-resolution-report.pdf
│
├── screenshots/
│   ├── 01-dataset-overview.png
│   ├── 02-data-preprocessing.png
│   ├── 03-linear-regression-results.png
│   ├── 04-svr-results.png
│   ├── 05-gridsearch-best-parameters.png
│   └── 06-model-predictions.png
│
└── README.md
```

---

## 🔗 Explore the Project

| Resource | Link |
|---|---|
| 📓 Jupyter Notebook | **[View Notebook](./code/customer-support-resolution-model.ipynb)** |
| 🐍 Python Script | **[View Python Code](./code/customer-support-resolution-model.py)** |
| 📄 Project Report | **[View Report](./report/customer-support-resolution-report.pdf)** |
| 📊 Dataset | **[View Dataset](./data/customer-support-tickets.csv)** |
| 🖼️ Results & Screenshots | **[View Screenshots](./screenshots/)** |

---

## 🎓 Academic Context

**Module:** Applied Statistics and Machine Learning  
**Module Code:** B9BA205  
**Academic Year:** 2025–26

This project was completed as part of postgraduate academic work in **Business Analytics**.

---

## 👩‍💻 Author

**Varsha Sundararaj**

MSc Business Analytics  
Dublin Business School, Ireland

Former Product Support Technical Advisor – IQVIA  
Aspiring Data Analyst | Business Analyst

🔗 [LinkedIn](https://www.linkedin.com/in/varsha-sundararaj-40a463201)  
🔗 [GitHub](https://github.com/varshasundararaj-analytics)

---

⭐ This repository forms part of my portfolio showcasing projects across **Data Analytics, Business Analytics, Machine Learning and Customer Support Analytics**.