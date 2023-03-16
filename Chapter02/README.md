# NLTK, Spacy and Visualization Techniques

## NLTK

NLTK is one of the major NLP packages in Python. It is targeted at learners rather than being a production library which makes a good starting point for our purposes.

The first step is to import nltk then make sure that all the necessary files are downloaded.

```
import nltk
nltk.download("all", quiet=True)
```

If you are running on your personal machine (not within Google colab), you only need to do this once.

NLTK offers a special module called "book" which can be imported using `from nltk.book import *`

After printing a welcome message, it loads the text of several books (this will take a few seconds).

```
from nltk.book import *
```

|*** Introductory Examples for the NLTK Book ***
Loading text1, ..., text9 and sent1, ..., sent9
Type the name of the text or sentence to view it.
Type: 'texts()' or 'sents()' to list the materials.
text1: Moby Dick by Herman Melville 1851
text2: Sense and Sensibility by Jane Austen 1811
text3: The Book of Genesis
text4: Inaugural Address Corpus
text5: Chat Corpus
text6: Monty Python and the Holy Grail
text7: Wall Street Journal
text8: Personals Corpus
text9: The Man Who Was Thursday by G . K . Chesterton 1908|
