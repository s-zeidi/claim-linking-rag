# CLEF 2026 Task 1 — Source Retrieval for Scientific Web Claims

This pipeline was developed by our team as part of our participation in [CheckThat! Lab @ CLEF 2026, Task 1](https://checkthat.gitlab.io/clef2026/task1/). Task 1 focuses on retrieving the referenced scientific paper from a candidate pool given a multilingual social media post that implicitly mentions it, across English, German, and French.


**Approach:** Dense retrieval with Harrier → cross-encoder reranking with Jina Reranker v3 → evaluated with MRR@5.


---

## Structure

```
clef2026-task1/
├── pipeline.ipynb          # Main pipeline notebook
├── config/
│   └── default.yaml        # Hyperparameters and model settings
├── data/                   # Generated at runtime — gitignored
│   ├── embeddings/         # Document & query embeddings (.pt, .npy)
│   ├── candidates/         # Top-50 retrieval results per language (.json)
│   └── results/            # Reranked results + results.xlsx
├── requirements.txt
└── .gitignore
```

---

## Setup

```bash
pip install -r requirements.txt
```

The dataset is gated — accept the Declaration of Commitment on the
[HuggingFace page](https://huggingface.co/datasets/sschellhammer/CT26_Task1_SourceRetrievalForScientificWebClaims)
and log in before running:

```bash
huggingface-cli login
```

Then open `pipeline.ipynb` and run top to bottom. Each step checkpoints to `data/` so the notebook can be resumed after interruptions.

---

## Output

| Path | Contents |
|---|---|
| `data/embeddings/{tag}/collection/` | Document embeddings |
| `data/embeddings/{tag}/{lang}/` | Query embeddings per language |
| `data/candidates/{tag}/{lang}_dev.json` | Top-50 retrieval candidates |
| `data/results/{tag}/{lang}_dev_reranked.json` | Reranked results |
| `data/results/results.xlsx` | MRR@5 scores per experiment |


## Authors

Farnoush Zeidi, Farnaz Zeidi, Roman Christof, Renate Koenig, Liam Childs