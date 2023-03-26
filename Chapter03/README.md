# Revision Notes - Chapter 03: NLP Basic Tasks II

## Word Normalization and other issues (Cont'd from Chapter02)

### Normalization
- Normalize terms for better matching in Information Retrieval
- Define equivalence classes of terms
- Asymmetric expansion: different search results based on input form

### Case folding
- Reduce all letters to lower case, except when case is important (e.g., sentiment analysis, MT, Information extraction)

### Lemmatization
- Represent words as their shared root or dictionary headword form
- Done by Morphological Parsing
- Morphemes: Stems (core meaning-bearing units) and Affixes (with grammatical functions)

## Stemming
- Reduce terms to stems, crudely chopping off affixes
- Language dependent (e.g., automate, automatic, automation → automat)

### Porter Stemmer
- Cascade of rewrite rules run in series
- Sample rules:
  - ATIONAL $\rightarrow$ ATE (e.g., relational $\rightarrow$ relate)
  - ING $\rightarrow$ ε if stem contains vowel (e.g., motoring $\rightarrow$ motor)
  - SSES $\rightarrow$ SS (e.g., grasses $\rightarrow$ grass)

### Dealing with complex morphology
- Necessary for many languages, like Turkish

### Sentence Segmentation
- Deciding whether a period is part of a word or a sentence-boundary marker
- Use abbreviation dictionary and rules based on tokenization

### Decision Trees
- General decision tree for determining E-O-S (end of sentence)
- Numeric features and case features
- Decision trees implemented as if-then-else statements
- Structure usually learned by machine learning from a training corpus

## Introduction to N-grams

### Probabilistic Language Models
- Assign probability to a sentence
- Compute the probability of a sentence or sequence of words: P(W) = P(w1,w2,w3,w4,w5…wn)
- Compute the probability of an upcoming word: P(w5|w1,w2,w3,w4)

### Chain Rule applied to compute joint probability of words in sentence
- P(w1w2…wn) = Π_i P(wi | w1w2…wi−1)
- Simplifying assumption: Markov Assumption
- Unigram, Bigram, Trigram, N-gram models

## Estimating N-gram Probabilities

### Estimating bigram probabilities
- Maximum Likelihood Estimate: P(wi | wi−1) = count(wi−1,wi )/ count(wi−1)

### Practical Issues
- Use log space to avoid underflow and for faster computation
