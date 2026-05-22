# Evoked-Potential Metric Equation Inventory

This repository contains a curated inventory of mathematical metric formulations reviewed in our manuscript on standardized metrics for clinical evoked potentials.

The dataset summarizes equations used across auditory and visual evoked-potential paradigms, including ABR, ASSR, VEP, and SSVEP. Metric families include signal-to-noise ratio, morphology, phase metrics, significance and difference tests, supplementary metrics, and reproducibility metrics.

## Search Keywords

The review search used one topic keyword and two inclusion-keyword blocks: evoked-potential modality terms and quantitative metric terms. Query-level exclusions reduced retrieval of BCI-speller, motor-imagery, and machine-learning-only records that did not report physiological EP metrics. Database-specific query strings are represented in `Included_Paper_V1.xlsx` under the `search_query` field.

### Topic Keyword

- `"quantitative metrics for clinical evoked potentials"`

### Inclusion Keywords

**Evoked-potential modality terms**

- `"ABR"`
- `"ASSR"`
- `"VEP"`
- `"SSVEP"`
- `"cABR"`
- `"auditory brainstem response"`
- `"auditory brain-stem response"`
- `"brainstem auditory evoked response"`
- `"brainstem auditory evoked potential"`
- `"complex auditory brainstem response"`
- `"auditory steady-state response"`
- `"auditory steady state response"`
- `"auditory steady-state evoked potential"`
- `"visual evoked potential"`
- `"visual-evoked potential"`
- `"steady-state visual evoked potential"`
- `"steady-state evoked potential"`

**Metric and analysis terms**

- `"SNR"`
- `"signal-to-noise ratio"`
- `"signal to noise ratio"`
- `"signal-to-noise-ratio"`
- `"noise"`
- `"background noise"`
- `"residual background noise"`
- `"spectral power"`
- `"power spectral density"`
- `"PSD"`
- `"Fourier"`
- `"phase locking value"`
- `"PLV"`
- `"phase-sensitiv*"`
- `"frequency detection"`
- `"harmonic frequenc*"`
- `"statistical significan*"`
- `"t-test"`
- `"F-test"`
- `"ANOVA"`
- `"canonical correlation analysis"`
- `"CCA"`
- `"threshold detection"`
- `"suprathreshold"`
- `"stop averaging sweeps"`
- `"objective detection"`
- `"response detector"`
- `"mutual information"`
- `"Bayesian Inference"`
- `"adaptive strategy"`
- `"weight*"`
- `"quantitative measur*"`
- `"quantitative statistic*"`
- `"mathematical analysis*"`
- `"statistical analysis"`
- `"statistical detector"`
- `"objective quantitativ*"`
- `"objective"`
- `"automatic"`
- `"statistic"`

### Exclusion Keywords

- `"BCI speller*"`
- `"brain-computer interface speller*"`
- `"motor imagery"`
- `"machine-learning-only studies without physiological metric reporting"`

## API Sources

Paper records in `Included_Paper_V1.xlsx` were ingested from the following API/source labels before deduplication and relevance screening. Human reviewer 1 performed abstract screening. Human reviewer 2 cross-verified this stage by checking a sample of the papers accepted and rejected by Human reviewer 1. Human reviewers 3 and 4 then performed full-paper screening. The table reports the abstract-screening counts from `Reviewer 1: decision` and the full-paper screening status from `Reviewer 2: decision` in the Excel file.

Note: in the Excel file, `Reviewer 1` refers to the abstract-screening stage by Human reviewers 1 and 2, whereas `Reviewer 2` refers to the full-paper screening stage by Human reviewers 3 and 4.

| API/source label | Records | Abstract screening (Human reviewers 1 and 2) | Full-paper screening (Human reviewers 3 and 4) |
|---|---:|---|---|
| `pubmed` | 814 | accepted: 144; rejected: 105; pending: 565 | agreed: 17; disagreed: 116; unsure: 12; pending: 669 |
| `scopus` | 362 | accepted: 81; rejected: 45; pending: 236 | agreed: 17; disagreed: 60; unsure: 4; pending: 281 |
| `crossref` | 287 | accepted: 47; rejected: 43; pending: 197 | agreed: 4; disagreed: 36; unsure: 7; pending: 240 |
| `openalex` | 274 | accepted: 43; rejected: 33; pending: 198 | agreed: 11; disagreed: 31; unsure: 1; pending: 231 |
| `springer_openaccess` | 143 | accepted: 25; rejected: 11; pending: 107 | agreed: 4; disagreed: 21; unsure: 0; pending: 118 |
| `core` | 113 | accepted: 11; rejected: 17; pending: 85 | agreed: 0; disagreed: 11; unsure: 0; pending: 102 |
| `springer` | 35 | accepted: 4; rejected: 5; pending: 26 | agreed: 1; disagreed: 3; unsure: 0; pending: 31 |
| `iop` | 4 | accepted: 1; rejected: 0; pending: 3 | agreed: 0; disagreed: 0; unsure: 1; pending: 3 |
| **Total** | **2032** | **accepted: 356; rejected: 259; pending: 1417** | **agreed: 54; disagreed: 278; unsure: 25; pending: 1675** |

## Gemini Relevance Scoring

Gemini was used as a relevance-screening aid during paper ingestion:

- **Inputs sent to Gemini**
  - Paper-specific fields: title and abstract.
  - Review-level context: **Topic Keyword**, **Inclusion Keywords**, and **Exclusion Keywords**.
  - The keyword sections were used to keep the scoring anchored to clinical evoked-potential metric relevance rather than general EEG, BCI, or machine-learning relevance.

- **Model and prompt settings**
  - Model: `gemini-2.5-flash`.
  - Temperature: `1.0`.
  - The structured prompt requested:
    - a relevance score from `0` to `100`;
    - a `3` to `5` bullet summary of why the paper may be relevant;
    - a brief rationale explaining the score.

- **When scoring was applied**
  - Automatically after scraping and deduplication.
  - Re-run when papers were first added, when metadata changed, or when papers were explicitly refreshed in a job.

- **Topic-guard validation**
  - A secondary validation layer checked whether the title and abstract overlapped with the **Topic Keyword** and **Inclusion Keywords**.
  - Scores were capped at `35` when no topic-token overlap was detected.
  - Scores were capped at `60` when only weak topic-token overlap was detected.
  - This guard was used to prevent high Gemini scores for papers that appeared methodologically relevant but were off-topic for clinical EP metric review.

## Contents

- `Included_Paper_V1.xlsx`  
  Paper-screening workbook with search-query metadata and relevance-screening fields.

- `metrics.xlsx`  
  Excel version of the equation inventory.

- `equations.csv`  
  CSV version for programmatic use.

- `metrics_open_access_check.csv`  
  Open-access metadata for cited source papers, where available.

## Included Fields

The inventory includes:

- metric family
- equation label
- citation key
- source title
- DOI or URL
- equation in Excel-friendly text format
- original LaTeX equation transcription
- verification status
- review notes
- open-access status where available
