# Data and Code for: Nanoconfinement of Hydrophobic Domains Facilitates Strong Mesoscale Networks in Silk-Inspired Materials

This repository contains processed data and plotting notebooks
used to generate figures for the manuscript:

"Nanoconfinement of Hydrophobic Domains Facilitates Strong Mesoscale Networks in Silk-Inspired Materials"

Gwen Liu, Jacob Graham, Sinan Keten  
Nano Letters, 2026

**Dataset DOI:** 10.5281/zenodo.18461972


**Version:** 1.0  
**Release Date:** February 2026

## Citation

If you use this dataset, please cite:

```
Liu, G., Graham, J., & Keten, S. (2026). 
Nanoconfinement of Hydrophobic Domains Facilitates Strong Mesoscale Networks in Silk-Inspired Materials. 
Nano Letters. [DOI to be added upon publication]

Dataset: 10.5281/zenodo.18461972
```

## Contact

**Gwen Liu**  
Email: gwenliu2024@u.northwestern.edu  
Department of Mechanical Engineering, Northwestern University

For questions about this dataset or the associated research, please contact the corresponding author.

## Acknowledgments

This work was supported by the National Science Foundation (award number OIA-2219149)
and the Ryan Fellowship organized through the International Institute for Nanotechnology
at Northwestern University.

Computational resources were provided by the Quest high-performance computing facility at Northwestern University, which is jointly supported by the Office of the Provost, the Office for Research, and Northwestern University Information Technology.

## Contents

### Data Files (`data/`)

Processed tabular data derived from molecular dynamics simulations.

#### Network and Mechanical Data
- **`large_system_diff_pull_force_frames13_41_51.pkl`** (681 MB) - Network metrics and graph structures for systems with 111 pN processing force across multiple simulation frames (13, 41, 51) corresponding to post-equilibration, post-processing, and pre-tensile states.
- **`large_system_frames13_41_51.pkl`** (4.1 MB) - Network data for systems with 222 pN processing force at frames 13, 41, and 51 corresponding to post-equilibration, post-processing, and pre-tensile states.

#### Degree and Shape Metrics
- **`deg_shape_metric_pull_force_111.csv`** - Degree and shape metrics for systems with 111 pN processing force (final selected force)
- **`deg_shape_metric_pull_force_222.csv`** - Degree and shape metrics for systems with 222 pN processing force (alternate test force)

#### Network Summaries
- **`md_dbscan_network_summary_long_pretensile.csv`** (421 KB) - Long-format summary of DBSCAN clustering network metrics for pretensile simulations
- **`md_dbscan_network_corr_vs_toughness_pretensile.csv`** (89 KB) - Correlation data between network metrics and toughness for pretensile conditions
- **`dbscan_network_sensitivity_summary.csv`** - Summary of network sensitivity to DBSCAN clustering parameters

#### Tables
- **`table_S2_robust_local_network_metrics.csv`** - Robust local network metrics (supplementary table)

#### Simulation Subdirectories
- **`simulations_large/`** - Systems with 222 pN processing force. Contains stress-strain data (`stress_strain_5seeds.pkl`) and subdirectories for 5 test runs across 8 different A-B parameter combinations (A∈{1,2,4,6,8,12,24,48}, B=2A)
- **`simulations_large_diff_pull_force/`** - Systems with 111 pN processing force (final selected force). Same structure as `simulations_large/`

### Plotting Notebooks

#### Main Figures

**`Figure_2_mechanical_properties.ipynb`**  
Generates bar charts showing mechanical properties (toughness, max stress, max strain) across different nanoconfinement factors (α values). Uses data from systems with 111 pN processing force.

**`Figure_3_network_correlations.ipynb`**  
Analyzes correlations between network topology metrics and mechanical properties (toughness/strength). Plots scatter plots with error bars showing relationships between metrics like cluster size, degree centrality, clustering coefficient, and mechanical outcomes.

**`Figure_4_degree_distributions.ipynb`**  
Visualizes degree distributions of network nodes across different α values with lognormal fits. Shows how network connectivity patterns change with nanoconfinement.

