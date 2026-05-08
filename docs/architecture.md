## Pipeline Architecture

This project follows a lakehouse-style flow where raw audio becomes searchable fingerprint hashes.

| Layer | Purpose | Typical Contents |
|---|---|---|
| **Bronze** | Raw ingestion output | Downloaded song/clip audio files and ingestion metadata |
| **Silver** | Feature engineering | Flattened fingerprint pairs (`freq1`, `freq2`, `delta_time`, `anchor_time`) |
| **Gold** | Fast lookup index | SHA256 fingerprint hashes keyed for matching |
| **Staging** | Query-time comparison | Hashed fingerprints from uploaded/selected clips |

## Final Execution Path

1. Run local preprocessing in `AUDIO_PROCESSING.ipynb` to generate flattened fingerprints.
2. Upload song and clip fingerprint CSV outputs to DBFS Silver paths.
3. Run `03_Hashing_Fingerprints.ipynb` to build Gold fingerprint hashes.
4. Run `04_ZASHAM_APP.ipynb` to hash clips, match on hashes, and compute confidence scores.

## Legacy Context

Earlier VM-based experiments (NiFi + local Hadoop services) are preserved in `VM_VERSION_archive/` for historical reference only.  
They are not required for the current recommended Databricks workflow.