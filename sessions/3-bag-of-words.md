## Session 3: Bag-of-Words Method

**Track:** 1 — AI & Big Data in Econ/Fin
**Date:** TBD
**Presenter:** TBD

### Overview
If words or phrases associated with a construct appear in a text, their occurrence or frequency can be used as a proxy for how much the text discusses that construct.

### Readings
- Baker, Bloom, and Davis — *Measuring Economic Policy Uncertainty*: counts newspaper articles where terms for "economy/economic," "uncertainty/uncertain," and a policy-related word all co-occur, and uses that count as the uncertainty index.
- Hassan et al. — *Firm-Level Political Risk: Measurement and Effects*: searches earnings call transcripts for political bigrams, then checks whether a risk/uncertainty synonym shows up within a fixed word window around each hit.
- Hassan et al. — *Sources and Transmission of Country Risk*: builds a country-specific dictionary via TF-IDF over country-related documents, searches transcripts for that dictionary, and checks whether "risk" appears nearby within some window.
- Campbell et al. — *The Information Content of Mandatory Risk Factor Disclosures in Corporate Filings*: runs LDA on the Item 1A (Risk Factors) section of 10-Ks to mine out what topics/words actually show up there.
- Wu — *Text-Based Measure of Supply Chain Risk Exposure*: starts from seed words, uses BERT embeddings to find semantically similar terms, and expands those seeds into a full dictionary.
- Kalyani, Bloom, Carvalho, Hassan, Lerner, and Tahoun — *The Diffusion of New Technologies*: extracts bigrams from patents, filters them against COHA and Wikipedia to keep only genuine technology phrases, then searches job postings and earnings calls for those phrases to track diffusion.

### Notes / Slides

#### 1. Keyword Counts
Start with a predefined set of words and count how often they appear.

**Example:** Baker, Bloom, and Davis — *Measuring Economic Policy Uncertainty*

**Problem:** A single word can have multiple meanings and ignores context.

#### 2. N-grams
Use combinations of words, such as bigrams or trigrams, to capture more local context.

**Example:** Hassan et al. — *Firm-Level Political Risk: Measurement and Effects*

**Example:** Kalyani et al. — *The Diffusion of New Technologies*. Represents every patent as its set of bigrams (kept because "autonomous vehicle" or "cloud computing" are far less ambiguous than the unigrams "vehicle" or "cloud"), then narrows 17 million candidate bigrams down to a clean list of technology phrases through successive filters — see #4 below for how.

#### 3. TF-IDF
Some words appear everywhere and therefore contain little information.

TF-IDF gives more weight to terms that are common in the relevant text but uncommon elsewhere.

**Example:** Hassan et al. — *Sources and Transmission of Country Risk*

**Key idea:** frequency does not necessarily mean informativeness.

#### 4. Where Does the Word List Come From?
The main challenge is often not counting words, but deciding **which words to count**.

**Topic Models / LDA** — Use the corpus itself to discover groups of related words.
Example: Campbell et al. — *The Information Content of Mandatory Risk Factor Disclosures in Corporate Filings*

**External Training Corpus** — Use texts already known to represent a construct and identify characteristic words or phrases.
Example: *Sources and Transmission of Country Risk*

Example: Kalyani et al. — *The Diffusion of New Technologies* stacks two external corpora as sequential filters on patent bigrams: (1) the *Corpus of Historical American English* (pre-1970 text) removes bigrams that aren't actually novel, and (2) Wikipedia is used to keep only the bigrams matched to a page that reads as a technology (sections like "application," "device," "technical") rather than a problem or management term (sections like "symptoms," "risk assessment," "customer"). ~17M candidate bigrams → 1,899 technology phrases. A good illustration of chaining external corpora rather than relying on one dictionary.

**Embeddings** — Start with seed words and use semantic similarity to expand the dictionary.
Example: Wu — *Text-Based Measure of Supply Chain Risk Exposure*

#### Why Use Bag of Words in the LLM Era?
- Easy to interpret
- Easy to reproduce
- Cheap to run at scale
- Easy to validate
- Can run locally on sensitive or administrative data
- Useful as a transparent benchmark for LLM-based measures

**Bottom line:** LLMs do not eliminate bag-of-words methods. Bag of words remains a simple, transparent, and useful way to turn text into variables.

[← Back to home](../index.md)
