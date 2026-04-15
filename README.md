# Multi-Omic Manifold Alignment and Regulatory Decoherence in Wiedemann-Steiner Syndrome

## Project Overview
This project presents a computational framework to quantify the regulatory gap between the epigenetic "blueprint" (DNA Methylation) and transcriptional "execution" (RNA Expression) in Wiedemann-Steiner Syndrome (WSS). WSS is a rare neurodevelopmental disorder caused by mutations in the KMT2A gene, a major histone methyltransferase. 

By utilizing non-linear manifold learning and geometric superimposition, this study identifies a systemic breakdown in cellular synchronization, termed "Regulatory Decoherence," characterized by a global Disparity Score of approximately 0.93.

## Biological Context
KMT2A acts as a master architect of the chromatin landscape. Mutations lead to a failure in maintaining the correct "regulatory manifold," where the physical instructions encoded in the DNA are no longer accurately translated into gene expression. This project integrates human clinical episignatures with experimental mouse transcriptomes to map the topography of this failure.

## Methodology

### 1. Data Acquisition and Preprocessing
The analysis integrates two distinct omics layers:
* **DNA Methylation (Human):** GSE125367 (Illumina EPIC/450k array).
* **RNA Expression (Mouse):** GSE99250 (Bulk RNA-seq).
* **Ortholog Mapping:** Mouse Ensembl IDs were translated to Human Gene Symbols via the MyGene.info API to facilitate cross-species integration.

### 2. Dimensionality Reduction and Denoising
Given the high dimensionality of genomic data (866,150 DNA probes and 38,360 RNA transcripts), Principal Component Analysis (PCA) was applied to retain the top 30 components, capturing over 90% of cumulative variance while removing stochastic noise.

### 3. Manifold Construction (Isomap)
Non-linear manifolds were constructed for both layers using Isomap. Unlike linear methods, Isomap preserves the global geodesic structure of the gene regulatory network, projecting the data into a 3D coordinate system representing the "Regulatory Shape" of the cell.

### 4. Procrustes Superimposition
To quantify the gap between layers, the RNA manifold was geometrically aligned to the DNA manifold using Procrustes Analysis. This process involves translation, scaling, and rotation to find the optimal alignment, followed by the calculation of a normalized Disparity Score (Sum of Squared Differences).

## Key Results

### Global Disparity Score: 0.9881
A score of 1.0 represents total randomness, while 0.0 represents perfect synchronization. A score of ~0.98 indicates a near-total collapse of the regulatory link between DNA methylation and RNA output in KMT2A-deficient states.

### Top Regulatory Breakpoints (Gene Level)
The following genes exhibited the highest Euclidean distances between their DNA and RNA coordinates, marking them as the primary drivers of the syndrome's phenotype:

| Rank | Gene Symbol | Decoherence Score | Biological Significance |
| :--- | :--- | :--- | :--- |
| 1 | WNT3 | 0.2688 | Embryonic morphogenesis and limb development. |
| 2 | FGF23 | 0.2655 | Bone mineralization and phosphate homeostasis. |
| 3 | BRAT1 | 0.2640 | DNA damage response and cell growth. |
| 4 | COX5A | 0.2547 | Mitochondrial oxidative phosphorylation. |
| 5 | APOH | 0.2246 |Lipid metabolism and coagulation signaling. |
| 5 | LRP5 | 0.2003 | Wnt-mediated bone mass regulation. |

## Repository Structure
* **/data**: Contains processed RNA counts, mapping metadata, and links to raw NCBI GEO files.
* **/notebooks**: Jupyter Notebook containing the Python 3.12 pipeline (PCA, Isomap, Procrustes).
* **/results**: CSV files of gene-level decoherence scores and 3D manifold visualizations.
* **/images**: PNG exports of the alignment manifolds and decoherence heatmaps.

## Technical Stack
* **Language:** Python 3.12 (Google Colab Environment)
* **Libraries:** Scikit-Learn (Manifold Learning), Scipy (Procrustes Analysis), MyGene (ID Translation), Pandas/Numpy (Matrix Manipulation), Matplotlib/Mplot3d (Visualization).
