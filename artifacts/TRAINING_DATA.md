# Training Data Disclosure — AMP Challenge 2027

## 1. Primary Training Dataset
- **Source**: `data/antibacterial.fasta` (provided by AMP Challenge organizing committee).
- **Sequence Count**: 39,448 experimentally verified antimicrobial peptides.
- **Alphabet**: 20 canonical proteinogenic amino acids (ACDEFGHIKLMNPQRSTVWY).
- **Length Distribution**: 8 to 50 residues (median: 18 residues).

## 2. Data Splits
- **Training Set**: 37,476 sequences (95%).
- **Validation Set**: 1,972 sequences (5%) partitioned with fixed seed 42.
- **Negative Decoys**: None used in language model adaptation (unsupervised likelihood density estimation).

## 3. Data Licensing & Compliance
- In accordance with competition rules, all training sequences derive from publicly available reference databases (DBAASP, APD, DRAMP, dbAMP, UniProt).
- No proprietary or non-disclosed private data was used in the training of AmphiProt-LM.