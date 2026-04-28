# 🍽️ Restaurant Recommendation System

---

## 📌 Overview

This application uses **Content-Based Filtering** to recommend restaurants that share similar characteristics — such as cuisine type, restaurant type, and city — with a restaurant you already enjoy. Simply select a restaurant from the dropdown, and the system returns the **Top 10 most similar** restaurants along with their match scores.

---

## ✨ Features

- 🔍 **Smart Recommendations** — Cosine similarity-based engine for accurate matching
- 🎯 **Match Score** — Each recommendation shows a percentage-based similarity score
- 🖥️ **Modern UI** — Dark-themed, responsive interface with smooth animations
- 🔎 **Searchable Dropdown** — Quickly find any restaurant using the built-in search
- 📊 **Rich Restaurant Cards** — Displays location, cuisine, cost for two, and rating

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Language | Python 3.11 |
| Web Framework | Flask 3.1.0 |
| ML / Data | Scikit-Learn, Pandas, NumPy |
| Frontend | HTML5, CSS3, Jinja2 |
| UI Libraries | Choices.js, Font Awesome |
| Dataset | Zomato Bangalore Restaurants |
| Deployment | Gunicorn (Heroku-ready) |

---

## 📂 Project Structure

```
├── Model/
│   ├── build_model.py        # Data preprocessing, feature engineering & model export
│   └── Dataset/
│       └── archive/
│           └── zomato.csv    # Raw Zomato dataset
│
├── Flask/
│   ├── app1.py               # Flask application & recommendation logic
│   ├── restaurant1.csv       # Cleaned restaurant data (generated)
│   ├── restaurant.pkl        # Trained similarity model (generated)
│   ├── templates/
│   │   └── index.html        # Main UI template
│   └── static/
│       └── style.css         # Stylesheet
│
├── requirements.txt          # Python dependencies
├── runtime.txt               # Python version for deployment
├── Procfile                  # Gunicorn entry point for Heroku
└── README.md
```

---

## ⚙️ How It Works

### 1. Model Training (`build_model.py`)
1. **Data Cleaning** — Fixes encoding artifacts, standardizes ratings, removes duplicates
2. **Feature Engineering** — Merges `cuisines`, `rest_type`, and `listed_in(city)` into a single text "soup"
3. **Vectorization** — Uses `CountVectorizer` to convert text soup into token count matrix
4. **Similarity Computation** — Computes a **Cosine Similarity** matrix across all restaurants
5. **Export** — Saves the matrix, indices, and metadata into `restaurant.pkl`

### 2. Web Interface (`app1.py`)
1. Loads `restaurant.pkl` at server startup
2. On selection, retrieves the restaurant's similarity row
3. Sorts all restaurants by descending similarity score
4. Returns the Top 10 with metadata for display

---

## 🚀 Getting Started

### Prerequisites
- Python 3.11
- The Zomato dataset CSV placed at `Dataset/archive/zomato.csv`

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-username/restaurant-recommender.git
cd restaurant-recommender

# 2. Install dependencies
pip install -r requirements.txt
```

### Build the Model

```bash
cd Model
python build_model.py
```

This generates `restaurant1.csv` and `restaurant.pkl` inside the `Flask/` folder.

### Run the App

```bash
cd Flask
python app1.py
```

Open your browser and go to **http://localhost:5000**

---


> **Note:** The `restaurant.pkl` file must be committed or generated via a build step, as Heroku does not persist generated files across dynos.

---


## 📋 Dependencies

```
Flask==3.1.0
gunicorn==22.0.0
pandas==2.2.3
numpy==2.2.1
scikit-learn==1.6.1
```
