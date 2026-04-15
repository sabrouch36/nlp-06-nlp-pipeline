# NLP Portfolio

## Overview
This portfolio summarizes my work in Web Mining and Applied NLP. It highlights the techniques I implemented, the data sources I analyzed, the EVTL pipelines I built, the signals I computed, and the insights I generated from text-focused projects.

## 1. NLP Techniques Implemented

This project implements core Natural Language Processing (NLP) techniques as part of a structured pipeline applied to an academic document from arXiv.

- **Tokenization (word-level):**
  I converted cleaned text into tokens (individual words) using Python string processing, enabling downstream frequency and pattern analysis.

- **Text Cleaning and Normalization:**
  I applied multiple preprocessing steps to improve text quality:
  - lowercasing all text
  - removing punctuation
  - normalizing whitespace
  - removing stopwords using spaCy

- **Stopword Removal (spaCy):**
  I used the spaCy language model (`en_core_web_sm`) to filter out common words that do not add meaningful signal to the analysis.

- **Frequency Analysis (Unigrams):**
  I computed word frequency distributions using Python's `Counter`, identifying the most common terms in the cleaned abstract.

- **Text Extraction from HTML:**
  I extracted structured fields (title, authors, abstract, subjects, submission date) from raw HTML using BeautifulSoup, converting semi-structured data into usable text.

- **Feature Engineering:**
  I created derived analytical features from the cleaned text, including:
  - `token_count`
  - `unique_token_count`
  - `type_token_ratio` (vocabulary richness)
  - `author_count`
  - `abstract_word_count`

- **Data Cleaning Evaluation:**
  I measured the impact of preprocessing by comparing raw and cleaned text, including the number of characters removed and percentage reduction.

- **Pipeline-Based Processing:**
  All NLP steps were implemented within a modular EVTL pipeline (`extract`, `validate`, `transform`, `analyze`, `load`), ensuring repeatability and structured data flow.

## 2. Systems and Data Sources

This project analyzes an academic web document sourced from arXiv.

- **Data Source:**
  The input data comes from an arXiv abstract page:
  https://arxiv.org/abs/2401.00001

- **Data Type:**
  The source data is HTML, which is semi-structured and designed for human viewing rather than analysis.

- **Structure Differences:**
  - HTML contains nested tags and inconsistent formatting
  - Extracted fields (title, authors, abstract) required manual inspection of page structure
  - Unlike structured formats such as JSON, HTML requires parsing and validation

- **Handling Messy Data:**
  - Used BeautifulSoup to parse HTML content
  - Validated presence of required elements (title, authors, abstract, etc.)
  - Adapted validation logic when switching to a new data source
  - Cleaned extracted text to remove noise such as punctuation, stopwords, and formatting artifacts

- **Data Organization:**
  - Raw HTML stored in: `data/raw/sabri_raw.html`
  - Processed dataset stored in: `data/processed/sabri_processed.csv`
  -
## 3. Pipeline Structure (EVTL)

This project follows a structured EVTL (Extract, Validate, Transform, Load) pipeline to process and analyze text data from a web source.

### Extract
- Retrieved raw HTML content from an arXiv page using an HTTP request (`requests.get`)
- Applied custom headers to identify the request as educational use
- Saved the raw HTML to: `data/raw/sabri_raw.html`

### Validate
- Parsed HTML using BeautifulSoup
- Inspected document structure and verified the presence of required elements:
  - title
  - authors
  - abstract
  - subjects
  - submission date
- Adapted validation logic to handle differences in the new data source (arXiv)

### Transform
- Extracted structured fields from HTML into Python variables
- Cleaned and normalized text:
  - lowercasing
  - punctuation removal
  - whitespace normalization
  - stopword removal (spaCy)
- Engineered derived features:
  - token_count
  - unique_token_count
  - type_token_ratio
  - author_count
- Converted processed data into a Pandas DataFrame

