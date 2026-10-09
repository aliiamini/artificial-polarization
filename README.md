# Artificial polarization in silicon samples

Replication materials for:

> Amini, A. *Large language models promote artificial polarization by underpredicting middle survey responses.* Under review.

Persona-prompted large language models (LLMs) are used to build "silicon samples" of survey respondents. This project compares their predicted answers with the real answers of about 17,400 respondents in three surveys (ANES 2024, CES 2024, WVS Wave 7) and finds that the models give the middle answer category 14 to 23 percentage points less weight than people do.

**Status.** The full code, prompts, and model outputs will be posted here and archived on Zenodo when the paper is published. This repository currently holds part of the pipeline.

## What is in the study

| Step | What it does | Where |
|---|---|---|
| Personas and prompts | Builds one prompt per respondent from their survey profile | `src/prompt_utils.py`, `src/codebooks.py` |
| API runs | GPT-4.1-mini, Gemma-3-27B, Llama-3.1-70B, Mistral-Small-3.2-24B at temperature 0 | `scripts/` |
| Local runs | Original open-weight models run with vLLM on NVIDIA H100 GPUs; full probability over every answer option for every ANES respondent (145,713 distributions) | `hpc/` |
| Analysis | Midpoint gap, bootstrap intervals, total variation distance, ranked probability score, accuracy baselines, binary collapse | `scripts/` |
| Paper outputs | Tables and figures in the paper and Supplementary Information | `tables/`, `figures/` |

## Paper element to script

| Paper | Script |
|---|---|
| Table 1 (accuracy, baselines, excess inflation) | `scripts/31_table1_baselines.py` |
| Table 2, Fig. 2 (full answer distributions) | `scripts/21_compare_local_distributions.py`, `scripts/23_fig_fulldist.py` |
| Fig. 3 (27 items with intervals) | `scripts/32_fig_gap_intervals.py` |
| Supplementary Tables S7, S8 | `scripts/22_appendix_tables.py` |
| Supplementary Table S12 (7-point items) | `scripts/26_sevenpoint_table.py` |
| Supplementary Information 12 (prompts) | `scripts/25_export_prompts.py` |

## Data

Survey data are not redistributed here. Download them from the original sources:

- ANES 2024 Time Series: https://electionstudies.org/data-center/2024-time-series-study/
- CES 2024: https://dataverse.harvard.edu/dataverse/cces
- WVS Wave 7: https://doi.org/10.14281/18241.24

Place the files in `data/raw/` as described in `data/README.md`.

## Running it

```bash
pip install -r requirements.txt
cp .env.example .env    # add your own API keys; never commit .env
```

Local runs need a GPU cluster (about 250 GB of model weights, about three days on NVIDIA H100 GPUs). See `hpc/README.md`.

## Citation

See `CITATION.cff`.

## License

Code: MIT. Model outputs: CC BY 4.0.
