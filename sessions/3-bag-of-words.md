## Session 3: Bag-of-Words Method

**Track:** 1 — AI & Big Data in Econ/Fin
**Date:** TBD
**Presenter:** TBD

### Overview
If words or phrases associated with a construct appear in a text, their occurrence or frequency can be used as a proxy for how much the text discusses that construct.

### Readings
- Baker, Bloom, and Davis — *Measuring Economic Policy Uncertainty*
- Hassan et al. — *Firm-Level Political Risk: Measurement and Effects*
- Hassan et al. — *Sources and Transmission of Country Risk*
- Campbell et al. — *The Information Content of Mandatory Risk Factor Disclosures in Corporate Filings*
- Wu — *Text-Based Measure of Supply Chain Risk Exposure*

### Notes / Slides

#### 1. Keyword Counts
Start with a predefined set of words and count how often they appear.

**Example:** Baker, Bloom, and Davis — *Measuring Economic Policy Uncertainty*

**Problem:** A single word can have multiple meanings and ignores context.

#### 2. N-grams
Use combinations of words, such as bigrams or trigrams, to capture more local context.

**Example:** Hassan et al. — *Firm-Level Political Risk: Measurement and Effects*

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
