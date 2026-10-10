---
permalink: /assignment-1/
title: "Assignment 1"
---

_Use of A.I. Disclosure: We used Claude Code and Copilot to write the logic for the data analysis. We made sure that it outputs what we need in accordance to what we were seeking for._

## Table of Contents

- [Introduction](#introduction)
  - [What we were looking for?](#what-we-were-looking-for)
  - [Hypothesis](#hypothesis)
  - [The method](#the-method)
    - [a. Distinctive vocabulary using TF-IDF](#a-distinctive-vocabulary-using-tf-idf)
    - [b. Thematic-tag comparison](#b-thematic-tag-comparison)
    - [c. Book length](#c-book-length)
    - [d. Book-level scatter plot](#d-book-level-scatter-plot)
- [Performing the analysis](#performing-the-analysis)
  - [a. Top 15 words](#a-top-15-words)
  - [b. Top 100 words](#b-top-100-words)
  - [c. Looking at tags](#c-looking-at-tags)
  - [d. Average length](#d-average-length)

---

# Introduction

---

### What we were looking for?

During the discussion we had, we noticed that Saeed Syed and me were really interested in checking if there was some kind of words related to space and their rate of frequency before, during (which was during 1939 to 1945) and after World War 2.

According to the reading by David Seed: _Science Fiction: A Very Short Introduction_ after World War 2 (34) there was a interest in exploring themes of alien invansions, with the whole ideas of "conquer or be conquered." There can be interesting facts about it, or some words that appear to be more frequent during specific times, but it is something we will be exploring during the course of this analysis.

### Hypothesis

Books written in the WW2 era will have more words related to science fiction as well as possess the war tag more than the rest in the science fiction corpus.

### The method

In order to analyze this, we used the following techniques, with the reasoning as to why we choose them:

#### a. Distinctive vocabulary using TF-IDF

The first analytical method deployed during our analysis was the TF-IDF, or short term for _term frequency-inverse document frequency_. This is a used to identify words that are especially characteristic of one group compared with other groups. In this case, we are tokenizing each book into individual words, removing any kind of punctuation, numbers, and common English stop words; all the books written in the corpus seem to be in English.

After tokenizing, the words frequencies are then counted within each book. After that, the books are grouped into the three historical periods as well as we specifically remove the words appearing in fewer than five different texts, in order to get a better sample size.

#### b. Thematic-tag comparison

During our analysis, we also wanted to see what kind of themes were more prevalent during the time periods.

#### c. Book length

During our analysis, we also found necessary later on to determine how long each book was during periods, as there could be some data that would be possible to theorize if we determine the book length. For example, during our analysis we found an outlier and we needed to determine why this outlier existed.

#### d. Book-level scatter plot

As mentioned in the previous method, there was an outlier that we needed to identify, and for this, we resorted to a scatter plot from books that were published before World War II. As we were comparing the data, we were noticing certain patterns that did not make much sense.

---

# Performing the analysis

---

### a. Top 15 words

The first step we made was to look for the first top 15 words that are the less frequent using the TF-IDF analysis. Which is displayed in Figure 1 below.

<figure>
  <img src="{{ '/assets/images/assignment1/distinctive_words_top15.png' | relative_url }}" alt="Top 15 distinctive words by period">
  <figcaption>Figure 1. Top 15 distinctive words before, during, and after World War II.</figcaption>
</figure>

As it can be seen in this figure, there is some prevalence of space related words during WW2, for example, words such as "Blaster," "Terran," "Spacer" can be seen. Before and after seem to show a bigger prevalence of unique words related to people's name. However, "fbi" can be seen in the "After WW2" section, suggesting there could be some themes of espionage in later books. I mainly say this given that in the book by _Science Fiction: A Very Short Introduction_ it was seems that there is some books that mention the CIA and FBI, such as Walter Tevis's _The Man Who Fell to Earth_ (1963). This book is not available in this science fiction corpus, but it is to mainly give you an idea.

### b. Top 100 words

When increasing the scope beyond the top 15 words, we notice that there are some words that start being more apparent that others. Take a look into figure 2.

<figure>
  <button class="figure-zoom-trigger" type="button" aria-haspopup="dialog" aria-controls="figure-2-lightbox">
    <img src="{{ '/assets/images/assignment1/distinctive_words_top100.png' | relative_url }}" alt="Top 100 distinctive words by period">
    <span>Click to maximize</span>
  </button>
  <figcaption>Figure 2. Top 100 distinctive words before, during, and after World War II.</figcaption>
</figure>

<div class="figure-lightbox" id="figure-2-lightbox" role="dialog" aria-modal="true" aria-labelledby="figure-2-lightbox-title" hidden>
  <div class="figure-lightbox__content">
    <button class="figure-lightbox__close" type="button" aria-label="Close maximized Figure 2">&times;</button>
    <h2 id="figure-2-lightbox-title">Figure 2. Top 100 distinctive words</h2>
    <div class="figure-lightbox__controls" aria-label="Figure zoom controls">
      <button type="button" class="figure-lightbox__zoom-out" aria-label="Zoom out">−</button>
      <span class="figure-lightbox__zoom-level">100%</span>
      <button type="button" class="figure-lightbox__zoom-in" aria-label="Zoom in">+</button>
      <button type="button" class="figure-lightbox__zoom-reset">Reset</button>
    </div>
    <div class="figure-lightbox__viewport">
      <img class="figure-lightbox__image" src="{{ '/assets/images/assignment1/distinctive_words_top100.png' | relative_url }}" alt="Top 100 distinctive words by period">
    </div>
  </div>
</div>

<style>
  .figure-zoom-trigger {
    position: relative;
    display: block;
    width: 100%;
    padding: 0;
    border: 0;
    background: transparent;
    cursor: zoom-in;
  }

  .figure-zoom-trigger img {
    display: block;
    width: 100%;
  }

  .figure-zoom-trigger span {
    position: absolute;
    right: 1rem;
    bottom: 1rem;
    padding: 0.45rem 0.7rem;
    color: #fff;
    background: rgb(0 0 0 / 75%);
    border-radius: 0.25rem;
    font-size: 0.9rem;
  }

  .figure-lightbox {
    position: fixed;
    inset: 0;
    z-index: 1000;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    padding: 2rem;
    overflow: auto;
    background: rgb(0 0 0 / 90%);
  }

  .figure-lightbox[hidden] {
    display: none;
  }

  .figure-lightbox__content {
    position: relative;
    width: min(95vw, 1400px);
    margin-top: 2rem;
    text-align: center;
  }

  .figure-lightbox h2 {
    margin: 0 0 1rem;
    color: #fff;
    font-size: 1.1rem;
  }

  .figure-lightbox__controls {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    margin-bottom: 0.75rem;
  }

  .figure-lightbox__controls button,
  .figure-lightbox__zoom-level {
    min-width: 2.25rem;
    padding: 0.35rem 0.65rem;
    color: #111;
    border: 1px solid #ccc;
    border-radius: 0.25rem;
    background: #fff;
    font-size: 1rem;
  }

  .figure-lightbox__controls button {
    cursor: pointer;
  }

  .figure-lightbox__zoom-level {
    min-width: 4.5rem;
  }

  .figure-lightbox__viewport {
    max-width: 95vw;
    max-height: 78vh;
    overflow: auto;
    background: #222;
    text-align: left;
  }

  .figure-lightbox__image {
    display: block;
    width: 100%;
    max-width: none;
    height: auto;
  }

  .figure-lightbox__close {
    position: absolute;
    top: -2.5rem;
    right: 0;
    color: #fff;
    border: 0;
    background: transparent;
    cursor: pointer;
    font-size: 2rem;
    line-height: 1;
  }

  body.figure-lightbox-open {
    overflow: hidden;
  }
</style>

<script>
  (function () {
    const trigger = document.querySelector('.figure-zoom-trigger');
    const lightbox = document.getElementById('figure-2-lightbox');
    const closeButton = lightbox.querySelector('.figure-lightbox__close');
    const image = lightbox.querySelector('.figure-lightbox__image');
    const zoomLevel = lightbox.querySelector('.figure-lightbox__zoom-level');
    let zoom = 1;

    function updateZoom() {
      image.style.width = `${image.naturalWidth * zoom}px`;
      zoomLevel.textContent = `${Math.round(zoom * 100)}%`;
    }

    function closeLightbox() {
      lightbox.hidden = true;
      document.body.classList.remove('figure-lightbox-open');
      trigger.focus();
    }

    trigger.addEventListener('click', function () {
      lightbox.hidden = false;
      document.body.classList.add('figure-lightbox-open');
      zoom = 1;
      updateZoom();
      closeButton.focus();
    });

    image.addEventListener('load', updateZoom);
    lightbox.querySelector('.figure-lightbox__zoom-in').addEventListener('click', function () {
      zoom = Math.min(zoom + 0.25, 3);
      updateZoom();
    });
    lightbox.querySelector('.figure-lightbox__zoom-out').addEventListener('click', function () {
      zoom = Math.max(zoom - 0.25, 0.5);
      updateZoom();
    });
    lightbox.querySelector('.figure-lightbox__zoom-reset').addEventListener('click', function () {
      zoom = 1;
      updateZoom();
    });
    closeButton.addEventListener('click', closeLightbox);
    lightbox.addEventListener('click', function (event) {
      if (event.target === lightbox) {
        closeLightbox();
      }
    });
    document.addEventListener('keydown', function (event) {
      if (event.key === 'Escape' && !lightbox.hidden) {
        closeLightbox();
      }
    });
  }());
</script>

Here, if we look into the new words that popped during World War 2, we notice that there are words such as "mercurians," "spacemen," "spaceships," "spacecraft." Words that are also related to themes of science fiction and space can be seen on the list of words from after World War 2. Such as "contragravity," "computers," "starship," "spaceport."

It might be natural that the writers felt more inclined to write towards ideas of very advanced spaceships that go through space given the technological development of the time, as well as the increase sight seeing of planes during the time of war as well as computational advances. However, when we were looking at the results from here, the name "Tarzan" popping out many times and as frequent as it was, it made us make some tests to see if our code for analysis was inherently broken, as we did not know why Tarzan, which we associate with Disney's version of Tarzan, recognizing that it is inspired by a book, was appearing as much.

### c. Looking at tags

The five tags that are available in the science fiction corpus are: action, mars, society, space travel and war. Although, we were not sure of the frequencies during the time periods we set in, so we made an analysis of the tag frequencies, as it can be seen in the following picture

<figure>
  <img src="{{ '/assets/images/assignment1/tag_comparison_before_during_after_ww2.png' | relative_url }}" alt="Comparison of thematic tags before, during, and after World War II">
  <figcaption>Figure 3. Thematic-tag comparison before, during, and after World War II.</figcaption>
</figure>

It can be noticed that, before WW2, there was still some interest in themes of action (78%) and war (47.2%). However, when it came to space travel, there was no much interest, since it was around a 23.6%, compared to during WW2 when it increased to a 81.4% and after WW2 which lowered to a 59.4%. This again, could correlate to the possibility of writers being fascinated by the technological advacenments of the time.

### d. Average length

During our analysis for the top 100 words, we became curious as to why Tarzan was appearing so consistently. So we

<figure>
  <img src="{{ '/assets/images/assignment1/average_length_before_during_after_ww2.png' | relative_url }}" alt="Average book length before, during, and after World War II">
  <figcaption>Figure 4. Average book length before, during, and after World War II.</figcaption>
</figure>
