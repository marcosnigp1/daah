---
permalink: /assignment-1/
title: "Assignment 1"
---

_Use of A.I. Disclosure: We used Claude Code and Copilot to write the logic for the data analysis. We made sure that it outputs what we need in accordance to what we were seeking for._

# Introduction

### What we were looking for?

During the discussion we had, we noticed that Saeed Syed and me were really interested in checking if there was some kind of words related to space and their rate of frequency before, during (which was during 1939 to 1945) and after World War 2.

According to the reading by David _Seed Science Fiction: A Very Short Introduction_ after World War 2 (34) there was a interest in exploring themes of alien invansions, with the whole ideas of "conquer or be conquered." There can be interesting facts about it, or some words that appear to be more frequent during specific times, but it is something we will be exploring during the course of this analysis.

### Hypothesis

Books written in the WW2 era will have more words related to science fiction as well as possess the war tag more than the rest in the science fiction corpus.

### The method

In order to analyze this, we used the following techniques, with the reasoning as to why we choose them:

#### Distinctive vocabulary using TF-IDF

The first analytical method deployed during our analysis was the TF-IDF, or short term for _term frequency-inverse document frequency_. This is a used to identify words that are especially characteristic of one group compared with other groups. In this case, we are tokenizing each book into individual words, removing any kind of punctuation, numbers, and common English stop words; all the books written in the corpus seem to be in English.

After tokenizing, the words frequencies are then counted within each book.
