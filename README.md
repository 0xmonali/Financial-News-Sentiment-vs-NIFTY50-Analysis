# Financial News Sentiment vs NIFTY50 Analysis

## Project Overview
This project explores the relationship between financial news sentiment and NIFTY50 market direction using real-world datasets. The goal is to investigate whether information extracted from financial news headlines can provide useful signals about short-term stock market movement.

### Key Components:
* 3,000+ financial news articles
* NIFTY50 stock market dataset
* Rule-based sentiment analysis
* Data preprocessing and feature engineering
* Exploratory Data Analysis (EDA)
* Simple prediction logic

**Tech Stack:** Python, Pandas, Matplotlib, and JupyterLab.

---

## Problem Statement
Financial markets are heavily influenced by information flow, investor psychology, and public sentiment. This project attempts to answer the following question:

> **Can financial news sentiment help explain or predict NIFTY50 market movement?**

Rather than using advanced NLP models or pretrained sentiment engines, this project intentionally uses a beginner-friendly, rule-based approach to build a complete end-to-end data science workflow.

---

## Objectives
* **Clean & Preprocess:** Handle real-world, messy financial datasets.
* **Align Data:** Synchronize stock market data with financial news by date.
* **Sentiment Scoring:** Create a custom sentiment scoring system using financial vocabulary.
* **Analyze & Visualize:** Explore relationships between sentiment and market movement using charts.
* **Predict:** Build and evaluate a basic sentiment-driven prediction model.

---

## Dataset Description

### 1. Financial News Dataset
* **Volume:** 3,000+ financial news headlines (multiple headlines per day)
* **Coverage Period:** February 2025 – August 2025
* **Features:** Date, News title / headline text

### 2. NIFTY50 Stock Dataset
* **Coverage Period:** February 2025 – August 2025
* **Features:** Date, Open, High, Low, Close, Shares Traded, Turnover

---

## Project Workflow
```text
Raw Financial News Dataset  +  Raw NIFTY50 Dataset
                       ↓
                 Data Cleaning
                       ↓
              Date Standardization
                       ↓
             News Grouping by Date
                       ↓
                  Dataset Merging
                       ↓
                Feature Engineering
                       ↓
          Rule-Based Sentiment Analysis
                       ↓
           Exploratory Data Analysis
                       ↓
                Prediction Logic
                       ↓
             Performance Evaluation