# Biomedical Knowledge Graph Extraction with BioBERT and SpERT
A BIOS 740 final project

Spring 2026

## Overview

This repository contains the implementation and experiments for the BIOS 740 final project on biomedical knowledge graph extraction. The project investigates transformer-based named entity recognition (NER) and relation extraction (RE) using the SpERT framework combined with BioBERT embeddings on biomedical literature datasets derived from PubMed abstracts.

The primary goal is to extract structured biomedical triplets of the form:

(subject, relation, object)

from scientific text and use them to construct biomedical knowledge graphs.

---

## Project Objectives

* Build a biomedical information extraction pipeline
* Perform named entity recognition (NER)
* Perform biomedical relation extraction (RE)
* Train and evaluate transformer-based RE models
* Compare performance across biomedical domains
* Investigate transfer learning and domain adaptation challenges

---

## Datasets

Two biomedical datasets were used in this project:

### ADKG — Alzheimer’s Disease Knowledge Graph

* 8,031 biomedical sentences
* Focused on Alzheimer’s disease and neurodegenerative disorders

### MDKG — Mental Disorder Knowledge Graph

* 6,678 biomedical sentences
* Covers schizophrenia, depression, bipolar disorder, PTSD, OCD, and related disorders

Both datasets contain manually annotated:

* biomedical entities
* semantic relations
* entity spans
* relation triplets

---

## Model Architecture

This project uses:

### BioBERT

A transformer language model pretrained on large-scale biomedical literature.

Paper:
Lee et al., *BioBERT: a pre-trained biomedical language representation model for biomedical text mining* (2020)

### SpERT

A span-based joint entity and relation extraction framework.

Paper:
Eberts and Ulges, *Span-based Joint Entity and Relation Extraction with Transformer Pre-training* (2019)

---

## Repository Structure

```text
.
├── data/
│   ├── raw datasets
│   ├── converted SpERT datasets
│
├── notebooks/
│   ├── check_data.ipynb
│   ├── convert_to_spert.ipynb
│   ├── train_adkg.ipynb
│   ├── train_mdkg.ipynb
│   ├── cross_domain_transfer.ipynb
│
├── logs/
│   ├── training logs
│
├── models/
│   ├── saved BioBERT + SpERT checkpoints
│
├── spert/
│   ├── modified SpERT framework
│
└── README.md
```

---

## Installation

Create a Python virtual environment:

```bash
python3 -m venv venv
source venv/bin/activate
```

Install required packages:

```bash
pip install torch torchvision torchaudio
pip install transformers datasets sentencepiece safetensors
pip install jupyter pandas numpy matplotlib scikit-learn
```

Clone the SpERT repository:

```bash
git clone https://github.com/lavis-nlp/spert.git
```

---

## Running the Project

### 1. Validate Datasets

Open:

```text
check_data.ipynb
```

This notebook:

* validates entity spans
* checks relation consistency
* analyzes dataset statistics

---

### 2. Convert Datasets to SpERT Format

Open:

```text
convert_to_spert.ipynb
```

This notebook:

* tokenizes biomedical text
* converts annotations into SpERT format
* generates train/dev/test JSON files

---

### 3. Train ADKG Model

Open:

```text
train_adkg.ipynb
```

This notebook trains:

* BioBERT + SpERT on ADKG

---

### 4. Train MDKG Model

Open:

```text
train_mdkg.ipynb
```

This notebook trains:

* BioBERT + SpERT on MDKG

---

### 5. Cross-Domain Transfer Learning

Open:

```text
cross_domain_transfer.ipynb
```

This notebook explores:

* transfer learning between ADKG and MDKG
* ontology mismatch challenges
* cross-domain biomedical RE generalization

---

## Experimental Results

| Dataset | NER Micro-F1 | NER Macro-F1 | RE Micro-F1 (w/o NEC) | RE Macro-F1 (w/o NEC) | RE Micro-F1 (with NEC) | RE Macro-F1 (with NEC) |
| ------- | ------------ | ------------ | --------------------- | --------------------- | ---------------------- | ---------------------- |
| ADKG    | 69.42        | 57.40        | 41.63                 | 33.27                 | 36.84                  | 30.19                  |
| MDKG    | 79.72        | 69.58        | 54.23                 | 53.93                 | 47.84                  | 47.72                  |

Footnote:

* “Without NEC” evaluates relations using only relation type and entity span correctness.
* “With NEC” additionally requires correct entity type classification.

---

## Key Findings

* BioBERT + SpERT achieves strong biomedical NER performance
* Relation extraction is substantially more difficult than NER
* MDKG outperformed ADKG across most metrics
* Rare entity and relation classes remain challenging
* Cross-domain transfer learning is complicated by ontology mismatch and incompatible label spaces

---

## Hardware and Environment

Experiments were conducted on:

* UNC Longleaf GPU cluster
* Jupyter notebook environment
* PyTorch + HuggingFace Transformers

---

## References

* Devlin et al. (2019). *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding*
* Lee et al. (2020). *BioBERT: a pre-trained biomedical language representation model for biomedical text mining*
* Eberts and Ulges (2019). *Span-based Joint Entity and Relation Extraction with Transformer Pre-training*

---

## Author
Ashkan Habib
BIOS 740 Final Project
Biomedical Knowledge Graph Extraction using BioBERT and SpERT
