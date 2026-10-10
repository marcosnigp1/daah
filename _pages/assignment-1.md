---
permalink: /assignment-1/
title: "Assignment 1"
---

_Use of A.I. Disclosure: We used Claude Code and Copilot to write the logic for the data analysis. We made sure that it outputs what we need in accordance to what we were seeking for._

# Introduction

### What we were looking for?

During the discussion we had, we noticed that Saeed Syed and me were really interested in checking if there was some kind of words related to space and their rate of frequency before, during (which was during 1939 to 1945) and after World War 2.

According to the reading by David Seed: _Science Fiction: A Very Short Introduction_ after World War 2 (34) there was a interest in exploring themes of alien invansions, with the whole ideas of "conquer or be conquered." There can be interesting facts about it, or some words that appear to be more frequent during specific times, but it is something we will be exploring during the course of this analysis.

### Hypothesis

Books written in the WW2 era will have more words related to science fiction as well as possess the war tag more than the rest in the science fiction corpus.

### The method

In order to analyze this, we used the following techniques, with the reasoning as to why we choose them:

#### Distinctive vocabulary using TF-IDF

The first analytical method deployed during our analysis was the TF-IDF, or short term for _term frequency-inverse document frequency_. This is a used to identify words that are especially characteristic of one group compared with other groups. In this case, we are tokenizing each book into individual words, removing any kind of punctuation, numbers, and common English stop words; all the books written in the corpus seem to be in English.

After tokenizing, the words frequencies are then counted within each book. After that, the books are grouped into the three historical periods as well as we specifically remove the words appearing in fewer than five different texts, in order to get a better sample size.

#### Thematic-tag comparison

During our analysis, we also wanted to see what kind of themes were more prevalent during the time periods.

#### Book length

During our analysis, we also found necessary later on to determine how long each book was during periods, as there could be some data that would be possible to theorize if we determine the book length. For example, during our analysis we found an outlier and we needed to determine why this outlier existed.

#### Book-level scatter plot

As mentioned in the previous method, there was an outlier that we needed to identify, and for this, we resorted to a scatter plot from books that were published before World War II. As we were comparing the data, we were noticing certain patterns that did not make much sense.

# Performing the analysis

### Top 15 words

The first step we made was to look for the first top 15 words that are the less frequent using the TF-IDF analysis. Which is displayed in Figure 1 below.

As it can be seen in this figure, there is some prevalence of space related words during WW2, for example, words such as "Blaster," "Terran," "Spacer" can be seen. Before and after seem to show a bigger prevalence of unique words related to people's name. However, "fbi" can be seen in the "After WW2" section, suggesting there could be some themes of espionage in later books. I mainly say this given that in the book by _Science Fiction: A Very Short Introduction_ it was seems that there is some books that mention the CIA and FBI, such as Walter Tevis's _The Man Who Fell to Earth_ (1963). This book is not available in this corpus, but it is to mainly give you an idea.

### Top 100 words

When increasing the scope beyond the top 15 words, we notice that there are some words that start being more apparent that others. Take a look into figure 2.

Here, if we look into the new words that popped during World War 2, we notice that there are words such as "mercurians," "spacemen," "spaceships," "spacecraft." Words that are also related to themes of science fiction and space can be seen on the list of words from after World War 2. Such as "contragravity," "computers," "starship," "spaceport."

It might be natural that the writers felt more inclined to write towards ideas of very advanced spaceships that go through space given the technological development of the time, as well as the increase sight seeing of planes during the time of war as well as computational advances. However, when we were looking at the results from here, the name "Tarzan" popping out many times and as frequent as it was, it made us make some tests to see if our code for analysis was inherently broken, as we did not know why Tarzan, which we associate with Disney's version of Tarzan, recognizing that it is inspired by a book, was appearing as much.

### Looking at tags
