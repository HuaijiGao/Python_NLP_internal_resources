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
> ![image](https://user-images.githubusercontent.com/19381768/225634659-32d42399-a113-46f1-8f7f-706fb018f790.png)

Try more words (e.g., liberty, constitution), and different texts. 
```py
text4.dispersion_plot(["liberty", "nation", "constitution", "kindness", "pope"])
```
> ![image](https://user-images.githubusercontent.com/19381768/225634799-447cdb08-d580-4b70-bc4e-73dde4be1ed1.png)

For these plots to work, it is assumed that ```numpy``` and ```matplotlib``` are installed.
