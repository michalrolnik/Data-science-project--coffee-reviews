[readme.md](https://github.com/user-attachments/files/21856343/readme.md)

# Coffee Reviews — Data Science Project (Python)

Predicting coffee review scores from scraped data using a reproducible, notebook‑based pipeline (crawling → cleaning → EDA/visualization → ML models → evaluation).

---

## 📁 Repository Structure

```
.
├── Crawling- coffee.ipynb           # Scrape coffee reviews from target website
├── cleaning _data-coffee.ipynb      # Data cleaning, parsing, feature prepping
├── Visualization - coffee (1).ipynb # EDA charts & insights
├── machine learning - coffee.ipynb  # Model training & evaluation
├── coffee final (1).ipynb           # End-to-end run / presentation notebook
└── data/                            # (created locally) raw & processed files
```

> Tip: keep file/column names consistent between notebooks. If you modify paths or features, update the later notebooks accordingly.

---

## 🧰 Requirements

Create a fresh Python environment (3.10 or 3.11 recommended) and install:

```txt
beautifulsoup4
requests
pandas
numpy
scikit-learn
matplotlib
seaborn
nltk
joblib
jupyterlab
```

Optional (if you add lemmatization/NER): `spacy` and the English model `en_core_web_sm`.

---

## 🚀 Quick Start

### 1) Clone & set up

```bash
# clone
git clone https://github.com/michalrolnik/Data-science-project--coffee-reviews.git
cd Data-science-project--coffee-reviews

# create & activate a virtual env (Windows PowerShell example)
python -m venv .venv
. .venv/Scripts/Activate.ps1

# install deps
pip install -r requirements.txt  # if you add one
# or install manually
pip install beautifulsoup4 requests pandas numpy scikit-learn matplotlib seaborn nltk joblib jupyterlab

# one‑time NLTK downloads (only if notebook asks for them)
python - <<'PY'
import nltk
for pkg in ["punkt", "stopwords", "wordnet", "punkt_tab"]:
    try:
        nltk.download(pkg)
    except Exception as e:
        print("NLTK download warning:", pkg, e)
PY
```

> If you prefer VS Code: install the Python & Jupyter extensions. If you prefer a browser: run `jupyter lab` and open the notebooks.

### 2) Notebook run order

1. **Crawling- coffee.ipynb** → produces a raw dataset (e.g., `data/raw/coffee_reviews_raw.csv`).
2. **cleaning _data-coffee.ipynb** → outputs a clean dataset (e.g., `data/processed/coffee_clean.csv`).
3. **Visualization - coffee (1).ipynb** → exploratory charts.
4. **machine learning - coffee.ipynb** → trains models, saves artifacts (e.g., `models/` & `metrics.json`).
5. **coffee final (1).ipynb** → optional end‑to‑end / presentation.

> If you already have a saved clean dataset, you can skip the crawling step by placing the file under `data/processed/` and adjusting the read path in the notebooks.

---

## 🌐 Crawling Notes

- The crawler targets a public coffee‑review site and extracts fields such as title, roaster, origin, processing method, textual review, and overall score (depending on page structure).
- Respect robots.txt and polite crawling: set delays (e.g., `time.sleep(1)`), avoid excessive parallelism, and cache pages locally during development.
- Site markup changes over time. If selectors break, re‑inspect the HTML and update the BeautifulSoup queries.

---

## 🧪 Features & Models

Typical text and tabular features used in the project:
- **Text**: TF‑IDF of the written review (e.g., “blind assessment”).
- **Sentiment**: optional sentiment scores (VADER / rule‑based) if included.
- **Meta**: origin/processing/roaster encoded as categories (if available).

Baseline regressors:
- Linear/ElasticNet, RandomForestRegressor (swap/add others as needed: XGBoost, SVR).

Common metrics:
- MAE, RMSE, R². Persist both model and vectorizer with `joblib` for reuse.

---

## 📊 What you should see when it runs

- **Crawling notebook**: progress logs and a CSV under `data/raw/`.
- **Cleaning notebook**: null handling, deduping, parsed columns → `data/processed/coffee_clean.csv`.
- **Visualization notebook**: histograms/boxplots/word clouds/topic charts (saved under `reports/figures/`).
- **ML notebook**: train/test split, metrics printed, and saved artifacts (e.g., `models/model.joblib`, `models/vectorizer.joblib`).

---

## 🔁 Reproducing Results quickly (no crawl)

If you keep a snapshot of processed data, place it in `data/processed/` and start from the **Visualization** and **ML** notebooks. Update the input path at the top of each notebook.

---

## 📦 Exporting Predictions

Add a cell to `machine learning - coffee.ipynb` to load a new coffee’s text/meta and call `model.predict(...)`. Save outputs to `predictions/pred_YYYYMMDD.csv`.

---

## 🧹 Tips & Troubleshooting

- Kernel errors → verify the active interpreter is your project’s virtual env.
- `ModuleNotFoundError` → re‑install missing packages in the same env.
- Scraper stops → website structure changed; re‑open a page in your browser, adjust CSS selectors.
- Non‑ASCII text → ensure UTF‑8 when reading/writing CSV (`encoding="utf-8"`).

---

## 📄 License & Attribution

This repo is for an academic project. When scraping or redistributing data, follow the source site’s terms of use. If you publish results, credit the original review source.

---

## ✅ Next Steps (nice to have)

- Add `requirements.txt` and `environment.yml`.
- Save cleaned dataset and models to versioned folders.
- Provide a small sample CSV in `data/sample/` for quick ML testing without crawling.
- Wrap the trained model into a small Streamlit app for interactive scoring.


