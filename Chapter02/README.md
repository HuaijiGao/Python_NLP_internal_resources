# NLTK, Spacy and Visualization Techniques

# NLTK

NLTK is one of the major NLP packages in Python. It is targeted at learners rather than being a production library which makes a good starting point for our purposes.

The first step is to import nltk then make sure that all the necessary files are downloaded.

```py
import nltk
nltk.download("all", quiet=True)
```

If you are running on your personal machine (not within Google colab), you only need to do this once.

NLTK offers a special module called "book" which can be imported using `from nltk.book import *`

After printing a welcome message, it loads the text of several books (this will take a few seconds).

```py
from nltk.book import *
```
> *** Introductory Examples for the NLTK Book ***<br>
Loading text1, ..., text9 and sent1, ..., sent9<br>
Type the name of the text or sentence to view it.<br>
Type: 'texts()' or 'sents()' to list the materials.<br>
text1: Moby Dick by Herman Melville 1851<br>
text2: Sense and Sensibility by Jane Austen 1811<br>
text3: The Book of Genesis<br>
text4: Inaugural Address Corpus<br>
text5: Chat Corpus<br>
text6: Monty Python and the Holy Grail<br>
text7: Wall Street Journal<br>
text8: Personals Corpus<br>
text9: The Man Who Was Thursday by G . K . Chesterton 1908

This module contains a number of Corpora that are ready to practice on. The Corpora are named: *text1* - *text9*

```python
text1
```
> <Text: Moby Dick by Herman Melville 1851>
```python
text2
```
> <Text: Sense and Sensibility by Jane Austen 1811>

## Searching Text
There are many ways to examine the context of a text apart from simply reading it. **A concordance view shows us every occurrence of a given word, together with some context**.

```py
text1.concordance("true")
```
> <img width="678" alt="image" src="https://user-images.githubusercontent.com/19381768/225631465-a0154cef-b5a8-4b48-9ef0-1a1d55a3d173.png">

Try it yourself. Let's find more about the words: ["often", "test", "extreme"] is text2

```py
text2.concordance("often")
```

> <img width="677" alt="image" src="https://user-images.githubusercontent.com/19381768/225632238-8307ac65-6d6b-4c97-8332-e6320cabe7d1.png">

A concordance permits us to see words in context. For example, we saw that monstrous occurred in contexts such as the \_\_\_ pictures and a \_\_\_ size . 

What other words appear in a similar range of contexts? We can find out by appending the term similar to the name of the text in question, then inserting the relevant word in parentheses:

```py
text1.similar("monstrous")
```

> true contemptible christian abundant few part mean careful puzzled mystifying passing curious loving wise doleful gamesome singular delightfully perilous fearless

```py
text2.similar("monstrous")
```

> very so exceedingly heartily a as good great extremely remarkably sweet vast amazingly

Observe that we get different results for different texts. Austen uses this word quite differently from Melville; for her, monstrous has positive connotations, and sometimes functions as an intensifier like the word very.

The method `common_contexts` allows us to examine just the contexts that are shared by two or more words, such as monstrous and very. 

```py
text2.common_contexts(["monstrous", "very"])
```
> am_glad a_pretty a_lucky is_pretty be_glad

Your Turn: pick another pair of words and compare their usage in two different texts, using the ```similar()``` and ```common_contexts()``` functions.

```py
text1.similar("benevolent")
```
> all out long allusions sung many thou wine one full eyes much sunrise also some king sixty man progress gills

```py
# find the common contexts in which the words: great and dangerous are used in text1
text1.common_contexts(["great", "dangerous"])

# find the common contexts in which the words: benevolent and fish are used in text1
text1.common_contexts(["benevolent", "fish"])
```
> a_man<br>
No common contexts were found

It is one thing to automatically detect that a particular word occurs in a text, and to display some words that appear in the same context. 

However, we can also determine the location of a word in the text: how many words from the beginning it appears. This positional information can be displayed using a dispersion plot. Each stripe represents an instance of a word, and each row represents the entire text.

```py
text4.dispersion_plot(["citizens", "democracy", "freedom", "duties", "America"])
```
> <img width="426" alt="image" src="https://user-images.githubusercontent.com/19381768/225637587-b4048b29-8e5a-4dd5-aa74-8634b325a123.png">

