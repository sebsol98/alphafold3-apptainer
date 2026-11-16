# AlphaFold 3: Apptainer container for HPC

This repository contains only the **recipe** to automatically build, with GitHub Actions,
an Apptainer image (`.sif`) of [AlphaFold 3](https://github.com/google-deepmind/alphafold3)
for use on a SLURM-based HPC cluster. The AlphaFold 3 source code is not stored here: the
workflow fetches it at every build from the official Google DeepMind repository and uses
their Dockerfile unmodified.

## What is (and is not) inside the container

| | Where it lives |
|---|---|
| Software (AlphaFold 3, HMMER, Python, JAX, CUDA libraries) | **inside the `.sif`** |
| Model parameters (`af3.bin`) | **not included**: granted by Google DeepMind to each individual user, kept in the user's home directory on the cluster |
| Genetic databases (~630 GB) | **not included**: stored in a shared directory on the cluster |

## How to build

1. Go to **Actions** → **Build AlphaFold 3 (Apptainer .sif)** → **Run workflow**
2. Enter the AlphaFold 3 release (e.g. `v3.0.5`) and start the run
3. After about 30–60 minutes the job page shows a summary with the release, the source
   commit, the SHA-256 checksum and the exact command to use on the cluster

## How to download it on the cluster

```bash
apptainer pull alphafold3_v3.0.5.sif oras://ghcr.io/<owner>/alphafold3-sif:v3.0.5
sha256sum alphafold3_v3.0.5.sif   # compare with the checksum in the build summary
```

## Licences

- AlphaFold 3 source code: Apache 2.0 (since release v3.0.3)
- AlphaFold 3 model parameters: subject to the
  [Google DeepMind terms of use](https://github.com/google-deepmind/alphafold3/blob/main/WEIGHTS_TERMS_OF_USE.md),
  non-commercial use only and not redistributable, which is why they are **not** part of
  this container
