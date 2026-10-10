---
permalink: /assignment-1/
title: "Assignment 1"
---

<!-- Scripts and stuff -->

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
  document.addEventListener('DOMContentLoaded', function () {
    const triggers = document.querySelectorAll('.figure-zoom-trigger');
    const lightbox = document.getElementById('figure-lightbox');
    const closeButton = lightbox.querySelector('.figure-lightbox__close');
    const title = lightbox.querySelector('#figure-lightbox-title');
    const image = lightbox.querySelector('.figure-lightbox__image');
    const zoomLevel = lightbox.querySelector('.figure-lightbox__zoom-level');
    let activeTrigger;
    let zoom = 1;

    function updateZoom() {
      image.style.width = `${image.naturalWidth * zoom}px`;
      zoomLevel.textContent = `${Math.round(zoom * 100)}%`;
    }

    function closeLightbox() {
      lightbox.hidden = true;
      document.body.classList.remove('figure-lightbox-open');
      activeTrigger.focus();
    }

    triggers.forEach(function (trigger) {
      trigger.addEventListener('click', function () {
        const sourceImage = trigger.querySelector('img');
        const caption = trigger.parentElement.querySelector('figcaption').textContent;

        activeTrigger = trigger;
        image.src = sourceImage.src;
        image.alt = sourceImage.alt;
        title.textContent = caption;
        lightbox.hidden = false;
        document.body.classList.add('figure-lightbox-open');
        zoom = 1;
        updateZoom();
        closeButton.focus();
      });
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
  });
</script>

<!-- END OF THAT -->

_Use of A.I. Disclosure and how did we work together: We used Claude Code and Copilot to write the logic for the data analysis. We made sure that it outputs what we need in accordance to what we were seeking for. As for the individual assignments, we made the data analysis process together, but we wrote the essays independently._

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

During the discussion we had, we noticed that Saeed Syed and I were really interested in checking whether there were words related to space and how frequently they appeared before, during (1939 to 1945), and after World War II.

According to David Seed’s _Science Fiction: A Very Short Introduction_, after World War II there was an interest in exploring themes of alien invasions, including the idea of “conquer or be conquered” (34). There could be interesting findings about this, or words that appear more frequently during specific periods, which is something we will explore during this analysis.

### Hypothesis

Books written during the WW2 era will have more words related to science fiction and will be more likely to possess the war tag than the rest of the science fiction corpus.

### The method

In order to analyze this, we used the following techniques. We also explain why we chose them.

#### a. Distinctive vocabulary using TF-IDF

The first analytical method we used was TF-IDF, short for _term frequency-inverse document frequency_. This method is used to identify words that are especially characteristic of one group compared with other groups. In this case, we tokenized each book into individual words, removing punctuation, numbers, and common English stop words. All the books in the corpus seem to be in English.

After tokenizing, we counted the word frequencies within each book. We then grouped the books into the three historical periods and removed words appearing in fewer than five different texts in order to get a better sample size.

#### b. Thematic-tag comparison

During our analysis, we also wanted to see what kinds of themes were more prevalent during the different time periods.

#### c. Book length

During our analysis, we later found it necessary to determine how long each book was in the different periods, as this could help us theorize about the data. For example, we found an outlier and needed to determine why it existed.

#### d. Book-level scatter plot

As mentioned in the previous method, there was an outlier that we needed to identify. For this, we used a scatter plot of books published before World War II. As we compared the data, we noticed certain patterns that did not make much sense.

---

# Performing the analysis

---

### a. Top 15 words

The first step we took was to look at the top 15 most distinctive words using TF-IDF analysis. These are displayed in Figure 1 below.

<figure>
  <button class="figure-zoom-trigger" type="button" aria-haspopup="dialog" aria-controls="figure-lightbox">
    <img src="{{ '/assets/images/assignment1/distinctive_words_top15.png' | relative_url }}" alt="Top 15 distinctive words by period">
    <span>Click to maximize</span>
  </button>
  <figcaption>Figure 1. Top 15 distinctive words before, during, and after World War II.</figcaption>
</figure>

As can be seen in this figure, there is some prevalence of space-related words during WW2. For example, words such as “blaster,” “Terran,” and “spacer” can be seen. The periods before and after the war seem to show a greater prevalence of distinctive words related to people’s names. However, “FBI” can be seen in the “After WW2” section, suggesting that there could be themes of espionage in later books. I mainly say this because _Science Fiction: A Very Short Introduction_ discusses books that mention the CIA and FBI, such as Walter Tevis’s _The Man Who Fell to Earth_ (1963). This book is not available in our science fiction corpus, but I mention it mainly to give you an idea.

### b. Top 100 words

When increasing the scope beyond the top 15 words, we noticed that some words became more apparent than others. Take a look at Figure 2.

<figure>
  <button class="figure-zoom-trigger" type="button" aria-haspopup="dialog" aria-controls="figure-lightbox">
    <img src="{{ '/assets/images/assignment1/distinctive_words_top100.png' | relative_url }}" alt="Top 100 distinctive words by period">
    <span>Click to maximize</span>
  </button>
  <figcaption>Figure 2. Top 100 distinctive words before, during, and after World War II.</figcaption>
</figure>

<div class="figure-lightbox" id="figure-lightbox" role="dialog" aria-modal="true" aria-labelledby="figure-lightbox-title" hidden>
  <div class="figure-lightbox__content">
    <button class="figure-lightbox__close" type="button" aria-label="Close maximized figure">&times;</button>
    <h2 id="figure-lightbox-title"></h2>
    <div class="figure-lightbox__controls" aria-label="Figure zoom controls">
      <button type="button" class="figure-lightbox__zoom-out" aria-label="Zoom out">−</button>
      <span class="figure-lightbox__zoom-level">100%</span>
      <button type="button" class="figure-lightbox__zoom-in" aria-label="Zoom in">+</button>
      <button type="button" class="figure-lightbox__zoom-reset">Reset</button>
    </div>
    <div class="figure-lightbox__viewport">
      <img class="figure-lightbox__image" src="" alt="">
    </div>
  </div>
</div>

If we look at the new words that appeared during World War II, we notice words such as “Mercurians,” “spacemen,” “spaceships,” and “spacecraft.” Words related to science fiction and space can also be seen on the list of words from after World War II, such as “contragravity,” “computers,” “starship,” and “spaceport.”

It might be natural that writers felt more inclined to write about ideas of very advanced spaceships traveling through space, given the technological developments of the time, the increased visibility of planes during the war, and advances in computing. However, when we looked at the results, the name “Tarzan” appeared many times. Because it appeared so frequently, we ran some tests to see whether our code for the analysis was broken. We did not know why Tarzan, whom we associate with Disney’s version of the character, although we recognize that it was inspired by a book, was appearing so much.

### c. Looking at tags

The five tags available in the science fiction corpus are action, Mars, society, space travel, and war. However, we were not sure how frequently they appeared during the time periods we had set, so we analyzed the tag frequencies, as can be seen in the following picture.

<figure>
  <button class="figure-zoom-trigger" type="button" aria-haspopup="dialog" aria-controls="figure-lightbox">
    <img src="{{ '/assets/images/assignment1/tag_comparison_before_during_after_ww2.png' | relative_url }}" alt="Comparison of thematic tags before, during, and after World War II">
    <span>Click to maximize</span>
  </button>
  <figcaption>Figure 3. Thematic-tag comparison before, during, and after World War II.</figcaption>
</figure>

It can be noticed that, before WW2, there was still some interest in themes of action (78%) and war (47.2%). However, when it came to space travel, there was not as much interest, since the figure was around 23.6%. This increased to 81.4% during WW2 and then lowered to 59.4% after WW2. Again, this could be related to the possibility of writers being fascinated by the technological advancements of the time.

### d. Average length and scatter plot to determine what is happening with "Tarzan"

During our analysis of the top distinctive words, we became curious about why “Tarzan” appeared so consistently. For example, before the cleanup, Tarzan appeared a lot in our data analysis! This did not make much sense to us, so we ran some code to estimate what was happening with the name and why it was so frequent. We imagined that someone might have written a long book that mentioned Tarzan many times, as can be seen in the following figure.

<figure>
  <button class="figure-zoom-trigger" type="button" aria-haspopup="dialog" aria-controls="figure-lightbox">
    <img src="{{ '/assets/images/assignment1/average_length_before_during_after_ww2.png' | relative_url }}" alt="Average book length before, during, and after World War II">
    <span>Click to maximize</span>
  </button>
  <figcaption>Figure 4. Average book length before, during, and after World War II.</figcaption>
</figure>

We became suspicious of this, but after creating a scatter plot that took into account the word counts and publication years of books published before World War II, we noticed that the extreme outlier, The Outline of History, did not seem to have anything to do with Tarzan. Instead, there was a book with Tarzan in its title: _Tarzan the Untamed_. This was making the data appear strange.

assets\images\assignment1\book_length_scatter_before_ww2.png

We could _not_ ignore the elephant in the room by skipping this detail.

---

# Summary of our findings

---
