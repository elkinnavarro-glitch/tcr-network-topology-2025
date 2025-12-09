# Data Directory

## Contents

Processed datasets for TCR Network Topology Analysis. All datasets derived from VDJdb (https://vdjdb.cdr3.net/) and processed through the pipelines in `src/`.

### Dataset Files

#### Pathogen-Specific Networks

- **network_EBV_edgelist.csv** - Network edges for EBV-specific TCR repertoire (Levenshtein distance ≤ 1)
  - Columns: source_cdr3, target_cdr3, weight, similarity_type
  - Nodes: ~2,847 unique CDR3 sequences
  - Edges: ~8,934 connections

- **network_CMV_edgelist.csv** - Cytomegalovirus TCR network
  - Nodes: ~1,205 unique CDR3 sequences
  - Edges: ~3,421 connections

- **network_SARSCOV2_edgelist.csv** - SARS-CoV-2 pandemic TCR network
  - Nodes: ~4,156 unique CDR3 sequences
  - Edges: ~12,089 connections

- **network_INFLUENZA_edgelist.csv** - Seasonal influenza TCR network
  - Nodes: ~892 unique CDR3 sequences
  - Edges: ~1,876 connections

#### Statistical Summaries

- **network_analysis_summary.csv** - Aggregate statistics across all pathogen networks
  - Fields: pathogen, n_nodes, n_edges, density, clustering_coeff, avg_degree, component_count, largest_component_size

- **powerlaw_distribution_analysis.csv** - Degree distribution model selection results
  - Fields: pathogen, degree_value, count, power_law_p, lognormal_p, selected_model, alpha_exponent

#### Null Model Comparisons

- **null_models_statistics.csv** - Configuration model null statistics (100 replicates)
  - Fields: pathogen, replicate_id, null_clustering, null_avg_degree, null_density, z_score_clustering, p_value

- **hla_exclusion_robustness.csv** - Leave-one-HLA-out stability analysis
  - Fields: hla_allele, excluded_sequences, network_size_after_exclusion, clustering_change, stability_metric

#### Processed VDJdb Input

- **vdjdb_processed_complete.csv** - Full processed VDJdb dataset
  - Columns: cdr3, v_gene, j_gene, hla_allele, pathogen, frequency, is_public, sequence_length
  - Rows: ~15,000+ unique TCR sequences across all pathogens

### Data Generation

All CSV files are generated reproducibly via:

```bash
python src/01_build_networks.py --input /path/to/vdjdb_raw/ --output data/
python src/02_null_models.py --n_reps 100 --output data/
python src/03_power_law_analysis.py --input data/network_*.csv --output data/
```

### Citation

If using these processed datasets, please cite:

1. **Original VDJdb**: Shugay M, et al. (2018). VDJdb: a curated database of T-cell receptor sequences with known antigen specificity. *Nucleic Acids Research*, 46(D1), D419-D427.

2. **This analysis**: See main README.md for citation details.

### License

All processed data are provided under MIT License. Original VDJdb data retain their respective licenses.
