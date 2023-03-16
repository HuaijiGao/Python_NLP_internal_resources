# NLTK, Spacy and Visualization Techniques

## NLTK

NLTK is one of the major NLP packages in Python. It is targeted at learners rather than being a production library which makes a good starting point for our purposes.

The first step is to import nltk then make sure that all the necessary files are downloaded.

```python
import nltk
nltk.download("all", quiet=True)
```

If you are running on your personal machine (not within Google colab), you only need to do this once.

NLTK offers a special module called "book" which can be imported using `from nltk.book import *`

After printing a welcome message, it loads the text of several books (this will take a few seconds).

```python
from nltk.book import *
```
<details>Output:
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
text9: The Man Who Was Thursday by G . K . Chesterton 1908<br>
</details>

