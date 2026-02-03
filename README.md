# Human Benchmark Version v3

Parallel sentence benchmarks for the following language pairs:

- English–Hindi
- English–Telugu
- Hindi–Telugu (derived via shared English)

This repository includes multiple domains, reference translations, and
balanced splits for development and evaluation.

## Authors

- Vandan Mujadia
- Dipti Misra Sharma

## Acknowledgment

Developed as part of Himangy, LTRC IIIT H.

## Source Data Layout

Raw data is organized by language pair and domain:

- `English-Hindi/`
  - `wiki-articles/`
  - `wiki-news/`
  - `news-on-air/`
- `English-Telugu/online/`
  - `wiki-articles/`
  - `wiki-news/`
  - `news-on-air/`

Each raw `.txt` file is tab-separated. The first three columns are:

1. Task or passage id (varies by file)
2. Source sentence (English)
3. Target sentence (Hindi or Telugu)

## Processed Outputs

All generated files are stored under `outputs/`.

### 1) Flat Parallel Pairs

Source–target TSVs (one sentence pair per line):

- `outputs/english-hindi.tsv`
- `outputs/english-telugu.tsv`
- `outputs/hindi-telugu.tsv`

For Hindi–Telugu, pairs are created by matching shared English sentences
across the English–Hindi and English–Telugu datasets.

### 2) Grouped References (per source)

One row per source sentence, followed by all references:

- `outputs/english-hindi.references.tsv`
- `outputs/english-telugu.references.tsv`
- `outputs/hindi-telugu.references.tsv`

Format:

```
source<TAB>reference1<TAB>reference2<TAB>reference3...
```

### 3) Domain-Specific Splits with References

Split files are created per language pair, per domain, and per reference
(ref1, ref2, ref3). Each split has an equal number of examples.

Location:

```
outputs/splits/
```

Filename pattern:

```
{pair}.{domain}.ref{1|2|3}.{dev|devtest|test}.tsv
```

Example:

```
english-hindi.wiki-news.ref1.dev.tsv
```

### 4) Grouped by Language and Reference

Domain-concatenated files grouped by language pair and reference:

```
outputs/grouped/{pair}/ref{1|2|3}/{dev|devtest|test}.tsv
```

Example:

```
outputs/grouped/english-hindi/ref1/dev.tsv
```

## Splitting Policy

For each language pair and domain, sources are shuffled and split into
`dev`, `devtest`, and `test` with equal sizes. Any remainder that would
make the splits uneven is dropped.

## Notes

- All files are UTF-8.
- Tabs are used as field separators.
- If a source has fewer than 3 references, ref2/ref3 may be empty.
