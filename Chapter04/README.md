# Chapter 04: NLP Text Classification I

|Table of Sections|
|--|
|:herb:  [The Task of Text Classification](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter04/README.md#the-task-of-text-classification)<br>:herb:  [Classification Methods](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter04/README.md#classification-methods)<br>:herb:  [Naïve Bayes](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter04/README.md#nave-bayes)<br>:herb:  [Naïve Bayes: Learning](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter04/README.md#nave-bayes-learning)<br>:herb:  [Binary Multinomial Naive Bayes Examples](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter04/README.md#binary-multinomial-naive-bayes-examples)<br>:herb:  [Naïve Bayes Others](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter04/README.md#nave-bayes-others)<br>:herb:  [Sentiment Classification](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter04/README.md#sentiment-classification)<br>:herb:  [Evaluation Metrics](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter04/README.md#evaluation-metrics)<br>:herb:  [Evaluation with More than Two Classes](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter04/README.md#evaluation-with-more-than-two-classes)<br>:herb:  [Avoiding Harms in Classification](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter04/README.md#avoiding-harms-in-classification)|

## The Task of Text Classification

### :sparkles: Text Classification: Definition
- Input: a document $d$ and a fixed set of classes $C =$ &#123; $c_1, c_2, \cdots, c_J$ &#125;
- Output: a predicted class $c \in C$

### :sparkles: Text Classification Examples
- Sentiment analysis
- Spam detection
- Authorship identification
- Language Identification
- Assigning subject categories, topics, or genres

## Classification Methods

### :sparkles: Hand-coded Rules
- Rules based on combinations of words or other features
- Accuracy can be high if rules carefully refined by an expert
- Building and maintaining these rules is expensive

### :sparkles: Supervised Machine Learning
- Input: a document $d$, a fixed set of classes $C =$ &#123; $c_1, c_2, \cdots, c_J$ &#125;, a training set of $m$ hand-labeled documents $(d_1,c_1), \cdots, (d_m,c_m)$
- Output: a learned classifier $\gamma:d \rightarrow c$
- Classifiers: Naïve Bayes, Logistic regression, Neural networks, k-Nearest Neighbors, etc.


|![image](https://user-images.githubusercontent.com/19381768/227757885-6f34cdbc-2022-4b5f-98aa-fe6134b8e58c.png)|
|:--:|
|Bag of Words representation|

## Naïve Bayes

### :sparkles: Naive Bayes Intuition
- Simple classification method based on Bayes rule
- Relies on the bag of words representation of documents

### :sparkles: Bayes' Rule Applied to Documents and Classes
- For a document $d$ and a class $c$

$$ P(c | d) = \frac{P(d | c)P(c)}{P(d)} \tag{1}$$

### :sparkles: Naïve Bayes Classifier

$$
\begin{align*}
    c_{MAP} &= \arg\max_{c \in C} P(c|d) \\
      		&= \arg\max_{c \in C} \frac{P(d | c)P(c)}{P(d)}\\
      		&= \arg\max_{c \in C} P(d |c)P(c)\\
      		&= \arg\max_{c \in C} P(x_1, x_2, \cdots, x_n | c)P(c)
\end{align*}
\tag{2}
$$

### :sparkles: Multinomial Naive Bayes Independence Assumptions

$$ P(x_1, x_2, \cdots, x_n | c) \tag{3}$$

- **Bag of Words assumption**: Assume position doesn't matter
- **Conditional Independence**: Assume the feature probabilities $P(x_i|c_j)$ are independent given the class $c$.

$$ P(x_1, x_2, \cdots, x_n | c) = P(x_1 |c) \cdot P(x_2 |c) \cdot \cdots \cdot P(x_n |c) \tag{4}$$

### :sparkles: Multinomial Naive Bayes Classifier

$$ c_{NB} = \arg\max_{c \in C} P(c_j) \prod_{x \in X} P(x | c) \tag{5}$$

### :sparkles: Applying Multinomial Naive Bayes Classifiers to Text Classification

$$ c_{NB} = \arg\max_{c_j \in C} [log P(c_j) + \sum_{i \in positions} log P(x_i | c_j)] \tag{6}$$

## Naïve Bayes: Learning

### :sparkles: Learning the Multinomial Naive Bayes Model
- Maximum likelihood estimates using frequencies in the data

$$ \hat{P}(c_j) = \frac{doccount(C = c_j)}{N_{doc}} \tag{7}$$

$$ \hat{P}(w_i|c_j) = \frac{count(w_i, c_j)}{\sum_{w \in V}count(w, c_j)} \tag{8}$$

### :sparkles: Parameter estimation

fraction of times word $w_i$ appears among all words in documents of topic $c_j$

$$ \hat{P}(w_i|c_j) = \frac{count(w_i, c_j)}{\sum_{w \in V}count(w, c_j)} $$

- Create mega-document for topic j by concatenating all docs in this topic
	- Use frequency of w in mega-document

### :sparkles: Problem with Maximum Likelihood

- What if we have seen no training documents with the word fantastic and classified in the topic positive (thumbs-up)?

$$ \hat{P}(\textrm{fantastic}|positive) = \frac{count(\textrm{fantastic}, positive)}{\sum_{w \in V}count(w, positive)} = 0$$

- Zero probabilities cannot be conditioned away, no matter the other evidence!

$$ c_{MAP} = argmax_c \hat{P}(c) \prod_i \hat{P}(x_i|c) $$

### :sparkles: Laplace (add-1) smoothing for Naïve Bayes

$$
\begin{align*}
    \hat{P}(x_i|c) &= \frac{count(w_i, c)+1}{\sum_{w \in V}(count(w, c)+1)} \\
    			   &= \frac{count(w_i, c)+1}{\sum_{w \in V}count(w, c)+|V|}
\end{align*}
\tag{9}
$$

### :sparkles: Unknown words
- What about unknown words
	- that appear in our test data
	- but not in our training data or vocab
- We ignore them
	- Remove them from the test document!
	- Pretend they weren't there!
	- Don't include any probability for them at all.
- Why don't we build an unknown word model?
	- It doesn't help: knowing which class has more unknown words is not generally a useful thing to know!

### :sparkles: Stop words
- Some systems ignore another class of words:
- Stop words: very frequent words like the and a.
	- Sort the whole vocabulary by frequency in the training, call the top 10 or 50 words the stopword list.
	- Now we remove all stop words from the training and test sets as if they were never there.
- But in most text classification applications, removing stop words don't help, so it's more common to not use stopword lists and use all the words in naive Bayes

### :sparkles: Multinomial Naïve Bayes: Learning

- From training corpus, extract Vocabulary
- Calculate $P(c_j)$ terms
```
for each c_j in C do
    docs_j ← all docs with class =c_j
    P(c_j) ← |docs_j| / |total # documents|
```

- Calculate $P(w_k | c_j)$ terms
```
Text_j ← single doc containing all docs_j
for each word w_k in Vocabulary
    n_k ← # of occurrences of w_k in Text_j
    P(w_k|c_j) ← (n_k +α) / (n + α|Vocabulary|)
```

### :sparkles: Multinomial Naïve Bayes: Classification

- Given a new document d, tokenize it into words
- Calculate class scores using log probabilities
```
for each c_j in C do
	score(c_j) = log(P(c_j))
for each word w_k in d
	score(c_j) += log(P(w_k|c_j))
```

- Choose the class with the highest score
```
c_MAP = argmax_c score(c)
```

## Binary Multinomial Naive Bayes Examples

Given sentences (or we can call them documents):

1. (neg) it was pathetic the worst part was the boxing scenes
2. (neg) no plot twists or great scenes
3. (pos) and satire and great plot twists
4. (pos) great scenes great film

After per-document binarization, the sentences become:

1. (neg) it was pathetic the worst part boxing scenes
2. (neg) no plot twists or great scenes
3. (pos) and satire great plot twists
4. (pos) great scenes film

We can generate a counts table comparing NB Counts and Binary Counts:

<table align="center">
  <tr><th rowspan="2"></th><th colspan="2">NB Counts</th><th colspan="2">Binary Counts</th></tr>
  <tr><th>+</th><th>-</th><th>+</th><th>-</th></tr>
  <tr><td>and</td><td>2</td><td>0</td><td>1</td><td>0</td></tr>
  <tr><td>boxing</td><td>0</td><td>1</td><td>0</td><td>1</td></tr>
  <tr><td>film</td><td>1</td><td>0</td><td>1</td><td>0</td></tr>
  <tr><td>great</td><td>3</td><td>1</td><td>2</td><td>1</td></tr>
  <tr><td>it</td><td>0</td><td>1</td><td>0</td><td>1</td></tr>
  <tr><td>no</td><td>0</td><td>1</td><td>0</td><td>1</td></tr>
  <tr><td>or</td><td>0</td><td>1</td><td>0</td><td>1</td></tr>
  <tr><td>part</td><td>0</td><td>1</td><td>0</td><td>1</td></tr>
  <tr><td>pathetic</td><td>0</td><td>1</td><td>0</td><td>1</td></tr>
  <tr><td>plot</td><td>1</td><td>1</td><td>1</td><td>1</td></tr>
  <tr><td>satire</td><td>1</td><td>0</td><td>1</td><td>0</td></tr>
  <tr><td>scenes</td><td>1</td><td>2</td><td>1</td><td>2</td></tr>
  <tr><td>the</td><td>0</td><td>2</td><td>0</td><td>1</td></tr>
  <tr><td>twists</td><td>1</td><td>1</td><td>1</td><td>1</td></tr>
  <tr><td>was</td><td>0</td><td>2</td><td>0</td><td>1</td></tr>
  <tr><td>worst</td><td>0</td><td>1</td><td>0</td><td>1</td></tr>
</table>
 
## Naïve Bayes Others

### :sparkles: Spam Filtering

- SpamAssassin Features: Mentions millions of dollars, From: starts with many numbers, Subject is all capitals, HTML has a low ratio of text to image area, "One hundred percent guaranteed", Claims you can be removed from the list.

|![image](https://user-images.githubusercontent.com/19381768/227757798-ce90063c-6502-4c8d-8c26-804ec9ed490b.png)|
|:--:|
|Spam Email|

### :sparkles: Language Identification

- Determine the language of a piece of text.
- Character n-grams perform well.
- Train on a variety of language instances.

### :sparkles: Naïve Bayes: Relationship to Language Modeling

- Each class is a unigram language model.
- Assigning each word: $P(\text{word} | c)$
- Assigning each sentence: $P(s|c)= \prod P(\text{word}|c)$

|![image](https://user-images.githubusercontent.com/19381768/227759914-97057801-a97b-4d3c-b728-793d7c6742cc.png)|
|:--:|
|Generative model for multinomial Naïve Bayes|

### :sparkles: Naïve Bayes Summary

1. Multinomial Naïve Bayes is a simple, powerful model for text classification
2. Based on Bayes rule and the independence assumption
3. Parameter estimation is done by counting word frequencies in the training set
4. Laplace (add-1) smoothing is used to avoid zero probabilities
5. Unknown words are ignored during classification
6. The model can be easily trained and applied for classification using log probabilities to avoid underflow

### :sparkles: Additional notes

- Naïve Bayes can be applied to other types of data and not just text; the multinomial model is well-suited for text classification.
- The independence assumption is a strong assumption, but the model still works well in practice, especially for text classification tasks.
- It is a fast and efficient algorithm that can be easily scaled to large datasets.

## :sparkles: Sentiment Classification

### :sparkles: Dealing with Negation

- Negation changes the meaning of words (e.g., "I really `don't` like this movie").
- Simple baseline method: Add `NOT_` to every word between negation and following punctuation.

### :sparkles: Lexicons

- Pre-built word lists called lexicons can be useful when labeled training data is limited.
- Examples: MPQA Subjectivity Cues Lexicon, The General Inquirer, Bing Liu Opinion Lexicon.

### :sparkles: Using Lexicons in Sentiment Classification

- Add features that count occurrences of words from lexicons (e.g., positive or negative words).
- Dense lexicon features can help when training data is sparse or not representative of the test set.

### :sparkles: A Worked Sentiment Example

Training sentences:
- (neg) just plain boring
- (neg) entirely predictable and lacks energy
- (neg) no surprises and very few laughs
- (pos) very powerful
- (pos) the most fun film of the summer

Test sentence:
- predictable with no fun

### :sparkles: Training the Model

1. Calculate the class priors: $P(c)$
- $P(neg) = \frac{3}{5}$
- $P(pos) = \frac{2}{5}$

2. Calculate the likelihoods: $P(word | c)$. Given that $N_{neg}=14$, $N_{pos}=9$, $|V|=20$

For example, for the word "predictable":

- $P(predictable | neg) = \frac{1 + 1}{14 + 20} = \frac{1}{17}$
- $P(predictable | pos) = \frac{0 + 1}{9 + 20} = \frac{1}{29}$

### :sparkles: Classifying the Test Sentence

1. Tokenize the test sentence: "predictable", "with", "no", "fun"

2. Calculate the posterior probabilities using the likelihoods and priors:
    - $P(neg | text) \propto P(neg) \times P(predictable | neg) \times P(with | neg) \times P(no | neg) \times P(fun | neg)$
    - $P(pos | text) \propto P(pos) \times P(predictable | pos) \times P(with | pos) \times P(no | pos) \times P(fun | pos)$

3. Compare the posterior probabilities and assign the class with the highest probability:
    - Since $P(neg | text) > P(pos | text)$, the test sentence is classified as negative.

## Evaluation Metrics

|![image](https://user-images.githubusercontent.com/19381768/227759985-a881b102-ea20-45a2-985d-5ac8e877d271.png)|
|:--:|
|The 2-by-2 confusion matrix|

### :sparkles: Precision, Recall, and F measure

- Precision: 
$$\frac{\text{true positives}}{\text{true positives} + \text{false positives}}$$
- Recall: 
$$\frac{\text{true positives}}{\text{true positives} + \text{false negatives}}$$
- F measure: 
$$F_\beta = \frac{(\beta^2 + 1)PR}{\beta^2 P + R}$$ 
(balanced $F_1$: $\beta=1$)

### :sparkles: Development Test Sets ("Devsets") and Cross-validation

- Train on training set, tune on devset, report on testset.
- Cross-validation: multiple splits, pool results over splits, compute pooled dev performance.

|![image](https://user-images.githubusercontent.com/19381768/227760021-6ec9b1e7-fce0-42cf-9b28-c4c7dda1b8ec.png)|
|:-:|
|Cross-validation: multiple splits|

## Evaluation with More than Two Classes

|![image](https://user-images.githubusercontent.com/19381768/227760052-c1cfff13-dc6b-45f8-ac8d-d74297d94f1c.png)|
|:--:|
|Confusion Matrix for 3-class classification|

### :sparkles: Confusion Matrix and Combining P/R

- Macroaveraging: compute the performance for each class, and then average over classes.
- Microaveraging: collect decisions for all classes into one confusion matrix, compute precision and recall from that table.

|![image](https://user-images.githubusercontent.com/19381768/227760113-bc86ebbc-5a34-40a0-92cb-ce717a233fd6.png)|
|:--:|
|Macroaveraging and Microaveraging|

## Avoiding Harms in Classification

### :sparkles: Harms in Sentiment and Toxicity Classifiers

- Sentiment classifiers may assign lower sentiment to sentences with African American names.
- Toxicity classifiers may incorrectly flag non-toxic sentences mentioning certain identities.

### :sparkles: Causes of Harms

- Problems in training data, human labels, resources, or model architecture.
- Mitigation of these harms is an open research area.

### :sparkles: Model Cards

- Document training algorithms and parameters, data sources and motivations, intended use and users, and model performance across different demographic or other groups and environmental situations.

