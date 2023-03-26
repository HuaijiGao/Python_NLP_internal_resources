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

$$ \hat{P}(c_j) = \frac{doccount(C = c_j)}{N_{doc}} \tag{8}$$

$$ \hat{P}(w_i|c_j) = \frac{count(w_i, c_j)}{\sum_{w \in V}count(w, c_j)} \tag{9}$$

### Parameter estimation

fraction of times word $w_i$ appears among all words in documents of topic $c_j$

$$ \hat{P}(w_i|c_j) = \frac{count(w_i, c_j)}{\sum_{w \in V}count(w, c_j)} $$

• Create mega-document for topic j by concatenating all docs in this topic
	• Use frequency of w in mega-document

### Problem with Maximum Likelihood

• What if we have seen no training documents with the word fantastic and classified in the topic positive (thumbs-up)?

$$ \hat{P}("fantastic"|positive) = \frac{count("fantastic", positive)}{\sum_{w \in V}count(w, positive)} = 0$$

• Zero probabilities cannot be conditioned away, no matter the other evidence!

$$ c_{MAP} = argmax_c \hat{P}(c) \prod_i \hat{P}(x_i|c) $$

### Laplace (add-1) smoothing for Naïve Bayes

$$
\begin{align*}
    \hat{P}(x_i|c) &= \frac{count(w_i, c)+1}{\sum_{w \in V}(count(w, c)+1)} \\
    			   &= \frac{count(w_i, c)+1}{\sum_{w \in V}count(w, c)+|V|}
\end{align*}
\tag{10}
$$

### Unknown words
• What about unknown words
	• that appear in our test data
	• but not in our training data or vocab
• We ignore them
	• Remove them from the test document!
	• Pretend they weren't there!
	• Don't include any probability for them at all.
• Why don't we build an unknown word model?
	• It doesn't help: knowing which class has more unknown words is not generally a useful thing to know!

### Stop words
• Some systems ignore another class of words:
• Stop words: very frequent words like the and a.
	• Sort the whole vocabulary by frequency in the training, call the top 10 or 50 words the stopword list.
	• Now we remove all stop words from the training and test sets as if they were never there.
• But in most text classification applications, removing stop words don't help, so it's more common to not use stopword lists and use all the words in naive Bayes

### Multinomial Naïve Bayes: Learning

• From training corpus, extract Vocabulary
• Calculate $P(c_j)$ terms
```
for each c_j in C do
    docs_j ← all docs with class =c_j
    P(c_j) ← |docs_j| / |total # documents|
```


• Calculate $P(w_k | c_j)$ terms
```
Text_j ← single doc containing all docs_j
for each word w_k in Vocabulary
    n_k ← # of occurrences of w_k in Text_j
    P(w_k|c_j) ← (n_k +α) / (n + α|Vocabulary|)
```

### Multinomial Naïve Bayes: Classification

• Given a new document d, tokenize it into words
• Calculate class scores using log probabilities


