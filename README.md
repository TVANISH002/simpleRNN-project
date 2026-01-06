## 🎬 IMDB Sentiment Analysis using Simple RNN
Deep learning NLP project focused on understanding how basic recurrent neural networks
handle real-world text data — including where and why they fail.

---

### Why this project
Most sentiment analysis projects jump directly to LSTM or GRU models and report accuracy.
This project intentionally takes a **different approach**.

The goal is to:
- Build an end-to-end NLP pipeline using a **SimpleRNN**
- Observe its behavior on real movie reviews
- Analyze strengths, failure modes, and architectural limitations

This project emphasizes **model understanding and error analysis**, not just performance.

---

### Objective
- Build a complete NLP workflow: preprocessing → training → inference  
- Use SimpleRNN deliberately (instead of LSTM/GRU) for educational insight  
- Study differences in model behavior on positive vs negative sentiment  
- Deploy the trained model using Streamlit for real-time predictions  

---

### Dataset
- Dataset: IMDB Movie Reviews (Keras built-in dataset)
- Total samples: 50,000  
  - 25,000 training  
  - 25,000 testing  
- Task: Binary sentiment classification  
  - `1` → Positive  
  - `0` → Negative  
- Vocabulary size: Top 10,000 most frequent words  
- Sequence length: 100 tokens  

---

### Model architecture (SimpleRNN)
- Embedding layer (128 dimensions)  
- SimpleRNN layer (128 units, `tanh` activation)  
- Dropout (0.5)  
- Dense output layer (`sigmoid`)  

**Why SimpleRNN?**
- To understand basic sequence modeling  
- To highlight vanishing gradient issues  
- To establish a baseline for future comparison with LSTM/GRU models  

---

### Training details
- Loss function: Binary Crossentropy  
- Optimizer: Adam (learning rate = 0.0003)  
- Batch size: 32  
- EarlyStopping:
  - Monitored on validation accuracy  
  - Restores best model weights  

---

### Observed strengths
The model performs well on **short, strongly positive reviews**, where sentiment is
clearly indicated by local keywords.

**Examples:**
- “Absolutely loved it” → Positive (0.986)  
- “👌👌👌 masterpiece” → Positive (0.990)  
- “This movie was fantastic” → Positive (0.908)  

This indicates the model successfully captures **short-term word-level sentiment cues**.

---

### Observed limitations
The model struggles with **negative and context-dependent sentiment**, especially when:
- Negation is involved (e.g., “not good”, “doesn’t look nice”)  
- Reviews are longer or more descriptive  
- Sarcasm or informal language appears  

**Examples:**
- “This movie is bad and it doesn’t look nice” → Positive (0.908)  
- “Worst film ever!!!” → Positive (0.709)  

---

### Technical explanation
SimpleRNN maintains a single hidden state, which makes it difficult to:
- Retain long-term dependencies  
- Handle negation effectively  
- Capture sentence-level semantics  

As sequences grow longer, early information fades due to the
**vanishing gradient problem**, causing the model to rely on isolated word presence
rather than full contextual meaning.

This behavior is expected and well-documented in NLP research.

---

### Educational value
This project:
- Demonstrates a full NLP deep learning pipeline  
- Highlights real architectural limitations of SimpleRNN  
- Provides a clear baseline for more advanced recurrent models  
- Emphasizes diagnosis and reasoning over raw accuracy  

---

### Future improvements
- Replace SimpleRNN with LSTM or GRU  
- Use Bidirectional RNNs for richer context  
- Add pretrained embeddings (GloVe, Word2Vec)  
- Preserve punctuation and emojis for sentiment cues  
- Calibrate prediction thresholds for class imbalance  

---

### Deployment
The model is deployed using **Streamlit**, allowing users to:
- Enter any movie review  
- Receive sentiment classification (Positive / Negative)  
- View prediction confidence scores  

---

### Conclusion
This project successfully demonstrates an end-to-end sentiment analysis system using
SimpleRNN. While the model performs reliably for positive sentiment detection, its
difficulty in handling negation and long-range dependencies highlights the inherent
limitations of basic RNN architectures and reinforces the motivation for using
LSTM/GRU models in real-world NLP applications.
