# E-commerce Causal Analysis

An end-to-end data analysis project using e-commerce behavioral data to investigate customer purchase behavior and estimate the impact of promotional treatment on purchase outcomes.

---

## 📌 Project Overview

This project analyzes event-level behavioral data from a multi-category e-commerce store.

The main objective is to move beyond descriptive analysis and investigate how promotional treatment may affect customer purchase behavior.

The project focuses on:

- Customer behavioral patterns
- Product interactions
- Shopping sessions
- Promotional treatment
- Purchase outcomes
- Heterogeneous treatment effects
- Uplift modeling
- Promotion targeting policies

The analysis follows a structured pipeline from raw data preprocessing to causal effect estimation and promotion policy analysis.

---

## 🎯 Objectives

The project aims to:

1. Clean and preprocess raw e-commerce event data.
2. Explore customer behavioral patterns.
3. Construct customer sessions and identify decision points.
4. Define treatment and purchase outcomes.
5. Build customer-level features for modeling.
6. Establish baseline machine learning models.
7. Estimate heterogeneous treatment effects (CATE).
8. Validate model stability across multiple random seeds.
9. Analyze important features related to treatment response.
10. Develop a data-driven promotion policy.

---

## 📊 Dataset

The project uses the **E-commerce Behavior Data from a Multi-Category Store** dataset from Kaggle.

### Dataset Source

Kaggle dataset:

`mkechinov/ecommerce-behavior-data-from-multi-category-store`

The dataset contains user interaction events collected from an e-commerce platform.

### Available Files

The downloaded dataset contains:

- `2019-Oct.csv`
- `2019-Nov.csv`

The current analysis uses:

```text
2019-Oct.csv
```

as the primary dataset.

The raw dataset is downloaded programmatically using `kagglehub` and is not stored directly in this repository.

---

## 🧾 Main Variables

| Variable | Description |
|---|---|
| `event_time` | Timestamp of the user event |
| `event_type` | Type of user interaction |
| `product_id` | Product identifier |
| `category_id` | Product category identifier |
| `category_code` | Product category hierarchy |
| `brand` | Product brand |
| `price` | Product price |
| `user_id` | User identifier |
| `user_session` | Original user session identifier |

Typical event types include:

- `view`
- `cart`
- `remove_from_cart`
- `purchase`

---

## 📁 Analysis Results

The full uplift modeling results are available separately because the
generated CSV file exceeds GitHub's 100 MB file-size limit.

### Final Results

The complete `final_uplift_results.csv` file can be accessed here:

👉 **[Download final uplift results] https://drive.google.com/drive/folders/1hXgfJYUfgQdMQl9XwhMeeGbCvV3zood4?usp=sharing **

The file contains the final decision-level results produced by the
uplift modeling pipeline, including estimated treatment effects and
promotion targeting information.

The CSV file is hosted externally and is not stored directly in this
GitHub repository.

---

# 🔬 Analysis Pipeline

## Stage 1 — Data Cleaning

The raw event data is cleaned and prepared for analysis.

Main tasks include:

- Loading the raw dataset
- Parsing timestamps
- Handling missing values
- Removing invalid observations
- Preparing event-level variables

---

## Stage 2 — Event Discovery

Customer event behavior is analyzed to identify important and unusual event patterns.

This stage includes:

- Daily event aggregation
- Robust statistical analysis
- Event-level anomaly detection
- Event classification

---

## Stage 3 — Session Construction

User interactions are organized into behavioral sessions.

A session-gap rule is used to identify separate sessions and meaningful decision points.

Key outputs include:

- `session_id`
- Session-level event information
- Decision-point indicators

---

## Stage 4 — Treatment & Outcome

Treatment and outcome variables are constructed for causal analysis.

### Treatment

The treatment indicator represents whether a customer was exposed to the defined promotional condition.

```text
T = 1 → Treated
T = 0 → Control
```

### Outcome

The outcome represents whether a purchase occurred within the defined outcome window.

```text
Y = 1 → Purchase
Y = 0 → No Purchase
```

---

## Stage 5 — Feature Engineering

Customer- and session-level covariates are constructed for modeling.

Examples include:

- Customer activity features
- Behavioral frequency
- Product interaction features
- Session-level statistics
- Price-related variables
- Historical reference price

The resulting feature matrix is used as input for downstream models.

---

## Stage 6 — Baseline Models

Baseline machine learning models are established before applying causal and uplift modeling approaches.

The purpose is to provide a reference point for evaluating the performance of more advanced models.

---

## Stage 7 — CATE / Uplift Modeling

The project estimates **Conditional Average Treatment Effects (CATE)** to investigate heterogeneous treatment effects.

