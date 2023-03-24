# Introduction to Natural Language Processing

## What is Natural Language Processing?
NLP is a field of study that focuses on designing and analyzing computational algorithms and representations for processing natural human language, making human language accessible to computers.

## The Goals of NLP
The primary goal of NLP is to make computers capable of handling natural human language, such as email, library research, and conversation. However, natural human language is a complex system constructed to convey meaning that is different from vision or any other machine learning task, which makes it difficult for computers to understand. NLP tries to help computers learn language as humans do.

## What's So Special About Human (Natural) Language?
Human language is a system specifically constructed to convey meaning, and it's not produced by a physical manifestation of any kind. Most words are just symbols for an extra-linguistic entity, and the symbols of language can be encoded in several modalities: voice, gesture, writing, etc.

## Why is NLP Hard?
NLP is challenging because the mappings between different levels of language, such as syntax, semantics, and pragmatics, are extremely complex, and the appropriateness of a representation depends on the application.

## Successful NLP Applications and Systems
There are several successful NLP applications and systems, such as search engines, translation, anti-spam, smart assistants, autocomplete, and more. Other applications include sentiment analysis, emotion detection, question answering, text summarization, chatbots, semantic parsing, named entity recognition, speech recognition, text to speech, machine reading comprehension, and more.

## NLP Use Cases
NLP can be used to recognize and predict diseases based on electronic health records and patient's speech, perform sentiment analysis to understand customers' preferences, filter and classify emails, detect fake news, provide voice interfaces, track news and comments for financial traders, select talent recruitment, automate routine litigation tasks, and more.

## NLP and Related Fields
NLP is rooted in many fields, such as computational linguistics, machine learning, artificial intelligence, computer science, speech processing, ethics, and others, including computational social science, digital humanities, probabilistic topic models, information retrieval, and text mining.

## Human Language: Levels of Meaning
Human language consists of several levels of meaning, including discourse, pragmatics, semantics, syntax, lexemes, morphology, phonetics (phonology), and orthography.

## NLP Approaches
NLP approaches include rule-based, data-driven (statistical, machine learning, and deep learning).

## The History of NLP
The idea of computers understanding natural language has been a staple of science fiction since the first half of the twentieth century. The 1990s witnessed the adoption of statistical methods for NLP. In 2010, the success of deep learning on computer vision tasks spread to NLP tasks as well.

## Probability
Probability is the mathematical language for quantifying uncertainty, measuring the chance that something will happen. It's the proportion of observations where a given outcome happens, and it's used to quantify the strength of belief that something is true.

## Basic Concepts
An experiment is the process by which an observation is obtained, and a simple event is the outcome observed on a single repetition of the experiment. The set of all simple events of an experiment is called the sample space. An event is a collection of one or more simple events. Two events are mutually exclusive if, when one event occurs, the other cannot, and vice versa.

## The probability of an Event
- The probability of an event A measures “how often” we think A will occur. We write P(A).
- Suppose that an experiment is performed n times. The relative frequency for an event A is

$\frac{\text{Number of times A occurs } f}{n} = \frac{f}{n}$

- If we let n get infinitely large, $P(A) = \lim_{n\rightarrow\infty}\frac{f}{n}$
- $P(A)$ must be between 0 and 1.
  - If event A can never occur, $P(A) = 0$.
  - If event A always occurs, $P(A) = 1$.
- The sum of the probabilities for all simple events in $\Omega$ equals 1. $P(\Omega) = 1$.
- The probability of an event A can be found by adding the probabilities of all the simple events in A.

## Event Relations
- The union of two events, A and B, is the event that either A or B or both occur when the experiment is performed. We write $A \cup B$.
- The intersection of two events, A and B, is the event that both A and B occur. We write $A \cap B$.
