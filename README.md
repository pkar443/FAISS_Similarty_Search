# FAISS Similarity Search Tutorial

This tutorial shows how to compare vectors with cosine similarity and how to search them efficiently with FAISS. In simple terms, cosine similarity checks whether two vectors point in nearly the same direction, while FAISS builds search indexes that let you retrieve the closest vectors much faster than a manual scan when the dataset becomes large.

## Current State

The main script is [faiss.py](/mnt/h/prakash/Publication/Guest Lecture/Siamese NN/FAISS_Tutorial/faiss.py). It generates sample vectors, compares brute-force cosine search against `IndexFlatL2`, then demonstrates `IndexIVFFlat` with clustered regions and timing comparisons.

## What The Script Covers

- Cosine similarity for exact directional comparison between vectors.
- `IndexFlatL2` for exact nearest-neighbor search in FAISS.
- `IndexIVFFlat` for approximate search by clustering vectors into regions first.
- Visualizations for vectors, matches, and searched IVF regions.
- Timing comparisons across different dataset sizes.

## Setup

This repository is currently on a mounted drive under `/mnt/h/...`, so a project-local `.venv` could not be created reliably from this machine. The working virtual environment was created here instead:

```bash
/home/pkar443/.venvs/faiss_similarity_search
```

Activate that environment:

```bash
source /home/pkar443/.venvs/faiss_similarity_search/bin/activate
```

Install the required packages:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

If you later move the project to a native Linux filesystem, you can create a local environment with:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Requirements File

To install everything from the requirements file:

```bash
pip install -r requirements.txt
```

## Run

After activating the virtual environment, run:

```bash
python faiss.py
```

If you are running without a desktop display, use:

```bash
MPLBACKEND=Agg python faiss.py
```

## Search Modes Summary

- Brute-force cosine search checks every vector directly and is easiest to understand on small datasets.
- `IndexFlatL2` still checks all vectors, but uses FAISS for efficient exact search.
- `IndexIVFFlat` first groups vectors into regions, then searches only the most relevant regions, which is usually faster on larger datasets but may miss some exact matches depending on `nprobe`.

## Included Dependencies

- `faiss-cpu`
- `numpy`
- `matplotlib`
- `scikit-learn`
