# Synthetic Reading of O. Henry's "The Gift of the Magi"

A reader-oriented, language-model-assisted analysis of how the narrator's language turns economic loss into emotional value in O. Henry's short story "The Gift of the Magi" (1905). A short partial reading by the researcher gives four dimensions of analysis. A language model extracts matching words and phrases from the full text, and the phrases are verified, counted across the story and interpreted.

**Author:** Aditya Kumar

**Semester:** Monsoon Semester 2026

**Affiliation:** Department of Humanities and Social Sciences, Indian Institute of Technology (Indian School of Mines), Dhanbad

**Project webpage:** https://adityakumar190.github.io/synthetic_reading_gift_of_the_magi/

**Source text:** O. Henry, "The Gift of the Magi" (1905), Project Gutenberg: https://www.gutenberg.org/cache/epub/7256/pg7256-images.html

## Research question

How does the narrator's language turn economic loss into emotional value, and what does the reader learn to call "wise"?

**Claim tested:** Words of shame, counting and selling are concentrated in the first two stages of the story, while words of wisdom and the narrator's comments are concentrated in the last stage.

## Dimensions

| Dimension | Sub-types |
|---|---|
| Transactional shaming | amounts of money; counting, saving and bargaining; shame and want |
| Corporeal commodification | body as sellable; price, sale and exchange; reaction to the sale |
| Objects and feeling | gifts and possessions; qualities of objects; feelings attached |
| Paradoxical value inversion | wisdom and foolishness; narrator's comments; ironic register |

## Main results

The extraction gave 152 verified phrases and 193 occurrences in 2,057 words (9.4 per 100 words), counted across 13 segments and four stages.

- **Shame and counting come first.** 29 of 37 shame hits and all 11 counting hits are in Stage I. Shame falls from 5.86 to 0.00 hits per 100 words across the four stages.
- **Selling has two peaks.** The sale to Madame Sofronie (segment 5) and Della's confession to Jim (segment 9).
- **Value moves onto the gifts.** Objects and feeling is the largest dimension (72 hits) and is densest around the combs (segment 11) and in Stage IV (7.33 per 100 words).
- **Wisdom arrives at the end.** Value inversion rises from about 1.6 to 4.02 in Stage IV, and 11 of the 14 wisdom hits are in the final paragraph.
- **The claim is partly supported.** Shame and counting are early, but selling language returns in Stage III and narrator comments appear at both the start and the end.

The full discussion is in `docs/interpretation.md`.

## Method

The work follows the seven steps of the Google Colab notebook in this repository.

1. **Partial reading.** Three blocks of about 20% of each third of the story (first block of Part 1, a random block of Part 2 with seed 42, last block of Part 3).
2. **Initial impression.** Concept, position, research problem and four dimensions.
3. **Text upload.** The story is loaded, cleaned of stray page numbers and headers, and split into paragraphs.
4. **Query generation.** The dimensions are turned into a prompt with definitions, seven rules and a JSON structure.
5. **Targeted extraction and formatting.** Claude (Anthropic), claude.ai chat, 31 October 2026. Every phrase must occur word for word in the story and under one sub-type only. No phrases were rejected.
6. **Computation and visualisation.** Whole-word, case-insensitive matching, longest phrase first, no stretch of text counted twice, stoplist `at present`. Results are given in hits per 100 words, checked with chi-square and Spearman tests, and drawn as four figures.
7. **Interpretation.** Counts, tests and figures are read together with the passages of the story.

## Repository structure

```
synthetic_reading_gift_of_the_magi/
├── index.html                  project webpage (GitHub Pages)
├── README.md                   this file
├── synthetic_reading_gift_of_the_magi.ipynb   Google Colab notebook (Steps 1 to 7)
├── initial_impression.md       impression, concept, position, research problem, dimensions
├── corpus/
│   └── gift_of_the_magi.txt    full text of the story
├── partial_reading/
│   └── partial_reading.txt     sampling method and marked phrases
├── prompt/
│   └── prompt.txt              prompt template with a {{PASSAGE}} placeholder
├── extraction/
│   ├── full_prompt.txt         complete prompt as sent to the model
│   ├── raw_llm_output.json     model, date, prompt file and merged output
│   ├── llm_output.json         extracted phrases as received
│   ├── verified_items.json     152 verified phrases by dimension and sub-type
│   ├── Theme_JSON.py           verified phrases as a Python dictionary
│   ├── matches.csv             193 matched occurrences
│   ├── segment_counts.json     the same 193 occurrences in JSON form
│   └── README.md               extraction record
└── docs/
    ├── interpretation.md       written interpretation
    ├── visualisations.html     four interactive figures
    └── report.html             full report
```

## Usage

The notebook `synthetic_reading_gift_of_the_magi.ipynb` was run in Google Colab. It builds the folders and files in this repository from the story and the model's reply, which is pasted into the notebook in Step 5. The interactive figures and the full report are standalone HTML files that load Plotly from a CDN, so they need an internet connection. To reproduce the counts from the matched occurrences:

```python
import pandas as pd

m = pd.read_csv("extraction/matches.csv")
print(len(m))                                   # 193 occurrences
print(m.groupby("dimension").size())            # hits per dimension
print(m.groupby(["stage", "dimension"]).size().unstack(fill_value=0))   # hits per stage
```

Divide the counts by the number of words in each stage (495, 584, 555 and 423) to obtain hits per 100 words.

## Limitations

- Counting depends on a phrase list, and words with several senses are counted alike.
- The extraction was done by one language model with one prompt, so another model or reader could choose different phrases.
- The 13 segments and four stages were decided by the researcher from changes of scene.
- The story is short, so short segments can show high densities from few hits.
- Counts show vocabulary, not tone, and the statistical tests are a rough guide only.

## Citation

Kumar, A. (2026). *Synthetic Reading of O. Henry's "The Gift of the Magi": How the Narrator's Language Turns Economic Loss into Emotional Value*. Department of Humanities and Social Sciences, IIT (ISM) Dhanbad.
