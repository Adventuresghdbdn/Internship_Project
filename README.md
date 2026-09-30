<div align="center">

# 🎓 Course Feedback Sentiment Analysis

**Turning 185 student responses into clear, data-backed recommendations**

![Python](https://img.shields.io/badge/Python-3.13-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![TextBlob](https://img.shields.io/badge/NLP-TextBlob-4B8BBE)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white)

</div>

---

## 📌 Overview

This project analyzes a **course-feedback survey of 185 students** across **6 categories**: teaching, course content, examination, labwork, library facilities, and extracurricular activities. Each category has a numeric rating (-1 / 0 / 1) and a free-text review.

The notebook cleans the raw data, engineers NLP sentiment features from the written reviews, compares them with the numeric ratings, and ends with **actionable recommendations** for the institution.

## 🎯 Key Highlights

- 🧹 **Cleaned and preprocessed** the dataset using **Pandas and NumPy**, producing an ML-ready dataframe (185 rows, 20 columns, no nulls).
- 🧠 **Engineered polarity-score features** with **TextBlob** for every review column, then classified feedback as **Positive / Neutral / Negative** using a threshold-based approach.
- 📊 **Analyzed rating distributions** with Matplotlib/Seaborn:
  - 🔴 **Labwork is the weakest area**, with about **20% negative** ratings (37 of 185).
  - 🟢 **Extracurricular is the strongest**, with about **83% positive** ratings (154 of 185).
- 📝 **Documented improvement recommendations** for each weak area.

---

## 🗂️ Dataset

| Property | Detail |
|---|---|
| Responses | 185 students |
| Categories | 6 (teaching, coursecontent, Examination, labwork, library_facilities, extracurricular) |
| Rating columns | 6 numeric columns: `-1` Negative, `0` Neutral, `1` Positive |
| Review columns | 6 free-text columns, one per category |
| Source file | `course_review.csv` |

---

## 🔄 Workflow

```text
Raw CSV ──► Cleaning ──► Rating Analysis ──► TextBlob Polarity ──► Threshold Classification ──► Visuals ──► Recommendations
```

1. **Data cleaning and preparation**
   - Standardized column names (removed stray leading whitespace).
   - Separated rating columns from review columns.
   - Filled missing ratings with `0` (neutral) and missing reviews with empty strings, then stripped whitespace.
2. **Rating analysis**: counted Negative / Neutral / Positive responses per category.
3. **NLP sentiment analysis**
   - Computed a TextBlob polarity score (-1 to +1) for each of the 6 reviews per student.
   - Averaged them into `avg_sentiment` per student.
   - Applied thresholds to classify each student's overall feedback.
4. **Visualization** of ratings, sentiment split, most negative respondents, and common words.
5. **Export** of the processed data to `analyzed_student_feedback.csv`.

### Sentiment Classification Rule

| Average polarity | Label |
|:---:|:---:|
| `> 0.1` | ✅ Positive |
| `-0.1` to `0.1` | ⚪ Neutral |
| `< -0.1` | ❌ Negative |

The ±0.1 buffer zone filters out mild or ambiguous comments (for example "it was okay") so that only clearly positive or negative feedback gets a strong label.

---

## 📈 Results & Visuals

### Rating distribution by category

| Category | Negative (-1) | Neutral (0) | Positive (1) |
|---|:---:|:---:|:---:|
| Teaching | 13 | 35 | 137 |
| Course content | 30 | 27 | 128 |
| Examination | 24 | 31 | 130 |
| **Labwork** | **37** | 16 | 132 |
| Library facilities | 31 | 27 | 127 |
| **Extracurricular** | 12 | 19 | **154** |

<p align="center">
  <img src="images/satisfaction_by_category.png" alt="Student satisfaction levels by category" width="650"/>
</p>

> Labwork has the highest share of negative ratings (~20%), while extracurricular activities have the highest share of positive ratings (~83%).

### Overall sentiment of textual feedback

<p align="center">
  <img src="images/sentiment_distribution.png" alt="Overall student sentiment pie chart" width="380"/>
</p>

Based on each student's **average** polarity across all six reviews, **96.2%** fall in the Positive class and **3.8%** in Neutral.

### Most negative respondents

Ranking students by lowest `avg_sentiment` lets reviewers read the most critical comments first, which is useful when there are too many responses to read in full.

<p align="center">
  <img src="images/top10_negative_students.png" alt="Top 10 most negative students by average sentiment" width="650"/>
</p>

### Common words in feedback

<p align="center">
  <img src="images/wordcloud.png" alt="Word cloud of student feedback" width="700"/>
</p>

---

## 💡 Recommendations

| Area | Pain point | Suggested improvement |
|---|---|---|
| 🔬 Labs | Broken or missing equipment | Monthly equipment audits and cloud storage for lab data |
| 📝 Exams | Lack of transparency | Release answer keys and provide automated feedback |
| 📚 Library | Low book stock | Expand digital library and add a pre-booking app |
| 👩‍🏫 Teaching | Lack of depth | Interactive case studies and mid-term feedback |
| 🎭 Events | Timing conflicts | Universal free slots for activities |

---

## ⚠️ Limitations

Being upfront about the approach's limits:

- **Missing ratings were imputed as neutral (`0`)**, which may slightly understate both positive and negative counts.
- **TextBlob is lexicon-based**, so it can misread sarcasm, mixed comments, or short replies like "Good" or "Not good".
- **Averaging six polarity scores per student dilutes strong negatives** in a single category, which is why the overall sentiment split looks more positive than the per-category ratings. Category-level sentiment columns (`*_review_sentiment`) are available for a finer view.
- The thresholds (±0.1) are a judgement call and were not tuned against labelled data.

---

## 🚀 Getting Started

```bash
# 1. Clone the repository
git clone <your-repo-url>
cd <your-repo-folder>

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn textblob wordcloud jupyter

# 3. Run the notebook
jupyter notebook Task_3.ipynb
```

Make sure `course_review.csv` is in the same folder as the notebook.

---

## 📁 Project Structure

```text
├── Task_3.ipynb                     # Full analysis notebook
├── course_review.csv                # Raw survey data
├── analyzed_student_feedback.csv    # Output with sentiment features
├── images/                          # Charts used in this README
└── README.md
```

---

## 🔮 Future Work

- Train a supervised classifier (e.g., Logistic Regression) on the ML-ready features.
- Compare TextBlob against VADER or a transformer-based sentiment model.
- Add topic modeling (LDA) to group complaints automatically.
- Build an interactive dashboard for administrators.

---

## 🛠️ Tech Stack

`Python` · `Pandas` · `NumPy` · `TextBlob` · `Matplotlib` · `Seaborn` · `WordCloud` · `Jupyter Notebook`

---

<div align="center">

⭐ If you found this project useful, consider giving it a star!

</div>
