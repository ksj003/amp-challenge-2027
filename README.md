# AmphiProt-LM: Generative AI for De Novo Antimicrobial Peptide Design

[![License: BSD 3-Clause](https://img.shields.io/badge/License-BSD_3--Clause-blue.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://github.com/astral-sh/uv)

Official submission repository for the **AMP Challenge 2027** (NeurIPS 2026 Competition Track) by Team AmphiProt.

## Abstract
Antimicrobial resistance requires therapeutic molecules that selectively disrupt bacterial bilayers while maintaining synthetic accessibility, low host toxicity, and sequence novelty. **AmphiProt-LM** combines transfer learning on an autoregressive 512M-parameter protein language model (ProtGPT2), biophysically guided sequence curation, and multi-objective evolutionary foundation scoring.

ProtGPT2 is adapted via Low-Rank Adaptation (LoRA, r=8, alpha=16) on 37,476 curated antibacterial peptides. From a raw pool of 500,000 sampled sequences, we enforce strict biophysical synthesizability constraints (100% cysteine exclusion, complexity filtering via Shannon entropy >= 2.0, and tandem-repeat elimination) alongside zero exact reference overlap to compile a 50,000-member candidate library. On the official seqme benchmark, our library achieves a Fréchet Biological Distance (FBD) of 1.41 against natural AMPs and a Conformity Score of 0.469.

Top candidates are ranked using a composite oracle integrating:
1. Eisenberg alpha-Helical Hydrophobic Moment at 100 deg periodicity.
2. ESM-2 Bidirectional Pseudo-Perplexity (facebook/esm2_t6_8M_UR50D).
3. Fine-Tuned Generative Likelihood.
4. Cationic Charge Density Optimization (+2 to +7).

All top 100 candidates satisfy strict novelty (<0.80 Levenshtein ratio vs reference) and pairwise diversity (<0.70).

## Reproduction & Verification

To reproduce the submitted library and ranked candidates deterministically:

\\\ash
# 1. Clone repository
git clone https://github.com/ksj003/amp-challenge-2027.git
cd amp-challenge-2027

# 2. Sync dependencies
uv sync

# 3. Generate outputs
uv run generate --n-sequences 50000 --top-k 100 --seed 42
\\\

## Computational Evaluation (seqme)

| Metric | AmphiProt-LM (Ours) | Natural AMPs (Ref) | Baseline Target |
| :--- | :--- | :--- | :--- |
| **FBD** (ESM-2 Embeddings) | **1.41** | 0.00 | < 2.0 |
| **Property Conformity** | **0.469** | 0.503 | >= 0.40 |
| **Sequence Diversity (k=5)** | **0.891** | 0.854 | 0.80 - 0.86 |
| **Mean Net Charge** | **+2.16** | +2.90 | Cationic (+2 to +7) |
| **Uniqueness / Novelty** | **1.00 / 1.00** | 1.00 / 0.00 | 1.00 / 1.00 |

## License
BSD 3-Clause License — see [LICENSE](LICENSE) for details.
