# Customer Sentiment & Feedback Analytics

An end-to-end analytics and NLP project for transforming large volumes of customer reviews into **aspect-level sentiment, recurring product issues, and actionable business insights**.

The project combines **Python, SQL, NLP, spaCy, Tableau, and Streamlit** to help product and business teams understand what customers like, what they dislike, and which issues should be prioritized.

---

## Overview

Customer reviews contain valuable information about product quality, usability, performance, pricing, delivery, customer support, and other aspects of the customer experience.

However, manually reviewing thousands of comments makes it difficult to identify:

* Which product features customers discuss most frequently
* Which features generate positive or negative sentiment
* Which issues are recurring
* Whether customer sentiment is improving or declining
* Which problems should receive the highest priority

This project addresses these problems by building a pipeline that converts unstructured customer feedback into structured analytical insights.

### Analytics Pipeline

```text
                    CUSTOMER REVIEWS
                           │
                           ▼
                    Data Ingestion
                           │
                           ▼
                     Data Cleaning
                           │
                ┌──────────┴──────────┐
                ▼                     ▼
           SQL Analysis          NLP Pipeline
                │                     │
                │              ┌──────┴──────┐
                │              ▼             ▼
                │        Aspect/Topic    Sentiment
                │        Extraction      Analysis
                │              │             │
                │              └──────┬──────┘
                │                     ▼
                │              Aspect-Level
                │               Sentiment
                │                     │
                └────────────┬────────┘
                             ▼
                     Issue Categorization
                             │
                             ▼
                       Priority Scoring
                             │
                             ▼
                  Business Recommendations
                             │
                     ┌───────┴────────┐
                     ▼                ▼
                  Tableau          Streamlit
                  Dashboard         Explorer
```

---

## Business Problem

A product team receives thousands of customer reviews but does not have an efficient way to convert those reviews into structured product intelligence.

The goal is to answer:

> **What are customers talking about, how do they feel about each aspect, and which issues should the business prioritize?**

---

## Key Questions

The analysis is designed to answer questions such as:

### Customer Feedback

* What are the most frequently mentioned product aspects?
* Which topics generate the most customer discussion?
* What percentage of reviews are positive, neutral, or negative?

### Product Issues

* Which features receive the most negative sentiment?
* Which problems occur repeatedly?
* Are particular product categories associated with specific issues?

### Trends

* Is sentiment changing over time?
* Are negative reviews increasing for a particular feature?
* Which issues are becoming more prominent?

### Business Prioritization

* Which issues have both high frequency and negative sentiment?
* Which product areas should be investigated first?
* What actions could potentially improve customer satisfaction?

---

## Features

### 1. Data Ingestion & Cleaning

The pipeline processes customer-review data and prepares it for downstream analysis.

Typical fields include:

```text
review
rating
product
category
date
```

The preprocessing stage handles:

* Missing values
* Duplicate reviews
* Text normalization
* Invalid ratings
* Date formatting
* Basic text cleaning

---

### 2. Aspect / Topic Extraction

The NLP pipeline identifies product features and topics mentioned by customers.

For example:

```text
Review:
"The sound quality is excellent but the battery drains too quickly."

Extracted aspects:

sound quality
battery
```

spaCy is used to identify relevant noun phrases and nouns before applying cleaning and filtering rules.

---

### 3. Aspect-Level Sentiment Analysis

Instead of assigning a single sentiment to an entire review, the project attempts to associate sentiment with individual aspects.

Example:

```text
Review:
"The sound is amazing but the battery dies quickly."

Aspect              Sentiment
--------------------------------
Sound               Positive
Battery             Negative
```

This provides more useful information than simply classifying the complete review as positive or negative.

---

### 4. Issue Categorization

Extracted aspects can be grouped into broader business categories such as:

```text
Product Quality
Performance
Battery
Connectivity
Usability
Pricing
Delivery
Packaging
Customer Support
Features
```

This makes the results easier for product and business teams to interpret.

---

### 5. Priority Scoring

The project introduces a prioritization layer to identify issues that deserve further investigation.

A priority score can consider factors such as:

```text
Issue Frequency
×
Negative Sentiment
×
Impact Weight
```

The exact scoring methodology will be documented based on the dataset and analysis performed.

The purpose is not to produce an arbitrary score, but to provide a transparent way of ranking recurring customer problems.

---

## Example Business Insight

Instead of reporting:

> "The dataset contains negative reviews."

The system should produce insights such as:

> **Battery performance is one of the most frequently mentioned negative aspects and should be investigated as a high-priority product issue.**

The dashboard can then allow the user to drill down into the reviews contributing to that result.

---

## SQL Analytics

The processed review data is stored in a relational database to support structured analysis.

Example analytical questions include:

