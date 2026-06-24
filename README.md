# Spam Email Classifier

I built this to get a feel for how text classification actually works — not just running a model but understanding why certain messages get flagged and others don't.

The dataset is the UCI SMS Spam Collection — 5,572 messages, 747 spam, 4,825 ham. Real messages, not synthetic ones.

---

## What it does

- Loads and explores the dataset (class distribution, message length patterns)
- Vectorizes text using TF-IDF
- Trains two models: Naive Bayes and Logistic Regression
- Compares them on accuracy, precision, recall, and F1
- Runs a live Gradio interface where you paste any message and get back highlighted spam triggers, reasons it was flagged, confidence scores, and a final verdict

---

## Results

| Model | Accuracy | Spam Precision | Spam Recall |
|---|---|---|---|
| Naive Bayes | 97.22% | 100% | 79% |
| Logistic Regression | 97.04% | 100% | 78% |

Naive Bayes edges it out. Both models never incorrectly flag a ham message as spam — the tradeoff is they miss roughly 1 in 5 actual spam messages.

One thing I noticed: spam messages average around 138 characters, ham messages around 71. Spammers write more. Makes sense when you think about it — they're trying to convince you of something.

---

## The Gradio interface

The interesting part. Paste any message and it:

- Highlights the words that pushed the spam score up (in red)
- Lists the specific reasons each word was flagged
- Shows ham vs spam confidence as a bar
- Gives a final verdict

It uses a weighted keyword signal system rather than the trained model directly, so the highlight logic is transparent and explainable — you can see exactly what it reacted to.

---

## Known limitation

The model misses about 21% of spam. Most of what it misses is context-dependent spam — messages that don't use classic trigger words but rely on tone or implication. That's a harder problem. For this project scope, 97% accuracy on a real-world dataset is a solid baseline.

---

## Stack

- Python, pandas, scikit-learn, matplotlib, seaborn
- Gradio for the interface
- Google Colab

---

## How to run

Open the notebook in Google Colab and run cells top to bottom. The Gradio interface launches at the end with a public share link.

Dataset loads automatically from a public URL — no manual download needed.
