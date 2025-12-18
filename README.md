# Legal-BERT Fine-Tuning for Contract Clause Classification

## 1. Introduction

Contracts are long legal documents written in formal and complex language.
Understanding and categorizing contract clauses manually requires legal expertise and significant time.
Automating this process using Natural Language Processing (NLP) helps reduce human effort and improves consistency.

This project focuses on fine-tuning Legal-BERT to classify individual contract clauses into predefined clause types such as termination, liability, governing law, confidentiality, and others.

The emphasis of this repository is model understanding, training, and evaluation, not application development.

## 2. Why Clause-Level Classification?
Legal documents are typically very long.
Classifying an entire contract as a single label hides important information.

Clause-level classification:
- Improves precision
- Reduces ambiguity
- Allows fine-grained legal analysis
- Enables downstream tasks like risk detection and clause comparison
- Each clause is treated as an independent semantic unit.

## 3. What is BERT?
BERT (Bidirectional Encoder Representations from Transformers) is a transformer-based language model introduced by Google.

### Key ideas behind BERT:
- Bidirectional context: Unlike traditional models that read text left-to-right, BERT reads text from both directions simultaneously.
- Self-attention mechanism: Each word attends to all other words in a sentence, allowing BERT to understand long-range dependencies.
- Pretraining + Fine-tuning: BERT is pretrained on large text corpora and then fine-tuned for specific downstream tasks.

## 4. How BERT Understands Language (Conceptual)
BERT converts text into tokens and then maps each token into a vector representation.
Through multiple transformer layers:
- Syntax is captured in lower layers
- Semantics and meaning are captured in higher layers
  
For classification tasks:
- A special token [CLS] is added at the beginning
- The final hidden state of [CLS] represents the entire sentence
- This representation is passed to a classification head

## 5. Limitations of General BERT for Legal Text
General BERT models are trained on everyday English text such as books, news articles, and Wikipedia, which is very different from legal writing. Legal documents usually contain long and complex sentences, formal and sometimes archaic words, and many domain-specific legal terms. They also follow repetitive and structured patterns that are uncommon in general language. Because of this mismatch, a general BERT model may misunderstand the meaning of legal terms, overlook important contractual conditions, or fail to capture subtle legal nuances. As a result, its predictions can be inaccurate when applied to contracts or legal clauses. These limitations make it necessary to use domain-specific models, such as Legal-BERT, which are trained on legal texts and are better suited to understand legal language correctly.

## 6. What is Legal-BERT?
Legal-BERT is a specialized version of BERT that is pretrained on legal texts such as contracts, court decisions, and legislation. While it keeps the same architecture as BERT, it learns legal-specific vocabulary, sentence structures, and domain semantics during pretraining. Because of this legal-focused training, Legal-BERT understands legal language more accurately and performs better on legal NLP tasks like clause classification and contract analysis.

## 7. Problem Statement

The objective of this project is to build and train a machine learning model that can automatically analyze legal contract clauses. The model takes a **single contract clause** as input and predicts the **type of clause** it belongs to, such as termination, liability, or governing law. Along with the predicted clause type, the model also outputs a **confidence score** that indicates how certain the model is about its prediction. This helps in assessing the reliability of the prediction and identifying clauses that may require human review.

### Example
Input  
`Either party may terminate this Agreement upon thirty days notice.`  
Output  
`Termination`

## Model Training Results

The table below shows the performance of the Legal-BERT model across training epochs.

| Epoch | Training Loss | Validation Loss | Micro F1 | Macro F1 | Precision | Recall |
|------:|---------------|-----------------|----------|----------|-----------|--------|
| 1 | 0.050100 | 0.047102 | 0.679245 | 0.186361 | 0.972125 | 0.521983 |
| 2 | 0.029200 | 0.029068 | 0.840874 | 0.361371 | 0.920935 | 0.773620 |
| 3 | 0.022900 | 0.024962 | 0.845309 | 0.397758 | 0.905882 | 0.792329 |
| 4 | 0.018000 | 0.022965 | 0.853767 | 0.467348 | 0.901247 | 0.811038 |
| 5 | 0.017300 | 0.022206 | 0.853333 | 0.473992 | 0.903766 | 0.808232 |

---

## 8. Explanation of Evaluation Metrics

**Training Loss**  
Training loss measures how well the model fits the training data. A decreasing training loss across epochs indicates that the model is learning meaningful patterns from the data.

**Validation Loss**  
Validation loss shows how well the model generalizes to unseen data. The steady decrease and stabilization of validation loss suggest that the model is not overfitting.

**Micro F1 Score**  
Micro F1 calculates precision and recall globally across all classes by counting total true positives, false positives, and false negatives. It is influenced by dominant classes and reflects overall classification performance.

**Macro F1 Score**  
Macro F1 computes the F1 score independently for each class and then averages them. This metric is especially important for legal clause classification because it evaluates how well the model performs on **all clause types**, including less frequent ones.

**Precision**  
Precision indicates how many of the clauses predicted as a certain type were actually correct. High precision means the model makes fewer false positive predictions.

**Recall**  
Recall measures how many actual clauses of a given type were correctly identified. Higher recall indicates that the model misses fewer relevant clauses.

---

## Key Observations

- Training and validation losses decrease consistently, indicating stable learning.
- Micro F1 improves significantly, showing strong overall performance.
- Macro F1 increases steadily, demonstrating better handling of class imbalance.
- High precision with improving recall indicates reliable and confident predictions.

Overall, the results show that the Legal-BERT model learns legal clause patterns effectively and generalizes well to unseen contract clauses.

### CUAD Dataset

The Contract Understanding Atticus Dataset (CUAD) is a publicly available legal dataset designed for contract analysis tasks. It contains real-world business contracts annotated at the clause level with fine-grained legal labels such as termination, liability, governing law, and confidentiality. CUAD is widely used in legal NLP research and provides high-quality, expert-labeled data, making it well suited for training and evaluating models on legal clause classification tasks.

## 9. Future Improvements

- **Hybrid Rule-Based Integration**  
  Combine the trained model with deterministic rule-based systems to handle critical legal constraints such as notice periods, liability caps, and unilateral termination clauses, improving reliability and reducing risk.

- **Clause Similarity and Comparison**  
  Use sentence embeddings to identify similar clauses across different contracts, enabling contract-to-contract comparison and deviation analysis from standard templates.

- **Explanation and Reasoning Models**  
  Integrate explanation models such as T5 to generate plain-English summaries and risk explanations for each clause, improving transparency and user trust.

- **Multilingual Contract Support**  
  Extend the system to support multilingual contracts by incorporating multilingual language models, allowing analysis of contracts written in languages other than English.

