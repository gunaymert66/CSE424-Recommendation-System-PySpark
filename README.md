# CSE424 - Book Recommendation System with Apache Spark

**Aydın Adnan Menderes University | Big Data Analysis Term Project | 2026**


---

## Overview

Large-scale book recommendation engine built with Apache Spark's ALS (Alternating Least Squares) collaborative filtering algorithm on the Goodreads Book Reviews dataset containing 11 million user-book interactions.

---

## Dataset

- **Source:** [Goodreads Book Reviews - Kaggle](https://www.kaggle.com/datasets/pypiahmad/goodreads-book-reviews1)
- **Size:** 11,000,000 rows
- **Fields:**
  - `userId` (IntegerType): Unique user identifier
  - `bookId` (IntegerType): Unique book identifier
  - `rating` (FloatType): Explicit rating from 1.0 to 5.0

---

## System Environment

- **Platform:** Google Colab High-RAM Compute Node
- **OS:** Linux 6.6.122 x86_64
- **RAM:** 50.99 GB
- **Storage:** Google Drive via Fuse File System

---

## Features

- Computer info display (IP, CPU, RAM)
- ETL pipeline with type casting, null treatment, outlier filtering
- Apache Parquet columnar storage for optimized read performance
- RDD map() and reduceByKey() operations
- EDA with histograms and bar charts
- ALS collaborative filtering with 18 hyperparameter combinations
- MSE & RMSE performance evaluation for all models
- Predictions vs real values comparison
- Cosine similarity — Top 10 users for a given book

---

## ALS Hyperparameter Grid

| Parameter | Values |
|---|---|
| Rank | 10, 50, 200 |
| Max Iterations | 10, 50, 200 |
| Lambda (λ) | 0.01, 0.1 |
| **Total Models** | **18** |

---

## Results

### Full Model Comparison (RMSE Ranked)

| Rank | MaxIter | Lambda | RMSE | MSE | Status |
|---|---|---|---|---|---|
| 50 | 200 | 0.01 | **0.6401** | **0.4097** | 🥇 Best |
| 50 | 50 | 0.01 | 0.6718 | 0.4513 | Rank 2 |
| 50 | 200 | 0.1 | 0.6796 | 0.4618 | Rank 3 |
| 50 | 50 | 0.1 | 0.6809 | 0.4636 | Rank 4 |
| 50 | 10 | 0.1 | 0.6897 | 0.4757 | Rank 5 |
| 10 | 200 | 0.1 | 0.7021 | 0.4930 | Rank 6 |
| 10 | 50 | 0.1 | 0.7032 | 0.4945 | Rank 7 |
| 10 | 10 | 0.1 | 0.7101 | 0.5043 | Rank 8 |
| 10 | 200 | 0.01 | 0.7145 | 0.5106 | Rank 9 |
| 10 | 50 | 0.01 | 0.7325 | 0.5365 | Rank 10 |
| 10 | 10 | 0.01 | 0.7812 | 0.6103 | Rank 11 |
| 50 | 10 | 0.01 | 0.7912 | 0.6261 | Rank 12 |
| 200 | 200 | 0.1 | 1.0737 | 1.1529 | Rank 13 |
| 200 | 200 | 0.01 | 1.2562 | 1.5780 | Rank 14 |
| 200 | 50 | 0.1 | 1.3125 | 1.7225 | Rank 15 |
| 200 | 50 | 0.01 | 1.4561 | 2.1203 | Rank 16 |
| 200 | 10 | 0.1 | 1.6215 | 2.6291 | Rank 17 |
| 200 | 10 | 0.01 | 1.8987 | 3.6050 | Rank 18 (Overfitting) |

### Best Model

- **Rank:** 50 | **MaxIter:** 200 | **Lambda:** 0.01
- **RMSE:** 0.640091 — average prediction error of ~0.64 on a 5-star scale
- **MSE:** 0.409717

### Key Findings

- **Rank = 50** optimal — enough latent dimensions without overfitting
- **Rank = 200** causes severe overfitting (RMSE up to 1.89)
- **Lambda = 0.01** outperforms 0.1 at higher ranks
- Higher iterations consistently reduce RMSE for stable rank configurations

---

## Requirements

```
pyspark
kagglehub
numpy
pandas
matplotlib
psutil
```

## Usage

1. Open notebook in Google Colab
2. Mount Google Drive
3. Run cells sequentially (Cell 2 → Cell 38)
4. Dataset downloads automatically via kagglehub

## Files

- `notebook.ipynb` — Main project notebook
- `notebook.html` — HTML export
- Dataset: [Kaggle Link](https://www.kaggle.com/datasets/pypiahmad/goodreads-book-reviews1)
