# Introduction to Natural Language Processing

|Table of Sections|
|---|
|:star: [Natural Language Processing (NLP)](https://github.com/JefoGao/Resource_NLP-in-Python/blob/main/Chapter01/README.md#natural-language-processing-nlp)<br>:star: [Probability in NLP](https://github.com/JefoGao/Resource_NLP-in-Python/blob/main/Chapter01/README.md#probability-in-nlp)<br>:star: [NLP and Related Fields](https://github.com/JefoGao/Resource_NLP-in-Python/blob/main/Chapter01/README.md#nlp-and-related-fields)|

# Natural Language Processing (NLP)
**Definition**: NLP is a set of methods for making human language accessible to computers.

**Goals**: Enable computers to handle human language tasks such as email management, library research, and communication.

**Challenges**: Human language is complex, and understanding it requires dealing with ambiguity, multiple interpretations, and context.

**Applications**: Search engines, translation, spam filtering, smart assistants, sentiment analysis, emotion detection, chatbots, speech recognition, text generation, and more.

## Ambiguity in Language
Ambiguity occurs when sentences or phrases have multiple interpretations. Resolving ambiguity requires knowledge of the world and common sense reasoning.

## NLP Approaches
1. Rule-based
2. Data-driven
   1. Statistical
   2. Machine learning
   3. Deep learning

# Probability in NLP
**Probability** is the mathematical language for quantifying uncertainty.

**Basic Concepts:**
- **Experiment**: Process of obtaining an observation or measurement.
- **Simple Event**: Outcome observed on a single repetition of the experiment.
- **Sample Space (Ω)**: Set of all simple events of an experiment.
- **Event**: Collection of one or more simple events.

## Event Relations:
- **Union (A ⋃ B)**: Event that either A or B or both occur.
- **Intersection (A ⋂ B)**: Event that both A and B occur.

## Probability Rules & Relations of Events:

- Complement Event: $P(A^C) = 1-P(A)$
- Additive Rule: $P(A \cup B) = P(A) + P(B) - P(A \cap B)$
- Multiplicative Rule: $P(A \cap B) = P(A)P(B|A)$
- Conditional probability: $P(A|B) = \frac{P(A \cap B)}{P(B)}$
- Mutually Exclusive Events: $P(A \cap B) = 0$, $P(A \cup B) = P(A) + P(B)$
- Independent Events: $P(A \cap B) = P(A)P(B)$, $P(A|B)=P(A)$, $P(A \cap B \cap C)=P(A)P(B)P(C)$

|![image](https://user-images.githubusercontent.com/19381768/227531466-ecdaf113-06f1-4fe1-bd12-e9774c3b8116.png)|
|:--:|
|Venn Diagrams|

# NLP and Related Fields
NLP is rooted in fields such as computational linguistics, machine learning, artificial intelligence, computer science, speech processing, ethics, and others.

## Human Language: Levels of Meaning
***Discourse -> Pragmatics -> Semantics -> Syntax -> Lexemes -> Morphology -> Phonetics (Phonology) and Orthography***

Human language can be analyzed at several levels to understand and process its meaning. These levels are:

1. **Phonetics (Phonology) and Orthography**: Phonetics studies the sounds in human languages, while phonology focuses on the organization and patterns of these sounds. Orthography deals with the written representation of language, including the rules for spelling and punctuation.
2. **Morphology**: Morphology is the study of the structure and formation of words. It involves the analysis of morphemes, which are the smallest meaningful units in a language. Morphemes can be roots, prefixes, suffixes, or infixes, and they can modify word meaning or grammatical function.
3. **Lexemes**: Lexemes are the basic units of meaning in a language, such as words and idiomatic expressions. They form the basis for constructing sentences and conveying meaning through syntax and semantics.
4. **Syntax**: Syntax is the study of the rules and principles that govern the structure of sentences in a language. It specifies the order in which words are arranged to form sentences and how different sentence components (e.g., subject, verb, and object) relate to one another.
5. **Semantics**: Semantics is the study of meaning in language, focusing on how words, phrases, and sentences are used to convey meaning. It involves understanding the relationships between words and the concepts they represent, as well as how context can influence the interpretation of language.
6. **Pragmatics**: Pragmatics deals with the way language is used in context to convey meaning and perform social functions. It involves understanding how speakers use language to convey their intentions, how listeners interpret what is said, and how context, tone, and non-verbal cues can impact meaning.
7. **Discourse**: Discourse is the study of larger units of language, such as conversations, narratives, or written texts. It investigates how these units are structured, how they convey meaning, and how they are used in different social and cultural contexts.

Understanding and processing human language at these different levels is essential for effective natural language processing. NLP algorithms and techniques often focus on one or more of these levels, depending on the specific task or application.

## NLP as a Field
NLP sits at the intersection of computer science and linguistics.

## Course Outline
1. Basic text processing techniques
2. Topic modeling
3. Text classification and sentiment analysis
4. Vector space models
5. NLP on Azure
