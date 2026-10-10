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
    - [a. Frequent words](#a-frequent-words)
    - [b. Distinctive vocabulary using TF-IDF](#b-distinctive-vocabulary-using-tf-idf)
    - [c. Thematic-tag comparison](#c-thematic-tag-comparison)
    - [d. Book length](#d-book-length)
    - [e. Book-level scatter plot](#e-book-level-scatter-plot)
- [Performing the analysis](#performing-the-analysis)
  - [a. Frequent Words](#a-frequent-words-1)
  - [b. Top 15 distinctive words](#b-top-15-distinctive-words)
  - [c. Top 100 distinctive words](#c-top-100-distinctive-words)
  - [d. Looking at tags](#d-looking-at-tags)
  - [e. Average length and scatter plot to determine what is happening with "Tarzan"](#e-average-length-and-scatter-plot-to-determine-what-is-happening-with-tarzan)
- [Summary of our findings](#summary-of-our-findings)
- [Conclusion](#conclusion)
  - [What our hypothesis correct?](#what-our-hypothesis-correct)
  - [What can we improve?](#what-can-we-improve)

---

# Introduction

---

### What we were looking for?

During the discussion we had, we noticed that Saeed Syed and I were really interested in checking whether there were words related to space and how frequently they appeared before, during (1939 to 1945), and after World War II (WW2).

According to David Seed’s _Science Fiction: A Very Short Introduction_, after World War II there was an interest in exploring themes of alien invasions, including the idea of “conquer or be conquered” (34). There could be interesting findings about this, or words that appear more frequently during specific periods, which is something we will explore during this analysis.

### Hypothesis

Books written during the WW2 era will have more words related to science fiction and will be more likely to possess the war tag than the rest of the science fiction corpus.

### The method

In order to analyze this, we used the following techniques. We also explain why we chose them.

### a. Frequent words

This is a very basic analysis, but even though it is basic, it is important to have an idea of which words commonly appear in the books. For example, some words might appear very frequently within a specific number of words. In this case, we measured their frequency per 1,000 words.

#### b. Distinctive vocabulary using TF-IDF

The first analytical method we used was TF-IDF, short for _term frequency-inverse document frequency_. This method is used to identify words that are especially characteristic of one group compared with other groups. In this case, we tokenized each book into individual words, removing punctuation, numbers, and common English stop words. All the books in the corpus seem to be in English.

After tokenizing, we counted the word frequencies within each book. We then grouped the books into the three historical periods and removed words appearing in fewer than five different texts in order to get a better sample size.

#### c. Thematic-tag comparison

During our analysis, we also wanted to see what kinds of themes were more prevalent during the different time periods.

#### d. Book length

During our analysis, we later found it necessary to determine how long each book was in the different periods, as this could help us theorize about the data. For example, we found an outlier and needed to determine why it existed.

#### e. Book-level scatter plot

As mentioned in the previous method, there was an outlier that we needed to identify. For this, we used a scatter plot of books published before World War II. As we compared the data, we noticed certain patterns that did not make much sense.

---

# Performing the analysis

---

### a. Frequent Words

We started by identifying the top 15 most frequent words per 1,000 words, excluding stop words, for the periods before, during, and after World War II. As mentioned in the method, we did this initially to see whether some words appeared more frequently across the whole science fiction corpus. Indeed, we noticed something peculiar at first in the results shown in Figure 1:

<figure>
  <button class="figure-zoom-trigger" type="button" aria-haspopup="dialog" aria-controls="figure-lightbox">
    <img src="{{ '/assets/images/assignment1/frequent_words_top15.png' | relative_url }}" alt="Top 15 most frequent words per 1000 words by period">
    <span>Click to maximize</span>
  </button>
  <figcaption>Figure 1. Top 15 most frequent words per 1000 words before, during, and after World War II.</figcaption>
</figure>

In this figure, we can see that there are no space-related words before World War II, compared with the “During WW2” and “After WW2” periods. For example, during World War II, some words related to space appear, such as “ship” and “space.” After World War II, the only word that appears to be related to space themes is “ship,” although it could be argued that “earth” is another, depending on how some writers use it in their narratives.

### b. Top 15 distinctive words

The first step we took was to look at the top 15 most distinctive words using TF-IDF analysis. These are displayed in Figure 2 below.

<figure>
  <button class="figure-zoom-trigger" type="button" aria-haspopup="dialog" aria-controls="figure-lightbox">
    <img src="{{ '/assets/images/assignment1/distinctive_words_top15.png' | relative_url }}" alt="Top 15 distinctive words by period">
    <span>Click to maximize</span>
  </button>
  <figcaption>Figure 2. Top 15 distinctive words before, during, and after World War II.</figcaption>
</figure>

As can be seen in this figure, there is some prevalence of space-related words during WW2. For example, words such as “blaster,” “Terran,” and “spacer” can be seen. The periods before and after the war seem to show a greater prevalence of distinctive words related to people’s names. However, “FBI” can be seen in the “After WW2” section, suggesting that there could be themes of espionage in later books. I mainly say this because _Science Fiction: A Very Short Introduction_ discusses books that mention the CIA and FBI, such as Walter Tevis’s _The Man Who Fell to Earth_ (1963). This book is not available in our science fiction corpus, but I mention it mainly to give you an idea.

### c. Top 100 distinctive words

When increasing the scope beyond the top 15 words, we noticed that some words became more apparent than others. Take a look at Figure 3.

<figure>
  <button class="figure-zoom-trigger" type="button" aria-haspopup="dialog" aria-controls="figure-lightbox">
    <img src="{{ '/assets/images/assignment1/distinctive_words_top100.png' | relative_url }}" alt="Top 100 distinctive words by period">
    <span>Click to maximize</span>
  </button>
  <figcaption>Figure 3. Top 100 distinctive words before, during, and after World War II.</figcaption>
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

### d. Looking at tags

The five tags available in the science fiction corpus are action, Mars, society, space travel, and war. However, we were not sure how frequently they appeared during the time periods we had set, so we analyzed the tag frequencies, as can be seen in the following picture.

<figure>
  <button class="figure-zoom-trigger" type="button" aria-haspopup="dialog" aria-controls="figure-lightbox">
    <img src="{{ '/assets/images/assignment1/tag_comparison_before_during_after_ww2.png' | relative_url }}" alt="Comparison of thematic tags before, during, and after World War II">
    <span>Click to maximize</span>
  </button>
  <figcaption>Figure 4. Thematic-tag comparison before, during, and after World War II.</figcaption>
</figure>

It can be noticed that, before WW2, there was still some interest in themes of action (78%) and war (47.2%). However, when it came to space travel, there was not as much interest, since the figure was around 23.6%. This increased to 81.4% during WW2 and then lowered to 59.4% after WW2. Again, this could be related to the possibility of writers being fascinated by the technological advancements of the time.

### e. Average length and scatter plot to determine what is happening with "Tarzan"

During our analysis of the top distinctive words, we became curious about why “Tarzan” appeared so consistently. For example, before the cleanup, Tarzan appeared a lot in our data analysis! This did not make much sense to us, so we ran some code to estimate what was happening with the name and why it was so frequent. We imagined that someone might have written a long book that mentioned Tarzan many times, as can be seen in the following figure.

<figure>
  <button class="figure-zoom-trigger" type="button" aria-haspopup="dialog" aria-controls="figure-lightbox">
    <img src="{{ '/assets/images/assignment1/average_length_before_during_after_ww2.png' | relative_url }}" alt="Average book length before, during, and after World War II">
    <span>Click to maximize</span>
  </button>
  <figcaption>Figure 5. Average book length before, during, and after World War II.</figcaption>
</figure>

We became suspicious of this, but after creating a scatter plot that took into account the word counts and publication years of books published before World War II, we noticed that the extreme outlier, The Outline of History, did not seem to have anything to do with Tarzan. Instead, there was a book with Tarzan in its title: _Tarzan the Untamed_. This was making the data appear strange.

<figure>
  <button class="figure-zoom-trigger" type="button" aria-haspopup="dialog" aria-controls="figure-lightbox">
    <img src="{{ '/assets/images/assignment1/book_length_scatter_before_ww2.png' | relative_url }}" alt="Scatter plot of book length and publication year before World War II">
    <span>Click to maximize</span>
  </button>
  <figcaption>Figure 6. Book length and publication year before World War II.</figcaption>
</figure>

We could _not_ ignore the elephant in the room by skipping this detail.

---

# Summary of our findings

---

After doing this analysis, we noticed that the periods during and after World War II did show a significant interest in space. New distinctive words appeared, and the space-related tags became more frequent. As of right now, there is not much we can hypothesize beyond showing that there was an increased interest in these themes. During our discussion, we considered the idea that this could have been because of rapid technological developments. We also wondered whether people were tired of conflicts in the real world and wanted to explore what lay beyond Earth. These are just possible explanations, so they have to be taken with a grain of salt.

In summary, there was an increased interest in space, extraterrestrials, and other planets, especially during World War II. There was also an interest in war-themed books, which surprisingly dropped after World War II.

---

# Conclusion

---

### What our hypothesis correct?

To a degree, it is. However, we cannot safely draw that conclusion, given the exploratory nature of this exercise. As of now, our analysis points toward writers being really interested in exploring themes of space. Look especially at how quickly the space travel tag became more frequent in the figure showing tag frequencies by period. As to why this happened, we cannot safely say. There could have been multiple reasons, and they may have varied from writer to writer.

After all, we are doing distant reading. We are not really engaging with the contents of the books themselves, as reading them all would take us years within a realistic reading schedule. That is where the magic of distant reading lies, though: we can get an idea of what the books are about without spending years of our lives reading them.

### What can we improve?

We could have taken a closer look at each of the books that were outliers and analyzed them to reach different conclusions. For example, we could have used the “Most Distinctive Words” method, which was taught to us in class. With this method, we would take a set of different books and analyze what kinds of correlations there are between words. However, given the time Saeed and I had, we could not do this during our analysis.

Not only that, but we could also have provided some quotes from the books to give an idea of how frequently interesting words such as “earth,” “Tarzan,” and “Mercurians” appeared.

READY FOR GRADING
