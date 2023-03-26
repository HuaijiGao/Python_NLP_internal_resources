# Chapter 04: NLP Text Classification I

## The Task of Text Classification

### Text Classification: Definition
- Input: a document $d$ and a fixed set of classes $C = {c_1, c_2, \cdots, c_J}$
- Output: a predicted class $c \in C$

### Text Classification Examples
- Sentiment analysis
- Spam detection
- Authorship identification
- Language Identification
- Assigning subject categories, topics, or genres

## Classification Methods

### Hand-coded Rules
- Rules based on combinations of words or other features
- Accuracy can be high if rules carefully refined by an expert
- Building and maintaining these rules is expensive

### Supervised Machine Learning
- Input: a document $d$, a fixed set of classes $C = {c_1, c_2, \cdots, c_J}$, a training set of $m$ hand-labeled documents $(d_1,c_1), \cdots, (d_m,c_m)$
- Output: a learned classifier $\gamma:d \rightarrow c$
- Classifiers: Naïve Bayes, Logistic regression, Neural networks, k-Nearest Neighbors, etc.

## Naïve Bayes

### Naive Bayes Intuition
- Simple classification method based on Bayes rule
- Relies on the bag of words representation of documents

### Bayes' Rule Applied to Documents and Classes
- For a document $d$ and a class $c$

$$ P(c | d) = \frac{P(d | c)P(c)}{P(d)} $$

### Naïve Bayes Classifier

$$
\begin{align*}
    c_{MAP} &= \arg\max_{c \in C} P(c|d) \\
      		&= \arg\max_{c \in C} \frac{P(d | c)P(c)}{P(d)}\\
      		&= \arg\max_{c \in C} P(d |c)P(c)\\
      		&= \arg\max_{c \in C} P(x_1, x_2, \cdots, x_n | c)P(c)
\end{align*}
\tag{1}
$$

### Multinomial Naive Bayes Independence Assumptions

$$ P(x_1, x_2, \cdots, x_n | c) \tag{2}$$

- **Bag of Words assumption**: Assume position doesn't matter
- **Conditional Independence**: Assume the feature probabilities $P(x_i|c_j)$ are independent given the class $c$.

$$ P(x_1, x_2, \cdots, x_n | c) = P(x_1 |c) \cdot P(x_2 |c) \cdot \cdots \cdot P(x_n |c) \tag{3}$$

### Multinomial Naive Bayes Classifier

$$ c_{NB} = \arg\max_{c \in C} P(c_j) \prod_{x \in X} P(x | c) \tag{5}$$

### Applying Multinomial Naive Bayes Classifiers to Text Classification

$$ c_{NB} = \arg\max_{c_j \in C} [log P(c_j) + \sum_{i \in positions} log P(x_i | c_j)] \tag{7}$$

## Naïve Bayes: Learning

### Learning the Multinomial Naive Bayes Model
- Maximum likelihood estimates using frequencies in the data

$$ \hat{P}(c_j