```sql
-- Review volume by month

SELECT
    DATE_TRUNC('month', review_date) AS month,
    COUNT(*) AS review_count
FROM reviews
GROUP BY month
ORDER BY month;
```

Additional SQL analysis includes:

* Review volume
* Average rating
* Negative-review percentage
* Aspect frequency
* Sentiment by aspect
* Product/category comparisons
* Monthly sentiment trends
* High-priority issue identification

---

## Technology Stack

### Programming & NLP

* Python
* Pandas
* NumPy
* spaCy
* NLP / Sentiment Analysis

### Data

* SQL
* MySQL / PostgreSQL
* CSV datasets

### Visualization

* Tableau
* Streamlit
* Matplotlib / Plotly where required

### Development

* Git
* GitHub
* Jupyter Notebook
* Pytest

---

## Project Structure

```text
customer-sentiment-feedback-analytics/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   ├── 01_exploratory_analysis.ipynb
│   └── 02_nlp_analysis.ipynb
│
├── src/
│   ├── ingestion/
│   │   └── load_data.py
│   │
│   ├── preprocessing/
│   │   └── clean_reviews.py
│   │
│   ├── nlp/
│   │   ├── aspect_extraction.py
│   │   ├── sentiment.py
│   │   └── categorization.py
│   │
│   ├── analytics/
│   │   └── priority_scoring.py
│   │
│   └── database/
│       └── queries.sql
│
├── dashboard/
│   └── app.py
│
├── tests/
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Dashboard

The dashboard is designed around business questions rather than only model outputs.

### Planned Views

**Overview**

* Total reviews
* Average rating
* Positive / negative sentiment
* Review volume
* Top customer concerns

**Aspect Analysis**

* Most frequently mentioned aspects
* Sentiment by aspect
* Positive vs. negative distribution
* Representative reviews

**Issue Prioritization**

* High-frequency negative issues
* Priority score
* Category-level breakdown
* Product/category comparison

**Trend Analysis**

* Sentiment over time
* Aspect frequency over time
* Emerging negative issues

---

## Validation & Testing

The project will include validation at both the data and application levels.

### Data Validation

* Missing-value checks
* Duplicate detection
* Invalid rating detection
* Data-type validation
* Date validation

### NLP Validation

* Review-level sentiment checks
* Aspect extraction examples
* Incorrect/common tag filtering
* Manual sample validation

### Application Testing

Planned tests include:

* Data preprocessing
* Aspect extraction
* Sentiment classification
* Priority calculation
* SQL queries
* Dashboard data loading

---

## Expected Business Value

The project is designed to help teams:

* Analyze customer feedback at scale
* Identify recurring product issues
* Understand sentiment around individual features
* Detect emerging customer concerns
* Prioritize product improvements
* Reduce manual review of large feedback datasets
* Support product decisions with evidence from customer data

---

## Future Improvements

Potential extensions include:

* Transformer-based sentiment models
* Better aspect-based sentiment analysis
* Topic modeling
* Automated issue clustering
* Multilingual review analysis
* Review summarization using LLMs
* Automated product-manager reports
* Real-time review ingestion
* Feedback classification using supervised learning
* Alerting for rapidly increasing negative sentiment

---

## Dataset

The application expects customer-review data containing a review text field.

Minimum required field:

```text
review
```

Optional fields:

```text
rating
product
category
review_date
customer_id
```

A public dataset will be used for development and evaluation. Dataset attribution and licensing information will be documented in the repository.

---

## Getting Started

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd customer-sentiment-feedback-analytics
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it on Windows:

```powershell
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the analysis

Run the notebooks or execute the processing pipeline:

```bash
python -m src.preprocessing.clean_reviews
```

### 5. Launch the Streamlit dashboard

```bash
streamlit run dashboard/app.py
```

---

## Project Status

**Status:** In Development

Current development stages:

* [ ] Dataset selection and data ingestion
* [ ] Data cleaning pipeline
* [ ] Exploratory data analysis
* [ ] Aspect extraction
* [ ] Sentiment analysis
* [ ] Aspect-level sentiment aggregation
* [ ] SQL analytics
* [ ] Issue categorization
* [ ] Priority scoring
* [ ] Tableau dashboard
* [ ] Streamlit dashboard
* [ ] Testing and validation
* [ ] Final business insights
* [ ] Documentation

---

## Disclaimer

This is an independent analytics and NLP project created for learning and demonstrating practical skills in **data analysis, natural language processing, SQL, visualization, and business intelligence**.

It is not affiliated with or endorsed by any company.

---

## Author

**Ishan Singh**

B.E. Artificial Intelligence & Machine Learning

Interests: **AI Engineering • Data Analytics • Business Analysis • NLP • AI Workflows**
