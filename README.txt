# Liquid-Liquid Phase Separation (LLPS) Prediction in *Neurospora crassa*

This repository contains a computational workflow based on Machine Learning and Natural Language Processing (NLP) techniques to predict the propensity of proteins to undergo **Liquid-Liquid Phase Separation (LLPS)**. 

The trained model is applied to scan the entire proteome of the model fungus *Neurospora crassa*, and the results are validated by cross-referencing them with the established bioinformatics tool **parSe v2**.

## Workflow and Methodology

The project is structured into the following main stages within the primary Jupyter Notebook:

1. **Dataset Preprocessing:**
   * Utilizes experimentally validated positive protein sequences (known to undergo LLPS) and a set of negative sequences.
   * Applies random undersampling to the negative set to create a perfectly balanced dataset.
2. **Feature Extraction (Vectorization):**
   * Amino acid sequences are split into 3-mer "words" using a sliding window approach.
   * A **Word2Vec (Skip-gram)** model is trained to generate 200-dimensional vector embeddings for each k-mer, capturing local biological context.
   * **Vaswani's positional encoding** (commonly used in Transformer architectures) is integrated to retain the global sequential order of the protein.
3. **Model Training:**
   * Implements a **Gradient Boosting Decision Tree (GBDT)** classifier.
   * The model is evaluated using 10-fold Stratified Cross-Validation, achieving an **average Accuracy and F1-Score of ~96%**.
4. ***N. crassa* Proteome Scanning:**
   * Processes over 10,200 sequences from the target proteome using the established vectorization pipeline.
   * The model computes an LLPS probability score for every protein.
5. **Validation with parSe v2:**
   * Extracts Phase-Separating Intrinsically Disordered Regions (PS IDRs) identified by the parSe v2 algorithm.
   * Performs statistical and visual comparisons (Boxplots, Scatter Plots, Venn Diagrams) to corroborate the agreement between the ML model's predictions and parSe v2 findings.

## Technologies and Libraries

To run this project, you will need Python 3 and the following libraries:

* **Data Manipulation:** `pandas`, `numpy`
* **Bioinformatics:** `biopython`
* **Machine Learning / NLP:** `gensim` (Word2Vec), `scikit-learn` (GradientBoostingClassifier, StratifiedKFold)
* **Data Visualization:** `matplotlib`, `seaborn`, `matplotlib-venn`

## Project Files

* `LLPS_N_CRASSA.ipynb`: The main Jupyter Notebook containing all the source code, from data preprocessing to visual analysis.
* `positivas.txt` / `negativas.txt`: Text files containing the sequences used to train the model. *(Note: Ensure these are uploaded unless restricted by file size/privacy).*
* `proteoma_ncrassa.fasta`: FASTA file containing the target proteome extracted from UniProt.
* `parSe v2/NCRASSA_filtered.FASTA`: File containing the PS IDR results extracted by the parSe v2 algorithm.

