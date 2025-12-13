# simpleRNN-project

# 🎬 IMDB Sentiment Analysis using Simple RNN

## 📌 Project Overview

This project implements an **end-to-end Deep Learning sentiment analysis system** using a **Simple Recurrent Neural Network (SimpleRNN)** on the IMDB movie reviews dataset.
The primary goal is to understand how basic RNN architectures handle sequential text data and to analyze their strengths and limitations in real-world NLP tasks.

---

## 🎯 Objective

* Build a complete NLP pipeline: **data loading → preprocessing → model training → inference**
* Use **SimpleRNN** intentionally (not LSTM/GRU) for educational purposes
* Observe how SimpleRNN behaves on **positive vs negative sentiment**
* Deploy the trained model for real-time predictions using **Streamlit**

---

## 📂 Project Structure

```
IMDB-Sentiment-Analysis/
│
├── app.py                  # Streamlit application
├── simple_rnn_imdb.keras   # Trained SimpleRNN model
├── requirements.txt        # Project dependencies
├── README.md               # Project documentation
```

---

## 📊 Dataset

* **Dataset**: IMDB Movie Reviews (Keras built-in dataset)
* **Total samples**: 50,000 reviews

  * 25,000 training
  * 25,000 testing
* **Task**: Binary sentiment classification

  * `1` → Positive
  * `0` → Negative
* **Vocabulary size**: Top 10,000 most frequent words

---

## 🧠 Model Architecture (SimpleRNN)

```text
Embedding Layer (128 dimensions)
↓
SimpleRNN (128 units, tanh activation)
↓
Dropout (0.5)
↓
Dense (Sigmoid)
```

### Why SimpleRNN?

The model deliberately uses **SimpleRNN** to:

* Understand basic sequence modeling
* Highlight vanishing gradient issues
* Compare against more advanced RNN variants in future work

---

## ⚙️ Training Details

* **Loss function**: Binary Crossentropy
* **Optimizer**: Adam (learning rate = 0.0003)
* **Batch size**: 32
* **Sequence length**: 100 tokens
* **EarlyStopping**:

  * Monitored on validation accuracy
  * Prevents overfitting
  * Restores best model weights

---

## ✅ Observed Strengths

The SimpleRNN model performs **well on positive sentiment**, especially when reviews contain strong positive keywords.

### Examples:

```
"Absolutely loved it" → Positive (0.986)
"👌👌👌 masterpiece" → Positive (0.990)
"This movie was fantastic" → Positive (0.908)
```

This indicates the model successfully learns **short-term word-level sentiment patterns**.

---

## ⚠️ Observed Limitations

The model **struggles with negative sentiment**, particularly in cases involving:

* Negation (e.g., *"not good", "doesn't look nice"*)
* Strong negative expressions
* Slang and informal language
* Sarcasm or contextual meaning

### Examples:

```
"This movie is bad and it doesn't look nice" → Positive (0.908)
"Worst film ever!!!" → Positive (0.709)
```

---

## 🔍 Technical Explanation of Limitations

SimpleRNN uses a **single hidden state**, which makes it difficult to:

* Retain long-term dependencies
* Handle negation effectively
* Capture sentence-level semantics

As sequences grow longer, earlier information fades due to the **vanishing gradient problem**, causing the model to rely more on isolated word presence than full contextual meaning.

This behavior is **expected and well-documented** in NLP research.

---

## 🎓 Educational Value

This project serves as a **learning-focused implementation** that:

* Demonstrates the full NLP deep learning workflow
* Highlights architectural limitations of SimpleRNN
* Provides a strong baseline for comparison with LSTM/GRU models

---

## 🚀 Future Improvements

Potential enhancements include:

* Replacing SimpleRNN with **LSTM or GRU**
* Using **Bidirectional RNNs**
* Adding **pretrained embeddings** (GloVe, Word2Vec)
* Preserving punctuation and emojis for richer sentiment cues
* Performing threshold calibration for class imbalance

---

## 🧪 Deployment

The model is deployed using **Streamlit**, allowing users to input any movie review and receive:

* Sentiment classification (Positive / Negative)
* Prediction confidence score

---

## 📌 Conclusion

This project successfully demonstrates an end-to-end sentiment analysis system using SimpleRNN. While the model performs reliably for positive sentiment detection, its difficulty in handling negative and context-dependent sentiment highlights the inherent limitations of basic RNN architectures. These findings reinforce the motivation for using more advanced recurrent models in real-world NLP applications.

---

## 👤 Author

**Anish Tirumala Venkata**
M.S. in Computer Science
University of Florida

