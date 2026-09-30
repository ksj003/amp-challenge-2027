# Selection and Ranking Documentation — AMP Challenge 2027

## 1. Candidate Generation
Candidates were sampled from AmphiProt-LM, a fine-tuned ProtGPT2 (512M) autoregressive language model
adapted via Low-Rank Adaptation (LoRA, r=8, alpha=16) on 37,476 curated antibacterial peptides.

## 2. Biophysical Pre-filtering
From the 50,000-member library, candidates were pre-filtered for pore-forming suitability:
- **Length Constraint**: 14 to 32 residues (optimal transmembrane bilayer-spanning dimension).
- **Cationic Charge**: Net charge between +2 and +7 to ensure bacterial selectivity without mammalian hemolysis.
- **Synthesizability**: Elimination of unconstrained cysteines (no terminal modifications/disulfides).
- **Sequence Complexity**: Shannon entropy >= 2.70 and rejection of all tandem repeats to prevent periodic loop collapse.

## 3. Foundation Model Scoring & Amphipathicity Optimization
Candidates were scored using a multi-objective composite function:
1. **Alpha-Helical Hydrophobic Moment (uH)**: Eisenberg hydrophobic moment at 100 deg periodicity to maximize amphipathic segregation.
2. **ESM-2 Bidirectional Pseudo-Perplexity**: Evaluated under facebook/esm2_t6_8M_UR50D for global evolutionary plausibility.
3. **ProtGPT2 Autoregressive Likelihood**: Domain-specific generative antimicrobial likelihood.
4. **Charge Density Optimization**: Balanced cationic density for selective bacterial lipid interaction.

## 4. Novelty & Diversity Guarantee
- **Strictest Novelty**: Levenshtein ratio < 0.80 against all reference sequences in data/antibacterial.fasta.
- **Greedy Diversity Clustering**: Maximum pairwise Levenshtein ratio < 0.70 among selected candidates.
- Total top candidates: 100 unique, novel, diverse, and synthesizable peptides.