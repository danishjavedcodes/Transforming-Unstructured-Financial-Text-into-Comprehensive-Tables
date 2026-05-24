# Transforming Unstructured Financial Text into Comprehensive Tables

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![NLTK](https://img.shields.io/badge/NLTK-NLP-green.svg)](https://www.nltk.org/)
[![spaCy](https://img.shields.io/badge/spaCy-NLP-orange.svg)](https://spacy.io/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Frames-lightgrey.svg)](https://pandas.pydata.org/)
[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-20BEFF.svg)](https://www.kaggle.com/code/danishjavedcodes/unstructured-financial-text-into-tables)

Convert **unstructured financial text** into **structured, analysis-ready tables** using **Natural Language Processing (NLP)** in Python. This project demonstrates how to turn long `.txt` documents—such as investment notes, deal summaries, and financial narratives—into organized **Pandas DataFrames** with columns for people, products, conditions, actions, and prices.

> **Medium article (full walkthrough):** [Converting Textual Data to Tabular Form Using NLP](https://medium.com/towards-artificial-intelligence/converting-textual-data-to-tabular-form-using-nlp-008a933fb872) — methodology, architecture, and step-by-step explanation on *Towards AI*.

---

## Table of Contents

- [Overview](#overview)
- [Why This Project](#why-this-project)
- [Features](#features)
- [How It Works](#how-it-works)
- [Output Schema](#output-schema)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [Sample Data](#sample-data)
- [Kaggle Notebook](#kaggle-notebook)
- [Related Reading](#related-reading)
- [Author](#author)
- [License](#license)

---

## Overview

Financial and business documents are often stored as **unstructured text**—hard to filter, sort, or visualize. This repository provides a complete **text-to-table NLP pipeline** that:

1. Reads raw text from a file
2. Splits records by title (colon-delimited format)
3. Tokenizes descriptions into sentences
4. Extracts structured fields with **POS tagging**, **spaCy**, and **regular expressions**
5. Builds a multi-column **tabular dataset** suitable for Excel, SQL, BI tools, or ML pipelines

Use cases include **financial text mining**, **document structuring**, **entity extraction**, and **preparing text for downstream analytics**.

---

## Why This Project

| Challenge | Solution |
|-----------|----------|
| Long text files are hard to scan | Convert to rows and columns |
| Manual copy-paste into spreadsheets | Automated NLP extraction |
| Mixed entities in one paragraph | Sentence-level tokenization + targeted extractors |
| Prices in varied formats (`$200,000`, `USD`, `dollars`) | Regex-based price detection |

---

## Features

- **Title–detail parsing** from colon-separated financial narratives
- **Sentence tokenization** with NLTK (`sent_tokenize`)
- **Person extraction** via proper nouns (`NNP`, `NNPS`)
- **Product extraction** via singular/plural nouns (`NN`, `NNS`)
- **Condition extraction** via adjectives and adverb–adjective patterns
- **Action extraction** with spaCy verb tagging
- **Price extraction** with regex for `$`, `USD`, and `dollars` patterns
- **Hierarchical table layout**—one row per sentence, grouped under each financial scenario title

---

## How It Works

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────────┐
│  Raw .txt file  │ ──► │  Title + Details │ ──► │  Sentence tokens    │
│  (financial)    │     │  (DataFrame)     │     │  (per description)  │
└─────────────────┘     └──────────────────┘     └──────────┬──────────┘
                                                            │
                    ┌───────────────────────────────────────┘
                    ▼
     ┌──────────────────────────────────────────────────────────────┐
     │  NLP extractors (per sentence)                               │
     │  • Proper nouns → Person    • Nouns → Product                │
     │  • Adjectives → Condition   • Verbs → Actions (spaCy)        │
     │  • Regex → Price                                             │
     └──────────────────────────────────────────────────────────────┘
                    │
                    ▼
     ┌──────────────────────────────────────────────────────────────┐
     │  Structured DataFrame: Title | Person | Product | Condition  │
     │                        | Actions | Price                     │
     └──────────────────────────────────────────────────────────────┘
```

For a detailed architecture diagram and methodology, see the [Medium article](https://medium.com/towards-artificial-intelligence/converting-textual-data-to-tabular-form-using-nlp-008a933fb872).

---

## Output Schema

| Column | Description | Extraction method |
|--------|-------------|-------------------|
| `Title` | Financial scenario (e.g., Real Estate Investment) | Text split on `:` |
| `Person` | Names and proper nouns | NLTK POS (`NNP`, `NNPS`) |
| `Product` | Nouns / product-like terms | NLTK POS (`NN`, `NNS`) |
| `Condition` | Descriptive state | Adjectives (`JJ`, `RB`+`JJ`) |
| `Actions` | Verbs in the sentence | spaCy (`VERB`, `VB`) |
| `Price` | Monetary values | Regular expressions |

---

## Tech Stack

- **Python 3**
- **[Pandas](https://pandas.pydata.org/)** — tabular data structures
- **[NLTK](https://www.nltk.org/)** — tokenization and POS tagging
- **[spaCy](https://spacy.io/)** (`en_core_web_sm`) — verb and linguistic analysis
- **`re`** — price pattern matching

---

## Installation

```bash
# Clone the repository
git clone https://github.com/danishjavedcodes/Transforming-Unstructured-Financial-Text-into-Comprehensive-Tables.git
cd Transforming-Unstructured-Financial-Text-into-Comprehensive-Tables

# Install dependencies
pip install pandas nltk spacy

# Download NLTK data (first run)
python -c "import nltk; nltk.download('punkt'); nltk.download('averaged_perceptron_tagger')"

# Download spaCy English model
python -m spacy download en_core_web_sm
```

---

## Usage

1. Open **`unstructured-financial-text-into-tables.ipynb`** in Jupyter, VS Code, or [Kaggle](https://www.kaggle.com/code/danishjavedcodes/unstructured-financial-text-into-tables).
2. Point the notebook to your text file (format: `Title: description text` per line).
3. Run all cells to produce the structured `new_df` table.

**Expected input format:**

```text
Real Estate Investment: John is considering buying a rental property listed for $200,000...
Stock Market Trading: Emily monitors the stock market daily, looking for opportunities...
```

---

## Sample Data

The notebook uses financial scenario narratives covering topics such as:

- Real estate investment  
- Stock market trading  
- Car purchase negotiation  
- Cryptocurrency investment  
- Forex, art, commodities, startup equity, and precious metals  

Each scenario is parsed into sentence-level rows with extracted entities.

---

## Kaggle Notebook

Run the project interactively (with sample dataset) on Kaggle:

**[Unstructured Financial Text into Tables — Kaggle Notebook](https://www.kaggle.com/code/danishjavedcodes/unstructured-financial-text-into-tables)**

---

## Related Reading

| Resource | Link |
|----------|------|
| **Medium article (Towards AI)** | [Converting Textual Data to Tabular Form Using NLP](https://medium.com/towards-artificial-intelligence/converting-textual-data-to-tabular-form-using-nlp-008a933fb872) |
| **Kaggle notebook** | [danishjavedcodes/unstructured-financial-text-into-tables](https://www.kaggle.com/code/danishjavedcodes/unstructured-financial-text-into-tables) |

---

## Author

**Danish Javed** — AI/ML Engineer  

- GitHub: [@danishjavedcodes](https://github.com/danishjavedcodes)  
- Medium: [Danish Javed](https://medium.com/@danish_javed)

---

## License

This project is open source. Feel free to use, modify, and cite with attribution.

---

### Keywords

`NLP` · `financial text mining` · `unstructured to structured data` · `text to table` · `Python pandas` · `entity extraction` · `POS tagging` · `spaCy` · `NLTK` · `tabular data conversion` · `financial NLP` · `document parsing`
