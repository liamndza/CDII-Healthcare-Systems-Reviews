# Yelp Health Plan Sentiment Analysis

Exploratory data analysis and sentiment analysis of Yelp reviews for California health plans and medical groups, with the goal of building a patient satisfaction metric.

---

## Introduction

Patient satisfaction is a critical but often underutilized signal in evaluating health plan performance. While traditional surveys are the standard, public review platforms like Yelp offer a large, unsolicited source of patient feedback that can complement existing measures. This was created when my office, at that time, was facing budget cuts in outsourcing traditional external survey and research organizations. Thus, I was tasked with utilizing non-traditional platforms, such as Yelp, to open up possible sources for feedback and rating frameworks.

This project is meant to open up new ideas and possibilities. I acknowledge that data from social media can be quite messy!

This project explores whether Yelp reviews can be used to derive a meaningful patient satisfaction metric for California health plans and medical groups. By scraping reviews via the SerpAPI Yelp engine and applying NLP-based sentiment analysis, we aim to surface patterns in patient experience that may not appear in structured survey data.

---

## Features

- **Yelp Data Scraping** via [SerpAPI](https://serpapi.com/) — searches by location/business name and fetches reviews by `place_id`
- **Exploratory Data Analysis** — rating distributions, word clouds for positive and negative reviews
- **Text Preprocessing** — lowercasing, punctuation removal, stopword filtering, and lemmatization via NLTK
- **Dual Sentiment Analysis**:
  - **VADER** (rule-based, optimized for social media text)
  - **RoBERTa** (`cardiffnlp/twitter-roberta-base-sentiment-latest`, transformer-based)
- **Category Labeling** — binary classification: positive (rating > 3) vs. negative (rating ≤ 3)
- **Mismatch Analysis** — identifies reviews where VADER sentiment contradicts the Yelp star rating

---

## Tools and Framework

| Purpose | Library |
|---|---|
| API Scraping | `serpapi` |
| Data Manipulation | `pandas`, `numpy` |
| Visualization | `matplotlib`, `wordcloud` |
| NLP / Preprocessing | `nltk` |
| Transformer Model | `transformers` (HuggingFace) |
| ML Utilities | `scikit-learn` |

---

The notebook is organized into four parts:

| Part | Description |
|---|---|
| I | Scrape Yelp review data via SerpAPI |
| II | EDA — rating distribution, word clouds |
| III | Sentiment analysis with VADER and RoBERTa |
| IV | Application to medical groups across California counties |

---

## Notes & Limitations

- Some insurance providers have **multiple Yelp listings** across locations — it is recommended to scrape and merge these for a more representative score.
- For smaller medical groups, review counts may be too low for statistically significant quantitative conclusions; qualitative interpretation is recommended in those cases.
- VADER occasionally misclassifies reviews containing positive words used in a negative context (e.g., sarcasm). RoBERTa generally handles this better.