Rather than assuming that a promotion affects every customer equally, the analysis attempts to identify differences in treatment response across customers.

Conceptually:

```text
CATE(x)
=
Expected Outcome under Treatment
-
Expected Outcome under Control
```

This allows customers to be analyzed based on their estimated response to treatment.

---

## Stage 8 — Multi-seed Validation

Model performance and treatment-effect estimates are evaluated across multiple random seeds.

This helps assess whether the results are stable rather than dependent on a single train/test split.

---

## Stage 9 — Explainability

Feature importance and treatment-response patterns are analyzed to better understand which customer characteristics are associated with heterogeneous treatment effects.

---

## Stage 10 — Promotion Policy

Estimated treatment effects are translated into a promotion decision policy.

The goal is to prioritize promotional resources toward customers who are expected to benefit most from treatment.

---

# 🗂️ Project Structure

```text
ecommerce-causal-analysis/
│
├── data/
│   └── .gitkeep
│
├── notebooks/
│   └── ecommerce_analysis.ipynb
│
├── src/
│
├── .gitignore
├── README.md
├── requirements.txt
│
└── .venv/
```

### Directory Description

| Directory / File | Purpose |
|---|---|
| `data/` | Local data directory |
| `notebooks/` | Jupyter notebooks for analysis |
| `src/` | Python source code and reusable functions |
| `.gitignore` | Files excluded from Git |
| `README.md` | Project documentation |
| `requirements.txt` | Python dependencies |
| `.venv/` | Local virtual environment |

> `.venv/` is a local Python environment and should not be committed to GitHub.

---

# ⚙️ Environment Setup

## 1. Clone the Repository

```bash
git clone <https://github.com/BaoVy2810/ecommerce-causal-analysis.git>
cd ecommerce-causal-analysis
```

---

## 2. Create a Virtual Environment

On macOS/Linux:

```bash
python3 -m venv .venv
```

Activate the environment:

```bash
source .venv/bin/activate
```

After activation, the terminal should display:

```text
(.venv)
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 4. Install the Jupyter Kernel

```bash
pip install ipykernel
```

Then register the environment:

```bash
python -m ipykernel install \
    --user \
    --name ecommerce-causal \
    --display-name "Python (ecommerce-causal)"
```

In VS Code, select:

```text
Python (ecommerce-causal)
```

as the notebook kernel.

---

# 📥 Dataset Download

The dataset is downloaded automatically using `kagglehub`.

```python
import kagglehub

path = kagglehub.dataset_download(
    "mkechinov/ecommerce-behavior-data-from-multi-category-store"
)

print("Dataset path:", path)
```

The analysis then loads:

```text
2019-Oct.csv
```

Raw dataset files are not committed to GitHub.

---

# ▶️ Running the Project

Open the notebook:

```text
notebooks/ecommerce_analysis.ipynb
```

Select the project environment:

```text
Python (ecommerce-causal)
```

Then run the notebook sequentially from top to bottom.

Recommended execution order:

```text
Setup
   ↓
Dataset Download
   ↓
Data Loading
   ↓
Configuration
   ↓
Stage 1 — Data Cleaning
   ↓
Stage 2 — Event Discovery
   ↓
Stage 3 — Session Construction
   ↓
Stage 4 — Treatment & Outcome
   ↓
Stage 5 — Feature Engineering
   ↓
Stage 6 — Baseline Models
   ↓
Stage 7 — CATE / Uplift
   ↓
Stage 8 — Validation
   ↓
Stage 9 — Explainability
   ↓
Stage 10 — Promotion Policy
```

---

# 🛠️ Technologies

The project is developed using Python and the following libraries:

- Python 3.12
- Pandas
- NumPy
- SciPy
- Scikit-learn
- Matplotlib
- Seaborn
- LightGBM
- KaggleHub
- Jupyter Notebook

---

# 📈 Expected Outputs

The analysis is expected to produce:

- Cleaned e-commerce event data
- Customer and session behavioral statistics
- Decision-point dataset
- Treatment and outcome variables
- Feature matrix
- Baseline model results
- CATE / uplift estimates
- Multi-seed validation results
- Feature importance analysis
- Promotion targeting policy
- Final uplift results (`final_uplift_results.csv`)

---

# 📌 Notes

- Raw datasets are not included in the repository.
- The dataset is downloaded through KaggleHub.
- `.venv/` is a local Python environment and should not be committed.
- The notebook should be executed sequentially because later stages depend on outputs generated by earlier stages.
- The primary dataset used in the current analysis is `2019-Oct.csv`.

---

# 👥 Project

This repository contains the implementation and analysis for an e-commerce causal and uplift modeling project.