# Google Play Reviews - Sentiment Analysis for Indonesian Telco Apps

Scrape, preprocess, and analyze Google Play reviews for the Big 3 telco apps in Indonesia:
- **MyTelkomsel** - Telkomsel
- **myXL** - XL Axiata
- **myIM3** - Indosat Ooredoo

## Pipeline

| Step | Notebook | Description |
|------|----------|-------------|
| 1 | `01_scrape_reviews.ipynb` | Scrape reviews from Google Play (max 10k/app, last 3 months, English) |
| 2 | `02_preprocessing.ipynb` | Clean text, remove duplicates, detect language |
| 3 | `03_sentiment_analysis.ipynb` | Sentiment analysis (TextBlob + VADER) and categorization |

## Setup

```bash
pip install -r requirements.txt
```

## Data Flow

```
01_scrape  -->  data/raw/all_reviews_YYYYMMDD.csv
02_preprocess  -->  data/processed/reviews_cleaned_YYYYMMDD.csv
03_analysis  -->  data/final/reviews_analyzed_YYYYMMDD.csv + .xlsx
```

Output files are tagged with the execution date (`YYYYMMDD`) for versioning.

## Categorization Labels

| Category | Description |
|----------|-------------|
| Apps | App performance, UI, crashes, bugs, updates |
| Feature | Specific features, functionality |
| Others - Price | Pricing, packages, cost |
| Others - Network | Signal, speed, coverage |
| Others - Content | Promos, offers, rewards |
| Others - General | Uncategorized |

## Sentiment Methods

- **TextBlob**: Polarity-based baseline (-1 to +1)
- **VADER**: Optimized for social media/review text (compound score)

Both methods classify reviews as positive, neutral, or negative.
