# TCR Network Topology Analysis: Beyond Frequency

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![DOI](https://img.shields.io/badge/DOI-pending-lightgrey.svg)](https://zenodo.org)

## Overview

This repository contains code, data, and analysis pipelines for the manuscript:

**"Beyond Frequency: Network Topology Reveals Non-Neutral Evolution in Public T-Cell Receptor Repertoires"**

*Submitted to PNAS (December 2025)*

### Key Finding

Public TCR sequences form dense **structural families**—networks of similar but non-identical sequences—that cannot be explained by neutral recombination biases alone. Network topology succeeds where frequency analysis fails, providing a falsifiable test for convergent antigenic selection.

---

## Repository Structure

```
tcr-network-topology-2025/
├── README.md                  # This file
├── LICENSE                    # MIT License
├── requirements.txt           # Python dependencies
├── scripts/
│   ├── production_neutral_null.py         # Neutral model simulation
│   ├── tcr_similarity_network_analysis.py # Network construction & metrics
│   ├── batch_network_analysis.py          # Multi-pathogen pipeline
│   ├── tcr_publicness_classifier.py       # Predictive model (Module C)
│   └── positional_entropy_analysis.py     # ΔS calculation (Module A)
├── data/
│   ├── VDJdb_processed/           # Filtered TCR sequences
│   └── network_edgelists/         # Network adjacency lists
├── figures/
│   ├── network_metrics_*.png      # Clustering/degree/component plots
│   └── network_components_*.png   # Size distributions
└── docs/
    ├── ZENODO_SUBMISSION.md       # Data deposit protocol
    └── ANALYSIS_PROTOCOL.md       # Step-by-step reproduction
```

---

## Quick Start

### 1. Installation

```bash
git clone https://github.com/elkinnavarro-glitch/tcr-network-topology-2025.git
cd tcr-network-topology-2025
pip install -r requirements.txt
```

### 2. Download VDJdb Data

```bash
wget https://github.com/antigenomics/vdjdb-db/releases/download/2023-12-13/vdjdb-2023-12-13.zip
unzip vdjdb-2023-12-13.zip -d data/VDJdb_raw/
```

### 3. Run Full Analysis Pipeline

```bash
# Process VDJdb & build networks for all 4 pathogens
python scripts/batch_network_analysis.py --input data/VDJdb_raw/ --output results/

# Generate neutral null models (100 replicates)
python scripts/production_neutral_null.py --n_reps 100 --size 1000 --output results/null_models/

# Calculate positional entropy (ΔS)
python scripts/positional_entropy_analysis.py --families data/structural_families.csv --output results/entropy/

# Train predictive classifier
python scripts/tcr_publicness_classifier.py --features data/features.csv --output results/classifier/
```

### 4. Reproduce Figures

All main & supplementary figures can be regenerated:

```bash
python scripts/generate_figures.py --results results/ --output figures/
```

---

## Key Analyses

### Module A: Falsificationist Framework

**Hypothesis testing with explicit null models:**

- **H0_freq**: Neutral model produces 1–30% public clones
- **H0_topology**: Neutral model → clustering C < 0.0001
- **H0_rich**: P_gen + V/J + length conditioned → < 0.5 edges/1000 nodes

**Rejection criteria:** z > 3, p < 0.001, Cohen’s d > 1

```python
from scripts.production_neutral_null import NeutralModel

model = NeutralModel(n_clones=1000, conditioning=['Pgen', 'VJ', 'length'])
null_network = model.generate_network(threshold=1)

print(f"Empirical clustering: {empirical_C:.4f}")
print(f"Null clustering: {null_network.clustering:.4f}")  # Expected: 0.0000
print(f"z-score: {(empirical_C - null_network.clustering) / null_network.std:.2f}")  # Expected: >5
```

### Module B: Network Construction

**Similarity networks with Levenshtein distance ≤ 1:**

```python
from scripts.tcr_similarity_network_analysis import build_network

G = build_network(sequences=['CASSLGQAYEQYF', 'CASSLGQAYELYF'], threshold=1)
print(f"Nodes: {G.number_of_nodes()}, Edges: {G.number_of_edges()}")
print(f"Clustering: {nx.average_clustering(G):.4f}")
```

### Module C: Predictive Classifier

**Does network topology improve prediction of public clones?**

| Model | Features | AUC | ΔAUC |
|-------|----------|-----|------|
| Generative only | P_gen, V/J, length | 0.68 | — |
| + Network features | + clustering, degree, component | **0.91** | **+0.23** |

```python
from scripts.tcr_publicness_classifier import train_classifier

clf, metrics = train_classifier(features=['Pgen', 'clustering', 'degree'], target='is_public')
print(f"AUC: {metrics['auc']:.3f}")
```

### Module D: Falsifiable Prediction

**Post-vaccination networks should show:**

1. Δclustering > 0 within 2 Levenshtein steps of vaccine clones
2. New edges form at conserved motif positions (high prior ΔS)
3. Component size grows faster than neutral expansion

Proposed validation: SARS-CoV-2 vaccination cohorts (ImmuneCODE, AIRR-seq)

---

## Citation

If you use this code or data, please cite:

```bibtex
@article{navarro2025tcr,
  title={Beyond Frequency: Network Topology Reveals Non-Neutral Evolution in Public T-Cell Receptor Repertoires},
  author={Navarro, Elkin and Collaborators},
  journal={eLife},
  year={2025},
  note={Preprint available at bioRxiv}
}
```

---

## Data Availability

- **VDJdb**: Public database at https://vdjdb.cdr3.net/
- **Processed datasets**: Zenodo (DOI pending)
- **Network edgelists**: `data/network_edgelists/` (CSV format)
- **Neutral model outputs**: `results/null_models/` (100 replicates)

---

## Contact

**Elkin Navarro**  
Research Center for Life Sciences (CICV)  
Universidad Simón Bolívar, Barranquilla, Colombia  

Questions? Open an [issue](https://github.com/elkinnavarro-glitch/tcr-network-topology-2025/issues) or contact via email.

---

## License

MIT License - see [LICENSE](LICENSE) for details