Try more words (e.g., liberty, constitution), and different texts. 
```py
text4.dispersion_plot(["liberty", "nation", "constitution", "kindness", "pope"])
```
> <img width="429" alt="image" src="https://user-images.githubusercontent.com/19381768/225637672-36093c7d-c66a-493e-a50f-9aa643674a2a.png">

For these plots to work, it is assumed that ```numpy``` and ```matplotlib``` are installed.

## Counting Vocabulary
The most obvious fact about texts that emerges from the preceding examples is that they differ in the vocabulary they use. 

Let's begin by finding out the length of a text from start to finish, in terms of the words and punctuation symbols that appear. 

Let's find the number of words in the book of Genensis:

```py
len(text3)
```
> 44764

So Genesis has 44,764 words and punctuation symbols, or "tokens." 

This includes duplicate tokens. To find the number of unique words, we use the ```set``` data structure as follows, and to get a sorted set, we use the Python ```sorted()``` function:

```py
# print(set(text3))
# print(sorted(set(text3)))
len(set(text3))
```
> 2789

Although it has 44,764 tokens, this book has only 2,789 distinct words, or "word types." 

Now, let's calculate a measure of the lexical richness of the text. The next example shows us that the number of distinct words is just 6% of the total number of words, or equivalently that each word is used 16 times on average.

```py
print(len(set(text3)) / len(text3))
print(len(text3)/len(set(text3)))
```
> 0.06230453042623537<br>
16.050197203298673

Next, let's focus on particular words. We can count how often a word occurs in a text, and compute what percentage of the text is taken up by a specific word:

```py
text3.count("smote")
```
> 5
```py
100 * text4.count("a") / len(text4)
```
> 1.457806031353621

Your Turn: How many times does the word *lol* appear in text5? How much is this as a percentage of the total number of words in this text?

```py
100 * text5.count("lol") / len(text5)
```
> 1.5640968673628082

To simplify things, let's create a functions for calculating lexical diversity

```py
def lexical_diversity(text):
  return len(set(text)) / len(text)

def percentage(count, total):
  return 100 * count / total
```

We can go ahead and use these functions, let's find the number of tokens, the number of types, the lexical diversity for for the for the following:

```py
from nltk.corpus import brown

print(f"The type of brown is: {type(brown)}")

len(brown.words()), len(set(brown.words())), lexical_diversity(brown.words())
```
> The type of brown is: <class 'nltk.corpus.util.LazyCorpusLoader'><br>
(1161192, 56057, 0.048275392872152066)

```py
print(brown.raw()[:10])
print(brown.words()[:10])
print(brown.sents()[:2])
print(brown.paras()[:2])
```
> 

	The/at <br>
['The', 'Fulton', 'County', 'Grand', 'Jury', 'said', 'Friday', 'an', 'investigation', 'of']<br>
[['The', 'Fulton', 'County', 'Grand', 'Jury', 'said', 'Friday', 'an', 'investigation', 'of', "Atlanta's", 'recent', 'primary', 'election', 'produced', '``', 'no', 'evidence', "''", 'that', 'any', 'irregularities', 'took', 'place', '.'], ['The', 'jury', 'further', 'said', 'in', 'term-end', 'presentments', 'that', 'the', 'City', 'Executive', 'Committee', ',', 'which', 'had', 'over-all', 'charge', 'of', 'the', 'election', ',', '``', 'deserves', 'the', 'praise', 'and', 'thanks', 'of', 'the', 'City', 'of', 'Atlanta', "''", 'for', 'the', 'manner', 'in', 'which', 'the', 'election', 'was', 'conducted', '.']]<br>
[[['The', 'Fulton', 'County', 'Grand', 'Jury', 'said', 'Friday', 'an', 'investigation', 'of', "Atlanta's", 'recent', 'primary', 'election', 'produced', '``', 'no', 'evidence', "''", 'that', 'any', 'irregularities', 'took', 'place', '.']], [['The', 'jury', 'further', 'said', 'in', 'term-end', 'presentments', 'that', 'the', 'City', 'Executive', 'Committee', ',', 'which', 'had', 'over-all', 'charge', 'of', 'the', 'election', ',', '``', 'deserves', 'the', 'praise', 'and', 'thanks', 'of', 'the', 'City', 'of', 'Atlanta', "''", 'for', 'the', 'manner', 'in', 'which', 'the', 'election', 'was', 'conducted', '.']]]
