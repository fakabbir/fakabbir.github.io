---
title: POS tagging using Hidden Markov Model
tags: [nlp]
style: fill
color: warning
description: Code snippets with concepts for building POS tagger using Hidden Markov Model
external_url: https://www.notion.so/Hidden-Markov-Model-70bca4981b7b45eb8016741e3a703254
---

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6adc6e76-7402-4987-85be-2e4c84c36a0e/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6adc6e76-7402-4987-85be-2e4c84c36a0e/Untitled.png)

**Part of speech tagging** is one of the important tasks which work with text data. The problem statement is to attach a pos tag with each word token in the sentence.

There are multiple ways to solve the problem statement. One way would be to count the most common tag for a given word and attach it whenever the word is encountered. Using this technique its shown to achieve an accuracy of 93%-95%. Even if this seems to be a good number, while working with a large dataset, the number of errors would be significant.

This could be even more optimized using the hidden Markov model.

Using the hidden Markov model, the problem statement is solved by picking up the tag sequence for a sentence that has the maximum probability based on the test data.

The probability of a path(sequence of token attached) is calculated in two steps.

The first probability is termed as **transition probability** which denotes the probability of assigning work with token t_i given that the previous token is t_prev.

The second probability term is called **emission probability**, which measures how probable the word is to occur in a sentence given the tag is identified as t_i.

To find the path with the highest probability, **vertebri algorithms** is used, where only the path which produces the highest probability for common paths are calculated.

While working this in python, **pomegranate** package could be used to produce the path effectively,

The step is follows

-   Initialize a model
-   Add states
-   Add transitions
-   Add start and end transitions
-   model.bake()