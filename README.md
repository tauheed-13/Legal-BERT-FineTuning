# Legal-BERT Fine-Tuning for Contract Clause Classification

## Introduction
Contracts are long, complex, and written in highly specialized legal language. 
Manually reviewing and categorizing contract clauses is time-consuming and error-prone. 
Natural Language Processing (NLP) models, especially transformer-based architectures, 
have shown strong performance in understanding legal text.

This repository demonstrates how **Legal-BERT** can be fine-tuned for **contract clause classification** at the clause level.

---

## What is BERT?
**BERT (Bidirectional Encoder Representations from Transformers)** is a transformer-based language model introduced by Google.
Unlike traditional models, BERT reads text **bidirectionally**, meaning it understands the context from both left and right sides of a word.

Key characteristics of BERT:
- Bidirectional context understanding
- Pretrained on large text corpora
- Can be fine-tuned for downstream NLP tasks such as classification, NER, and QA

---

## What is Legal-BERT?
**Legal-BERT** is a domain-specific variant of BERT trained on **legal corpora**, including:
- Contracts
- Legislation
- Court cases

Because legal language differs significantly from general English, Legal-BERT captures:
- Legal terminology
- Formal sentence structures
- Domain-specific semantics

This makes Legal-BERT significantly more effective than general BERT for legal NLP tasks.

---

## Why Legal-BERT is Popular in Legal NLP
Legal-BERT is widely used because:
- It is pretrained on real legal documents
- It improves accuracy on legal text classification tasks
- It generalizes better to contracts than generic language models
- It is stable and reliable for production use

Legal-BERT has been adopted in research and industry for:
- Contract analysis
- Clause extraction
- Legal document classification
- Risk detection systems

---

## Problem Statement
The objective of this project is to **classify contract clauses into predefined clause types** such as:
- Termination
- Governing Law
- Non-Compete
- Liability
- Confidentiality
- Payment Terms

The classification is performed at the **clause level** to avoid ambiguity and improve interpretability.

---

## Dataset
The dataset consists of contract clauses extracted from real-world agreements.
Each clause is labeled with a specific clause type.

**Format:**
```json
{
  "text": "Either party may terminate this Agreement upon thirty days notice.",
  "label": "Termination"
}
