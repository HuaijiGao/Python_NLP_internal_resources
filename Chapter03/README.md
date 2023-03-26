# Chapter 03: NLP Basic Tasks II

## Word Normalization and other issues
***Revision for the last part of Chapter02***

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

## Evaluation and Perplexity

### Evaluation: How good is our model?
- Does our language model prefer good sentences to bad ones?
    - Assign higher probability to “real” or “frequently observed” sentences
        - Than “ungrammatical” or “rarely observed” sentences?
- We train parameters of our model on a training set.
- We test the model’s performance on data we haven’t seen.
    - A test set is an unseen dataset that is different from our training set, totally unused.
    - An evaluation metric tells us how well our model does on the test set.

### Extrinsic evaluation of N-gram models
- Best evaluation for comparing models A and B
    - Put each model in a task
        - spelling corrector, speech recognizer, MT system
    - Run the task, get an accuracy for A and for B
        - How many misspelled words corrected properly
        - How many words translated correctly
    - Compare accuracy for A and B

### Difficulty of extrinsic (in-vivo) evaluation of N-gram models
- Extrinsic evaluation
    - Time-consuming; can take days or weeks
- So
    - Sometimes use intrinsic evaluation: perplexity
    - Bad approximation
        - unless the test data looks just like the training data
        - So generally only useful in pilot experiments
    - But is helpful to think about.

### Intuition of Perplexity
- The Shannon Game:
    - How well can we predict the next word?
        - I always order pizza with cheese and ____
        - The 33rd President of the US was ____
        - I saw a ____
    - Unigrams are terrible at this game. (Why?)
- A better model of a text
    - is one which assigns a higher probability to the word that actually occurs

### Perplexity

The best language model is one that best predicts an unseen test set
    - Gives the highest P(sentence)
Perplexity is the inverse probability of the test set, normalized by the number of words:

$$ PP(W) = P(w_1 w_2 ... w_N)^{-\frac{1}{N}} = \sqrt[N]{\frac{1}{P(w_1 w_2 ... w_N)}} $$

Chain rule: 

$$ PP(W) = \sqrt[N]{ \prod_{t=n+1}^N \frac{1}{P(w_t | w_{t-n} \cdots w_{t-1})} } $$

For bigrams: 

$$ PP(W) = \sqrt[N]{ \prod_{t=n+1}^N \frac{1}{P(w_t | w_{t-1} )} } $$

Minimizing perplexity is the same as maximizing probability

### The Shannon Game intuition for perplexity
- From Josh Goodman
- Perplexity is weighted equivalent branching factor
- How hard is the task of recognizing digits ‘0,1,2,3,4,5,6,7,8,9’
    - Perplexity 10
- How hard is recognizing (30,000) names at Microsoft.
    - Perplexity = 30,000
- Let's imagine a call-routing phone system gets 120K calls and has to recognize
    - "Operator" (let's say this occurs 1 in 4 calls)
    - "Sales" (1in 4)
    - "Technical Support" (1 in 4)
    - 30,000 different names (each name occurring 1 time in the 120K calls)
    - What is the perplexity? Next slide

We get the perplexity of this sequence of length 120K by first multiplying 120K probabilities (90K of which are 1/4 and 30K of which are 1/120K), and then taking the inverse 120,000th root:

Perp = (¼ * ¼ * ¼* ¼ * ¼ * …. * 1/120K * 1/120K * ….)^(-1/120K)

But this can be arithmetically simplified to just N = 4: the operator (1/4), the sales (1/4), the tech support (1/4), and the 30,000 names (1/120,000):
Perplexity= ((¼ * ¼ * ¼ * 1/120K)^(-1/4) = 52.6

### Perplexity as branching factor

- Let’s suppose a sentence consisting of random digits
- What is the perplexity of this sentence according to a model that assigns P=1/10 to each digit?

### Lower perplexity = better model

- Training 38 million words, test 1.5 million words, WSJ

| N-gram Order | Unigram | Bigram | Trigram |
|---|---|---|---|
| Perplexity    | 962   | 170  | 109    |

## Generalization and zeros

### The Shannon Visualization Method
- Choose a random bigram (<s>, w) according to its probability
- Now choose a random bigram (w, x) according to its probability
- And so on until we choose </s>
- Then string the words together

### Shakespeare as corpus
- N=884,647 tokens, V=29,066
- Shakespeare produced 300,000 bigram types out of V^2= 844 million possible bigrams.
    - So 99.96% of the possible bigrams were never seen (have zero entries in the table)
- Quadrigrams worse: What's coming out looks like Shakespeare because it is Shakespeare

### The perils of overfitting
- N-grams only work well for word prediction if the test corpus looks like the training corpus
    - In real life, it often doesn’t
    - We need to train robust models that generalize!
    - One kind of generalization: Zeros!
        - Things that don’t ever occur in the training set
            - But occur in the test set

### Zeros
- Training set:
```
… denied the allegations
… denied the reports
… denied the claims
… denied the request
```

- Test set
```
… denied the offer
… denied the loan
```

P(“offer” | denied the) = 0

### Zero probability bigrams
- Bigrams with zero probability
    - mean that we will assign 0 probability to the test set!
- And hence we cannot compute perplexity (can’t divide by 0)!

## Smoothing: Add-one (Laplace) smoothing

### The intuition of smoothing (from Dan Klein)

- When we have sparse statistics:
```
P(w | denied the)
3 allegations
2 reports
1 claims
1 request
7 total
```

- Steal probability mass to generalize better
```
P(w | denied the)
2.5 allegations
1.5 reports
0.5 claims
0.5 request
2 other
7 total
```

### Add-one estimation
- Also called Laplace smoothing
- Pretend we saw each word one more time than we did
- Just add one to all the counts!
- MLE estimate: $ P_{MLE} (w_i | w_{i-1}) = \frac{c(w_{i-1}, w_i)}{ c(w_i-1) }$
- Add-1 estimate: $ P_{Add-1} (w_i | w_{i-1}) = \frac{c(w_{i-1}, w_i) + 1}{ c(w_i-1)+V }$

### Maximum Likelihood Estimates
- The maximum likelihood estimate
    - of some parameter of a model M from a training set T
    - maximizes the likelihood of the training set T given the model M
- Suppose the word “bagel” occurs 400 times in a corpus of a million words
- What is the probability that a random word from some other text will be “bagel”?
- MLE estimate is 400/1,000,000 = .0004
- This may be a bad estimate for some other corpus
    - But it is the estimate that makes it most likely that “bagel” will occur 400 times in a million word corpus.

### Add-1 estimation is a blunt instrument
- So add-1 isn’t used for N-grams:
    - There are other methods that perform better
- But add-1 is used to smooth other NLP models
    - For text classification
    - In domains where the number of zeros isn’t so huge.

### Unknown words: Open versus closed vocabulary tasks
- If we know all the words in advance
    - Vocabulary V is fixed
    - Closed vocabulary task
- Often we don’t know this
    - Out Of Vocabulary = OOV words
    - Open vocabulary task
- Instead: create an unknown word token <UNK>
    - Training of <UNK> probabilities
        - Create a fixed lexicon L of size V
        - At text normalization phase, any training word not in L changed to <UNK>
        - Now we train its probabilities like a normal word
    - At decoding time
        - If text input: Use UNK probabilities for any word not in training