### Analyze
- Computed token frequency distributions using `Counter`
- Generated visualizations:
  - bar chart of top tokens (`sabri_top_tokens.png`)
  - word cloud (`sabri_wordcloud.png`)
- Logged summary statistics for inspection

### Load
- Saved the final dataset to:
  - `data/processed/sabri_processed.csv`
- Ensured results are reusable for downstream analysis
-
## 4. Signals and Analysis Methods

This project computes several analytical signals from the cleaned text to support interpretation and understanding of the document.

- **Word Frequency Analysis:**
  I used Python's `Counter` to calculate how often each token appears in the cleaned abstract. This helps identify dominant terms and key themes in the document.

- **Top Token Distribution:**
  I visualized the most frequent words using a horizontal bar chart (`sabri_top_tokens.png`), making it easier to compare their relative importance.

- **Word Cloud Visualization:**
  I generated a word cloud (`sabri_wordcloud.png`) where word size reflects frequency, providing a quick visual summary of the document content.

- **Token-Based Metrics:**
  I computed several numerical signals from the text:
  - `token_count`: total number of tokens after cleaning
  - `unique_token_count`: number of distinct words
  - `type_token_ratio`: ratio of unique words to total words, measuring vocabulary richness

- **Text Comparison (Raw vs Cleaned):**
  I compared raw and cleaned text to evaluate preprocessing impact, including the number of characters removed and percentage reduction.

- **Author and Metadata Signals:**
  I included additional features such as `author_count` and submission date to provide contextual information alongside text analysis.

## 5. Insights

The analysis of the arXiv abstract revealed several meaningful patterns and observations.

- **Dominant Technical Vocabulary:**
  The most frequent tokens in the cleaned text reflect domain-specific concepts related to the topic of the paper. This confirms that the preprocessing steps preserved important semantic content while removing noise.

- **Noise Reduction Effectiveness:**
  Comparing the raw and cleaned text showed a significant reduction in non-informative content (such as punctuation, stopwords, and formatting artifacts). This improved the clarity and reliability of the analysis.

- **Vocabulary Richness:**
  The computed `type_token_ratio` indicates the diversity of language used in the abstract. A higher ratio suggests a richer vocabulary, while a lower ratio would indicate repetition. This metric provides insight into the complexity of the document.

- **Consistency Between Visualizations and Data:**
  The top token frequency chart and the word cloud both highlighted similar key terms, confirming that the analysis results are consistent across different representations.

- **Structured Insight from Unstructured Data:**
  The project demonstrates how semi-structured HTML data can be transformed into a structured dataset and analyzed effectively, enabling meaningful interpretation of textual content.

- **Adaptability to New Data Sources:**
  By changing only the source URL (to an arXiv paper), the same pipeline was successfully reused. This highlights the flexibility and robustness of the system design.

## 6. Representative Work

### NLP Pipeline Project (arXiv Analysis)
https://github.com/sabrouch36/nlp-06-nlp-pipeline

This project implements a full EVTL pipeline to extract, validate, transform, analyze, and load text data from an arXiv web page. It demonstrates end-to-end NLP processing, including text cleaning, feature engineering, and visualization of word frequency patterns.

### NLP Web Documents Project
https://github.com/sabrouch36/nlp-05-web-documents

This project focuses on extracting and processing text from web documents, highlighting HTML parsing, data validation, and structured text transformation for analysis.


## 7. Skills

- Python-based data processing and scripting
- Natural Language Processing (NLP) fundamentals
- Text cleaning and normalization techniques
- Working with semi-structured HTML data
- Building structured EVTL data pipelines
- Feature engineering for text analysis
- Data visualization (matplotlib, wordcloud)
- Handling messy and inconsistent real-world data
- Creating analysis-ready datasets (Pandas DataFrames)
- Exporting and organizing data for reuse (CSV outputs)
- Professional documentation using Markdown
