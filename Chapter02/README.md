# NLP Basic Tasks I

## Regular Expressions (RegEx)
### What are Regular Expressions?
- A formal language for specifying text strings
- Used to search for specific patterns in text

## Disjunctions
- Letters inside square brackets `[]`
- Ranges `[A-Z]`

|Pattern|Matches|
|--|--|
|[wW]oodchuck	|Woodchuck, woodchuck|
|[1234567890]|	Any digit|

### Negation in Disjunction
- Negations `[^Ss]`
- Carat `^` means negation only when first in `[]`

###  More Disjunction
- The pipe `|` for disjunction

### Special Characters: ? *+.
- `?` Optional previous character
- `*` 0 or more of the previous character
- `+` 1 or more of the previous character
- `.` Any single character

### Anchors ^ $
- `^` Start of the line
- `$` End of the line

### Errors
1. False positives (Type I errors) - Matching strings that should not have been matched
2. False negatives (Type II errors) - Not matching things that should have been matched

### Substitutions
- Replace a pattern with another pattern
- `s/regexp1/pattern/`

### Capture Groups
- Use parentheses `()` to "capture" a pattern into a numbered register (1, 2, 3…)
- Use `\1` to refer to the contents of the register

### Non-Capturing Groups
- Add a `?`: after the parenthesis to create non-capturing groups

### Lookahead Assertions
- `(?=pattern)` is true if pattern matches, but is zero-width; doesn't advance character pointer
- `(?!pattern)` true if a pattern does not match

|![image](https://user-images.githubusercontent.com/19381768/227708353-660fc62a-1c23-45fc-9a19-c3752c9df3a1.png)|
|:--:|
|Lookahead and Lookbehind|

## Words and Corpora
### Tokens and Types
- **Token**: an instance of a type in running text
- **Type**: an element of the vocabulary

### Heaps Law (Herdan's Law)
- |V| = $kN^{\beta}$ where often $0.67 < \beta < 0.75$
- Vocabulary size grows with > square root of the number of word tokens

### Corpora
- Texts produced by specific writers, in specific languages, varieties, and genres, for specific functions

### Corpus Dimensions
- Language
- Variety
- Code switching
- Genre
- Author demographics

### Corpus Datasheets
- Motivation
- Situation
- Collection process
- Annotation process
- Language variety
- Speaker demographics

## Word Tokenization
### Text Normalization
1. Tokenizing (segmenting) words
2. Normalizing word formats
3. Segmenting sentences

### Issues in Tokenization
- Can't just blindly remove punctuation
- Handling clitics
- Multiword expressions (MWE)

### Tokenization without spaces
- Chinese, Japanese, Thai don't use spaces to separate words

### Word tokenization in Chinese
- Chinese words are composed of characters called hanzi
- Each one represents a meaning unit called a morpheme
- Deciding what counts as a word is complex and not agreed upon

|![image](https://user-images.githubusercontent.com/19381768/227709043-ceb36f2e-c637-4b98-828b-ab228683df39.png)|
|:--:|
|Word tokenization examples in Chinese|

