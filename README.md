## Instructions for CB2110 - LAB4

!CHANGE: [Link Google colab notebook.](https://colab.research.google.com/drive/1eQdzOJdNoMAbogB9PqgLW30WgJRqCTKG)

# CB2110 - LAB4

## Integrative analysis for multi-omics data

## Important - Read before you start the lab

**Before you start reading the introduction and instructions**, *execute* the first cell block which will load the MOFA R package, which is essential for this lab, this should take between ~20-30 min if using Google Colab, (less if you install through your local PC or MAC in R Studio).

### Instructions on how to hand in the lab

Questions are distributed throughout this notebook. You can view where the questions are by pressing on the "table of contents" icon right below the Google Colab icon ("outline" in R Studio), which is situated on the top left on this page (right in R Studio).

You should extract the questions and your answers (including any plots or code if requested) in the format of:

First name: 
Second name: 
Date: 

Question 1: [re-type the question here]
Answer: [your answer here]

Question 2: [re-type the question here]
Answer: [your answer here]

...

Question 10: [re-type the question here]
Answer: [your answer here]

Bonus question: [re-type the question here]
Answer: [your answer here]

Then submit your answers to the Canvas as a PDF file.

Good luck with all the questions! Reach out to the TAs if you have any questions regarding this lab.

## Introduction

The content of the computer lab session focuses on applying tools for **multi-omics data integration** to identify potential biomarkers and to be able to interpret the results from the analyses.

### Key Concepts

* Integrating different omics data - Focusing on an unsupervised model such as Multi-Omics Factor Analysis (MOFA)
* Early, middle and late integration - Applying middle integration using MOFA
* Latent factors and factor weights - Understanding how latent factors capture global sources of variability in the data and how factor weights relate features to factors

### Intended learning outcomes (ILOs)

After this computer lab, you will be able to:

1. Demonstrate the ability to implement and execute tools to integrate multi-omics data
2. Demonstrate the ability to implement and execute visualization of complex datasets
3. Demonstrate knowledge on how to interpret the visualization of multi-omics data
4. Identify relevant issues of complexity in integrating multi-omics data

### Background

The data we are using comes from a multi-omics study on breast cancer, published in The Journal of Nature: ["**Comprehensive molecular portraits of human breast tumours
**"](https://www.nature.com/articles/nature11412) by The Cancer Genome Atlas Network (2012).

This notebook draws its inspiration from a MOFA study that used the aforementioned study and published their work in Molecular Systems Biology: ["**Multi-Omics Factor Analysis-a framework for unsupervised integration of multi-omics data sets**"](https://pubmed.ncbi.nlm.nih.gov/29925568/) by Richard Argelaguet et al (2018).

## Goals of this session

1. a) Pair yourself into groups of two. b) Make your own copy of this notebook.
2. a) **Answer question 1-10** presented in this notebook in a word file. b) Mark it with the date and your names (g.e., "20240912_EmilJohanssonJosefineKenrick"). c) Export it to PDF.
3. Submit your notebook to the Canvas.

# Unsupervised clustering and latent factors

While you are installing the necessary R packages for this lab, it's recommended that you'll take a few minutes to understand more what latent factors and factor weights are. Here are a few explanations:

**Latent factors**
The MOFA factors capture the global sources of variability in the data. Mathematically, each factor ordinates cells along a one-dimensional axis centered at zero. The value per se is not interpretable, only the relative positioning of samples is important. Samples with different signs manifest opposite “effects” along the inferred axis of variation, with higher absolute value indicating a stronger effect. Note that the interpretation of factors is analogous to the interpretation of the principal components in PCA.

**Factor weights/loadings**
The weights (aka. loadings) provide a score for how strong each feature relates to each factor, hence allowing a biological interpretation of the latent factors. Features with no association with the factor have values close to zero, while genes with strong association with the factor have large absolute values. The sign of the weight indicates the direction of the effect: a positive weight indicates that the feature has higher levels in the cells with positive factor values, and vice versa.

**More information on latent factors**
[MOFA FAQ](https://biofam.github.io/MOFA2/faq.html)
[Sciencedirect on latent factors](https://www.sciencedirect.com/topics/mathematics/latent-factor)
[Wiki page on Factor analysis](https://en.wikipedia.org/wiki/Factor_analysis)