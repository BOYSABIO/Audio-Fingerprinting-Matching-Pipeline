## Notebook Breakdown

This repository contains both conceptual notebooks and the final practical execution path.

## Recommended Flow (Final Project Path)

### `AUDIO_PROCESSING.ipynb` (Local preprocessing)
- Downloads songs and creates short clips.
- Extracts/flattens fingerprints for both songs and clips.
- Exports consolidated fingerprint CSVs used as inputs for Databricks hashing/matching.

### `03_Hashing_Fingerprints.ipynb` (Databricks)
- Loads flattened fingerprints from Silver-layer inputs.
- Applies SHA256 hashing (`concat_ws` + `sha2`) to produce stable fingerprint signatures.
- Writes hashed song fingerprints to Gold-layer storage.

### `04_ZASHAM_APP.ipynb` (Databricks matching)
- Loads clip fingerprints and hashes with the same logic as songs.
- Joins clip hashes against Gold song hashes.
- Aggregates matches per song and computes confidence:
  `(matched_hashes / total_clip_hashes) * 100`.
- Ranks likely songs and reports top predictions.

---

## Concept / Demonstration Notebooks

### `01_Audio_Downloader.ipynb`
- Demonstrates ingestion approach in a Databricks notebook context.
- Not part of the final practical execution path due environment limitations with audio tooling.

### `02_Fingerprint_Extraction.ipynb`
- Demonstrates how fingerprint extraction would run in the Databricks workflow.
- Final project uses local extraction in `AUDIO_PROCESSING.ipynb` for reliability.

---