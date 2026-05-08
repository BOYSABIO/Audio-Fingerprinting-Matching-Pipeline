# Audio Fingerprinting and Matching Pipeline

Shazam-style audio matching pipeline built for a Modern Data Architectures final project.  
Final workflow: local audio preprocessing + Databricks/Spark hashing and matching.

## Key Results

- Built an end-to-end Lakehouse pipeline (Bronze -> Silver -> Gold) for audio matching.
- Implemented reproducible fingerprint hashing + confidence scoring for clip-to-song prediction.
- Delivered a production-ready Databricks path after iterating from a legacy VM prototype.

## Demo

### Audio Processing (Local)
Downloads songs, creates clips, and prepares fingerprint datasets.

![Audio processing demo](docs/media/gifs/audio_processing_demo.gif)

### Zasham Matching App (Databricks Notebook Flow)
Hashes clip fingerprints and matches them against song signatures.

![Zasham app demo](docs/media/gifs/zasham_app_demo.gif)

## Pipeline at a Glance

1. **Local preprocessing** (`AUDIO_PROCESSING.ipynb`)
   - Download songs, generate short clips, extract flattened fingerprints.
2. **Databricks hashing** (`03_Hashing_Fingerprints.ipynb`)
   - Compute SHA256 fingerprint hashes and store in Gold.
3. **Databricks matching** (`04_ZASHAM_APP.ipynb`)
   - Hash clip fingerprints, join with Gold hashes, rank by confidence.

## Notebook Flow

- `AUDIO_PROCESSING.ipynb` - local preprocessing used in the final workflow.
- `03_Hashing_Fingerprints.ipynb` - Databricks hash generation.
- `04_ZASHAM_APP.ipynb` - Databricks matching and confidence scoring.
- `01_Audio_Downloader.ipynb` - concept notebook.
- `02_Fingerprint_Extraction.ipynb` - concept notebook.

## Tech Stack

- **Data processing:** Apache Spark, Databricks
- **Audio/signal processing:** `librosa`, `ffmpeg`, `yt-dlp`
- **Storage pattern:** Lakehouse layers (Bronze / Silver / Gold)
- **Matching method:** Fingerprint pair hashing + hash joins + confidence scoring

## Repository Layout

- `README.md` - project overview and demos
- `docs/architecture.md` - architecture summary
- `docs/notebook_breakdown.md` - notebook responsibilities
- `docs/setup_guide.md` - setup and run path
- `docs/media/videos/` - source demo videos
- `docs/media/gifs/` - GIFs used in README
- `VM_VERSION_archive/` - historical/legacy approach

## Documentation

- [Setup Guide](docs/setup_guide.md)
- [Pipeline Architecture](docs/architecture.md)
- [Notebook Breakdown](docs/notebook_breakdown.md)
- [Slide Deck](docs/MDA_Group8_Project.pdf)
- [Individual Report](docs/Individual%20Submission%20Report%20-%20Spencer%20Wood.pdf)
- [GitHub Setup Guide](docs/github_setup_guide.md)

## Legacy Notes

`VM_VERSION_archive/` contains older experimentation with VM-based Apache tooling (`NiFi`, local Hadoop services, etc.).  
It is preserved for context and is not part of the recommended final workflow.
