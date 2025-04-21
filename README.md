# Seurat-Based Single-Cell RNA-seq Analysis of Mouse Brain Cortex

This repository documents a detailed scRNA-seq analysis pipeline built using **Seurat** to explore transcriptomic diversity in mouse brain cortex samples, downsampled from a larger dataset for memory efficiency. 

## Project Overview
This project processes and analyzes single-cell RNA-seq data from a filtered 10x Genomics matrix of mouse brain samples (Alzheimer's model). We create a Seurat object, perform quality control, normalization, PCA, UMAP visualization, clustering at multiple resolutions, and marker gene identification.

## Objectives
- Load and structure raw gene expression data into a Seurat object
- Downsample cells for manageable computation
- Normalize and scale the data
- Run PCA and UMAP for dimensionality reduction
- Cluster cells at increasing resolutions
- Identify and visualize marker genes

## Dataset Description
- Source: 10x Genomics h5 file containing multi-modal data
- Total cells: ~33,459
- Features: ~32,286 genes
- Subsampled to: 15,000 cells

## Pipeline Summary

### 1. Data Input and Preprocessing
- Load 10X `.h5` file using `Read10X_h5()`
- Retain only the `Gene Expression` matrix
- Create a Seurat object: `CreateSeuratObject()`
- Downsample to 15,000 cells: `subset(..., downsample=15000)`

### 2. Quality Control
- Calculate mitochondrial content: `PercentageFeatureSet()`
- Violin plots of QC metrics: `VlnPlot()`
- Scatter plot of gene vs UMI counts: `FeatureScatter()`

### 3. Normalization & Feature Selection
- Normalize data: `NormalizeData()`
- Find highly variable genes: `FindVariableFeatures()`

### 4. Scaling & Dimensionality Reduction
- Scale data: `ScaleData()`
- PCA computation: `RunPCA()`
- Extract PCA loadings for interpretation

### 5. UMAP Visualization
- Run UMAP: `RunUMAP(dims=1:10)`
- UMAP plots across resolutions: `DimPlot()`

### 6. Clustering at Multiple Resolutions
- Resolutions tested: 0.02 to 0.3
- Cluster assignments: `FindClusters()`
- Visualize clusters on UMAP and PCA

### 7. Marker Gene Analysis
- Use `FindMarkers()` for specific cluster comparisons
- Use `FindAllMarkers()` for top genes across all clusters
- Visualize expression via:
  - `VlnPlot()`
  - `FeaturePlot()`
  - `DoHeatmap()`

## Key Results
- Identified distinct clusters of brain cell types with high confidence
- Cluster 8 markers: **Flt1, Slco1a4, Mecom, Ptprb**
- Cluster 5 markers: **Hexb, Ctss, Inpp5d**
- Top variable genes included **Apoe, Zbtb20, Slc1a3, Gfap**

## Scalability
This pipeline supports datasets of varying sizes and origins:
- Can handle >30,000 cells with Seurat’s sparse matrix support
- Scalable UMAP and PCA via reduced dimensions
- Easily adjustable resolution settings for fine-tuned clustering
- Compatible with extended workflows like label transfer, multi-modal integration (e.g., ATAC+RNA), and trajectory analysis.


## Tech Stack
- **R**: Seurat, ArchR, ggplot2, dplyr, Matrix
- **Data format**: 10x Genomics `.h5`
- **Visuals**: UMAP, PCA, Violin plots, Feature plots, Heatmaps

## Key Visualizations
### 1. Violin Plot of Cell QC Metrics
Displays distribution of detected genes, UMI counts, and mitochondrial read fraction.
<img width="410" alt="Screenshot 2025-04-20 at 9 48 27 PM" src="https://github.com/user-attachments/assets/b8187b4c-04dc-435c-9a05-3dacb2804109" />

### 2. Violin Plots for Marker Genes
Expression of `Adgrl3` and `Hexb` across clusters, highlighting cluster-specific enrichment.
<img width="414" alt="Screenshot 2025-04-20 at 9 49 13 PM" src="https://github.com/user-attachments/assets/dc37b665-b6b3-4d20-898d-4024c0029ff3" />

### 3. Gene Expression Feature Plots on UMAP
Spatial distribution of genes like `Synpo2`, `Btbd11`, `Gja1`, and `Cnr1` across the UMAP space.
<img width="415" alt="Screenshot 2025-04-20 at 9 49 30 PM" src="https://github.com/user-attachments/assets/15750d59-24cf-4790-90ae-8acc295ba18d" />

## Insights & Applications
- Captures heterogeneity in mouse brain cell populations
- Highlights transcriptional signatures in Alzheimer’s disease model
- Serves as a foundation for downstream annotation or integration workflows

## License
MIT License
