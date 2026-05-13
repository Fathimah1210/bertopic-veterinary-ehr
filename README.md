# BERTopic Veterinary EHR Analysis

Topic modeling and statistical analysis of veterinary consultation narratives from the SAVSNET database.

## Overview

This project applies unsupervised machine learning to discover hidden patterns in veterinary clinical notes (veterinary medical records) using BERTopic, a modern transformer-based topic modeling method. This implementation draws on the methodology of Noble et al. (2026), who applied a similar approach to over one million dog medical records in the UK.

Veterinarians create free-text narrative notes detailing symptoms, examinations, and treatments after each consultation at a veterinary clinic. While this data is incredibly rich in information, it is difficult to manually evaluate on a large scale.

This method aims to answer the question of whether an algorithm, without prior labeling, can automatically identify significant clinical problems from thousands of such records.

## Dataset

Source: SAVSNET (Small Animal Veterinary Surveillance Network)
URL: https://www.liverpool.ac.uk/savsnet/

Dataset characteristics:
- Total records: 4,415 consultations
- Dog records analyzed: 2,771 (after cleaning)
- Time period: March 2014 - October 2019
- Species: Dogs (65.8%), cats, rabbits, and other animals
- Clinical categories: 10 Main Presenting Complaint (MPC) types

Data fields:
- SAVSNET_consult_id: Consultation identifier
- Narrative: Clinical narrative text
- SAVSNET MPC: Main Presenting Complaint
- Consult_date: Consultation date and time
- Species: Animal species

## Methods

### BERTopic Configuration
- Embedding model: all-MiniLM-L6-v2
- Dimensionality reduction: UMAP (5 components)
- Clustering algorithm: HDBSCAN (min_cluster_size=10)
- Vectorization: c-TF-IDF with unigrams and bigrams
- Topics discovered: 47 topics (1 outlier topic)

### Quality Metrics
- Coherence score (c_v): 0.4838
  - Good topics (≥0.7): 12.8%
  - Acceptable topics (0.5-0.7): 34.0%
  - Poor topics (<0.5): 53.2%

### Statistical Analysis
Odds ratios calculated with 95% confidence intervals:
- Formula: OR = (a × d) / (b × c)
- Standard error: SE = √(1/a + 1/b + 1/c + 1/d)
- 95% CI: exp(log(OR) ± 1.96 × SE)
- Continuity correction: +1 added to all cells
- Significant results: 46 associations (46% of 100 comparisons)

## Results

Top associations by Odds Ratio:
- Respiratory + cough topic: OR = 576.00 (95% CI: 121.85-2722.93)
- Gastroenteric + food topic: OR = 161.96 (95% CI: 79.58-329.60)
- Tumour + lump topic: OR = 58.87 (95% CI: 27.93-124.08)
- Post-op + wound topic: OR = 45.92 (95% CI: 26.02-81.04)
- Trauma + pain topic: OR = 32.59 (95% CI: 18.32-57.99)

```
python >= 3.8
bertopic
sentence-transformers
umap-learn
hdbscan
scikit-learn
gensim
plotly
pandas
numpy
```

Last Updated: May 13, 2026
