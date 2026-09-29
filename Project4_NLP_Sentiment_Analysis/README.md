# DecodeLabs — Data Science Internship: Project 4
## NLP & Sentiment Analysis (Optional Mastery Phase)

A text-classification pipeline that reads unstructured product reviews and
predicts whether each one is **Positive** or **Negative**.

## Pipeline

```
Raw text → Pre-Process → TF-IDF Vectorize → Model (Naive Bayes / SVM) → Prediction
```

1. **Pre-Processing** (NLTK)
   - Tokenization (`word_tokenize`)
   - Negation-safe stop-word removal — "not", "no", "never", "nor",
     "cannot" are deliberately kept out of the stop-word list, so
     negated reviews (e.g. "not happy") don't get flipped into the
     wrong sentiment
   - POS-guided Lemmatization (`WordNetLemmatizer` + `pos_tag`) — a
     word's part of speech is detected first so verbs/adjectives reduce
     to their correct root (e.g. "went" → "go", not left unchanged)

2. **Vectorization**
   - `TfidfVectorizer` with unigrams + bigrams (`ngram_range=(1,2)`)
     so phrases like "not good" are captured as a single feature
   - `max_features` and `min_df` bound the vocabulary size

3. **Modeling**
   - `MultinomialNB` (with Laplace smoothing, `alpha=1.0`)
   - `LinearSVC` trained and compared against it
   - Evaluated with accuracy, precision/recall/F1 (`classification_report`),
     and a confusion matrix on a held-out 25% test split

4. **Prediction**
   - `predict_sentiment(review)` runs any new review through the full
     pipeline and returns `"Positive"` or `"Negative"`

## Dataset

A template-generated, balanced set of 120 product reviews (60 positive /
60 negative), built from noun/adjective word banks so pre-processing and
modeling could be demonstrated end-to-end without a real labeled corpus.
Swap in a real CSV of labeled reviews by loading it into the `reviews` /
`labels` lists near the top of the notebook, e.g.:

```python
import pandas as pd
df = pd.read_csv("reviews.csv")
reviews, labels = list(df["review"]), list(df["sentiment"])
```

## Known limitation

Because the training vocabulary comes from a fixed set of templates, the
model performs perfectly (100% accuracy) on held-out reviews built from
the *same* templates, but makes mistakes on genuinely new phrasing it
never saw (e.g. "waste of money", "best thing I've bought") — a realistic
illustration of why real-world sentiment models need large, varied
training data rather than templated examples.

## Setup

```bash
pip install nltk scikit-learn
```

Then, once per machine, download NLTK's data (run once inside the
notebook):

```python
import nltk
nltk.download('punkt')
nltk.download('punkt_tab')
nltk.download('stopwords')
nltk.download('wordnet')
nltk.download('omw-1.4')
nltk.download('averaged_perceptron_tagger')
nltk.download('averaged_perceptron_tagger_eng')
```

## Run

Open `project4_nlp_sentiment.ipynb` in VS Code or Jupyter and run all
cells top to bottom.

## Author

Muqaddas — Data Science Intern, DecodeLabs (Batch 2026)