**`Figure_5_and_SI_9_entropy.ipynb`**  
Plots entropy-based metrics alongside toughness to show correlations. Creates dual-axis plots comparing shape/degree entropy with mechanical toughness across α values for both pull force configurations.

#### Supplementary Information Figures

**`SI_1_stress_strain.ipynb`**  
Generates stress-strain curves and mechanical property bar charts for the standard simulation set (at higher pulling processing force of 222 pN).

**`S2_clustering_sensitivity.ipynb`**  
Analyzes sensitivity of network metrics to DBSCAN clustering parameters (eps and min_samples). Creates heatmaps showing how cluster count, average cluster size, and edge count vary with clustering parameters.

**`S3_S4_network_metric_sensitivity.ipynb`**  
Creates comprehensive heatmaps showing how various network metrics respond to different DBSCAN parameters. Includes correlation heatmaps and metric value heatmaps for 12+ network properties.

**`S5_S6_correlations.ipynb`**  
Generates correlation matrices between network metrics and mechanical properties. Uses both Pearson and Spearman correlation methods to identify robust relationships.

## Requirements

### Python Version
- Python ≥ 3.10

### Required Packages
```
numpy>=2.2.0
pandas>=2.2.0
matplotlib>=3.8.0
scipy>=1.11.0
networkx>=3.0
seaborn>=0.12.0
```

### Installation
Install all required packages using pip:
```bash
pip install numpy pandas matplotlib scipy networkx seaborn
```

### Tested Environment
- Python 3.13.2 (conda-forge, Linux)
- numpy 2.2.3
- pandas 2.2.3
- matplotlib 3.10.0
- scipy 1.15.2

## Usage

Open any of the Jupyter notebooks in the top-level directory and run all cells:
```bash
jupyter notebook
```

All figures will be generated from the files in the `data/` directory.

## Pickle File Format Details

The `.pkl` files in this dataset are Python pickle files (protocol version 4.0) containing pandas DataFrames and NetworkX graph objects.

### Data Structures

**Large network files** (`large_system_*.pkl`):
- Contains nested dictionaries with keys corresponding to simulation parameters (A, B values)
- Each entry contains pandas DataFrames with columns including:
  - `test_num`: Simulation trial number (1-5)
  - `frame`: Simulation frame number
  - `G`: NetworkX graph object representing the network topology
  - Network metrics: `num_clusters`, `avg_cluster_size`, `number of edges`, `avg_degree_centrality`, `weighted_clustering`, etc.

**Stress-strain files** (`stress_strain_5seeds.pkl`):
- Pandas DataFrame with mechanical property data
- Columns: `A`, `B`, `test_num`, `Toughness`, `Max_Stress`, `Max_Strain`
- Rows correspond to different simulation trials and parameter combinations

### Loading Pickle Files

**Requirements:**
- Python ≥ 3.10
- pandas ≥ 2.2.0
- networkx ≥ 3.0 (for files containing graph objects)

**Example code:**
```python
import pickle
import pandas as pd

# Load network data with graph objects
with open('data/large_system_diff_pull_force_frames13_41_51.pkl', 'rb') as f:
    all_results = pickle.load(f)

# Load stress-strain data
df_mechanical = pd.read_pickle('data/simulations_large_diff_pull_force/stress_strain_5seeds.pkl')
```

**Note:** The large pickle files (681 MB) may require ~1-2 GB of RAM when fully loaded into memory due to decompression and Python object overhead.

## Notes

- Raw molecular dynamics trajectories and full intermediate analysis outputs are not included due to size constraints
- The provided datasets and notebooks are sufficient to reproduce the quantitative results and plotted figures reported in the manuscript
- All notebooks use pickle format version 4.0
- Data files use relative paths (`data/...`) so notebooks should be run from the repository root
- Some notebooks may take several minutes to run due to large data files
- Color schemes use `TwoSlopeNorm` for diverging colormaps centered on specific α values



