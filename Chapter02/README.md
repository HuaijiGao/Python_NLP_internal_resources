# NLP Basic Tasks I

|Table of Sections|
|---|
|:herb:  [Regular Expressions (RegEx)](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter02/README.md#regular-expressions-regex)<br>:herb:  [Words and Corpora](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter02/README.md#words-and-corpora)<br>:herb:  [Word Tokenization](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter02/README.md#word-tokenization)<br>:herb:  [Word Normalization and Other Issues](https://github.com/bosoninfo/Resource_NLP-in-Python/blob/main/Chapter02/README.md#word-normalization-and-other-issues)|

## Regular Expressions (RegEx)
### What are Regular Expressions?
- A formal language for specifying text strings
- Used to search for specific patterns in text

### :seedling: Disjunctions
- Letters inside square brackets `[]`
- Ranges `[A-Z]`

|Pattern|Matches|
|--|--|
|[wW]oodchuck	|Woodchuck, woodchuck|
|[1234567890]|	Any digit|

### :seedling: Negation in Disjunction
- Negations `[^Ss]`
- Carat `^` means negation only when first in `[]`

### :seedling: More Disjunction
- The pipe `|` for disjunction

### :seedling: Special Characters: ? *+.
- `?` Optional previous character
- `*` 0 or more of the previous character
- `+` 1 or more of the previous character
- `.` Any single character

### :seedling: Anchors ^ $
- `^` Start of the line
- `$` End of the line

### :seedling: Errors
1. False positives (Type I errors) - Matching strings that should not have been matched
2. False negatives (Type II errors) - Not matching things that should have been matched

### :seedling: Substitutions
- Replace a pattern with another pattern
- `s/regexp1/pattern/`

### :seedling: Capture Groups
- Use parentheses `()` to "capture" a pattern into a numbered register (1, 2, 3…)
- Use `\1` to refer to the contents of the register

### :seedling: Non-Capturing Groups
- Add a `?`: after the parenthesis to create non-capturing groups

### :seedling: Lookahead Assertions
- `(?=pattern)` is true if pattern matches, but is zero-width; doesn't advance character pointer
- `(?!pattern)` true if a pattern does not match

|![image](https://user-images.githubusercontent.com/19381768/227708353-660fc62a-1c23-45fc-9a19-c3752c9df3a1.png)|
|:--:|
|Lookahead and Lookbehind|

## Words and Corpora
### :seedling: Tokens and Types
- **Token**: an instance of a type in running text
- **Type**: an element of the vocabulary

### :seedling: Heaps Law (Herdan's Law)
- |V| = $kN^{\beta}$ where often $0.67 < \beta < 0.75$
- Vocabulary size grows with > square root of the number of word tokens

### :seedling: Corpora
- Texts produced by specific writers, in specific languages, varieties, and genres, for specific functions

### :seedling: Corpus Dimensions
- Language
- Variety
- Code switching
- Genre
- Author demographics

### :seedling: Corpus Datasheets
- Motivation
- Situation
- Collection process
- Annotation process
- Language variety
- Speaker demographics

## Word Tokenization
### :seedling: Text Normalization
1. Tokenizing (segmenting) words
2. Normalizing word formats
3. Segmenting sentences

### :seedling: Issues in Tokenization
- Can't just blindly remove punctuation
- Handling clitics
- Multiword expressions (MWE)

### :seedling: Tokenization without spaces
- Chinese, Japanese, Thai don't use spaces to separate words

### :seedling: Word tokenization in Chinese
- Chinese words are composed of characters called hanzi
- Each one represents a meaning unit called a morpheme
- Deciding what counts as a word is complex and not agreed upon

|![image](https://user-images.githubusercontent.com/19381768/227709043-ceb36f2e-c637-4b98-828b-ab228683df39.png)|
|:--:|
|Word tokenization examples in Chinese|

### :seedling: Tokenization Techniques
1. White space and punctuation tokenization
2. N-grams
3. Byte Pair Encoding (BPE)

### :seedling: Byte Pair Encoding Tokenization
A third option for word segmentation
- Use data to determine tokenization.
- Subword tokenization (tokens are parts of words)
- Can include common morphemes (smallest meaning-bearing unit in a language) like -est or -er.

### :seedling: Subword tokenization
- Three common algorithms:
  - Byte-Pair Encoding (BPE)
  - Unigram language modeling tokenization
  - WordPiece
- Two parts: token learner and token segmenter.

### :seedling: Byte Pair Encoding (BPE)
- Starts with a vocabulary of all individual characters.
- Repeats k merges of the most frequent adjacent symbols in the training corpus, updating the vocabulary and corpus each time.

### :seedling: BPE token learner algorithm
- Function BYTE-PAIR ENCODING(strings C, number of merges k) returns vocab V
- Merges are performed in order of frequency on training data.
- Test frequencies do not play a role.

## Word Normalization and Other Issues
### :seedling: Word normalization
- Putting words/tokens in a standard format.

### :seedling: Case folding
- Reducing all letters to lowercase (or uppercase).
- Case can be helpful in sentiment analysis, machine translation, and information extraction.

### :seedling: Lemmatization
- Representing words as their shared root (dictionary headword form).
- Requires morphological parsing.

### :seedling: Morphemes and Morphological Parsing
- **Morphemes**: small meaningful units that make up words.
- **Stems**: core meaning-bearing units.
- **Affixes**: parts that adhere to stems, often with grammatical functions.
- **Morphological Parsers**: parse words into morphemes and their grammatical features.

### :seedling: Stemming
- Reducing terms to stems by crudely removing affixes.
- Example: Porter Stemmer, based on a series of rewrite rules.

### :seedling: Complex Morphology
- Necessary for many languages, such as Turkish.

### :seedling: Sentence Segmentation
- Punctuation marks like ! and ? are less ambiguous than periods.
- Common algorithm: decide whether a period is part of a word or a sentence-boundary marker.
- Abbreviation dictionaries can help.
