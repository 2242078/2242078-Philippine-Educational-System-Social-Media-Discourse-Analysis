# Philippine Educational System: Social Media Discourse Analysis

A text-mining pipeline that collects public social media discussion about the Philippine education system, then applies **topic modeling (LDA)**, **similarity and distance measures**, and a **rule-based sentiment classifier** to find what people talk about and how they feel about it.

> **Course:** 9349 ITE 17 – Data Mining, Saint Louis University (SAMCIS) · **Submitted:** June 25, 2026

---

## Table of Contents
- [Objectives](#objectives)
- [Data](#data)
- [Pipeline](#pipeline)
- [Key Findings](#key-findings)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Ethics & Data Handling](#ethics--data-handling)
- [Limitations](#limitations)
- [Team](#team)
- [License](#license)

## Objectives
1. Identify the main themes in public discussion of the Philippine educational system (LDA).
2. Measure textual similarity between comments and topics (cosine, Jaccard, Euclidean, Manhattan).
3. Evaluate topic quality with coherence and perplexity.
4. Determine public sentiment (positive, negative, neutral) toward each theme.
5. Build and validate a corpus-driven, rule-based sentiment classifier.

## Data
| Item | Detail |
|---|---|
| Collection | Web scraping with Apify and Python scripts |
| Platforms | Reddit, Facebook, TikTok, YouTube, Instagram, X/Twitter |
| Period | Public posts, comments, and threads from 2023 to the present |
| Final dataset | 971 rows × 9 columns after cleaning |

**Preprocessing:** removal of duplicates, spam, and incomplete records; text normalization; tokenization and stop-word handling; splitting grouped comments into individual entries.

> Raw scraped data is **not** included in this repository. See [Ethics & Data Handling](#ethics--data-handling).

## Pipeline
```
Scraping → Cleaning & preprocessing → Frequency analysis → LDA topic modeling
        → Similarity / distance analysis → Rule-based sentiment analysis → Validation
```

| Phase | Method |
|---|---|
| Topic modeling | Latent Dirichlet Allocation (gensim), number of topics chosen using coherence (c_v) and perplexity |
| Proximity | Cosine similarity, Jaccard similarity, Euclidean distance, Manhattan distance |
| Sentiment | Rule-based classifier built from a corpus-driven dictionary using Pointwise Mutual Information (PMI) |
| Validation | Manual annotation of a held-out sample; accuracy, precision, recall, F1 |

**Tools:** Python, pandas, NumPy, NLTK, gensim, scikit-learn, Matplotlib, Seaborn, WordCloud, Apify client.

## Key Findings
- **Five topics** gave the best balance of coherence and interpretability (coherence 0.2936 at 3 topics, **0.4924 at 5**, 0.4540 at 7, 0.4895 at 10).
- Themes included the **ARAL Program**, **DepEd's national education agenda and governance**, **teachers' financial struggles and loans**, **overall system performance and development**, and program/school implementation.
- **Sentiment leaned negative overall:** about 42 % negative, 29 % positive, 28 % neutral.
- Teachers' financial burdens drew the most negative sentiment (48.5 %), while DepEd's national education agenda was the only theme with a comparatively higher positive share (33.7 %).
- The rule-based classifier reached **69.47 % accuracy** on the manually validated hold-out set (negative class strongest; positive class precision 56.52 %, recall 76.47 %, F1 65.00 %).

## Repository Structure
```
ph-education-social-media-discourse-analysis/
│
├── data/
│   ├── README.md
│   └── social_media_cleaned_anonymized.csv
│
├── docs/
│   └── Ph-Social-Media-Discourse-Analysis-Report.pdf
│
├── figures/
│   ├── complete_lexicon.csv
│   ├── negative_lexicon.csv
│   ├── neutral_lexicon.csv
│   ├── positive_lexicon.csv
│   ├── lda_vis_interactive.html
│   ├── phase1_exploration.png
│   ├── phase3_proximity_heatmaps.png
│   ├── phase4_sentiment.png
│   └── phase4_wordclouds.png
│
├── notebooks/
│   └── Ph-Social-Media-Discourse-Analysis-*.ipynb
│
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

## Getting Started
```bash
git clone https://github.com/<your-username>/ph-education-social-media-analysis.git
cd ph-education-social-media-analysis

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

cp .env.example .env             # then add your own Apify token
```
Run the scripts in `src/` in pipeline order (collection → preprocessing → topic modeling → similarity → sentiment → validation).

## Ethics & Data Handling
- Only **public** content was collected, and the repository shares **aggregate results** rather than raw posts.
- Usernames, profile links, and other identifying details should be removed from any data you publish.
- API tokens are read from environment variables and are never committed.
- Check each platform's terms of service before collecting or redistributing content.

## Limitations
- The final dataset is small (971 records) and drawn from platforms whose users are not representative of the whole population.
- The sentiment classifier is dictionary-based and validated on a small manually labeled sample; it can struggle with sarcasm and Filipino–English code-switching.
- Topic coherence scores were moderate (below 0.5), so topic labels involve interpretation.

## Team
Jecquar Ravent Aguilan, Mark Angara, Ryan Adelard Barrera, Syed Karim, Leon Neil Padiernos, Gelina Tibayan, Daniel Linus Torres, Marvin John Vergara, Benedict Wacdagan.

Submitted to Mrs. Beverly Ferrer.

## License
Released under the [MIT License](LICENSE).
