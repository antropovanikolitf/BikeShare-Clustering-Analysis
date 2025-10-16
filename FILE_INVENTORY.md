# File Inventory & Cleanup Guide

**Author**: Nicoli Antropova
**Date**: October 2025

---

## ✅ KEEP THESE FILES (Core Project)

### Documentation (Root)
- `README.md` - **Main documentation (UPDATED with your name)**
- `PROJECT_CHARTER.md` - Project goals & stakeholders
- `RELATED_WORK.md` - Literature review
- `METHODS_PLAN.md` - Algorithm selection rationale
- `EVALUATION_PLAN.md` - Metrics & success criteria
- `DATA_SOURCES.md` - Dataset provenance
- `DATA_FITNESS_ASSESSMENT.md` - Data quality analysis
- `DECISIONS_LOG.md` - **All decisions documented (UPDATED)**

### Source Code (`src/`)
- `src/__init__.py` - Package initialization
- `src/paths.py` - Path management utilities
- `src/loaders.py` - Data loading & validation
- `src/diagnostics.py` - Data quality checks & plots
- `src/preprocess.py` - Cleaning & feature engineering
- `src/clustering.py` - K-Means, DBSCAN, metrics
- `src/interpretation.py` - Cluster profiling & naming
- `src/visualization.py` - PCA, t-SNE, plots

### Notebooks (`notebooks/`)
- `notebooks/01_framing_clustering_problem.ipynb` - Problem framing
- `notebooks/02_dataset_preparation.ipynb` - Data cleaning
- `notebooks/03_clustering_experiments.ipynb` - K-Means k=7 selection
- `notebooks/04_evaluating_visualizing_clusters.ipynb` - PCA, visualizations
- `notebooks/05_impact_reporting.ipynb` - Impact analysis

### Data Files (`data/`)
#### Raw Data (`data/raw/bikeshare/`)
- `202503-citibike-tripdata_1.csv` through `202506-citibike-tripdata_5.csv` (18 files)
- `provenance.csv` - Metadata about raw data

#### Processed Data (`data/processed/`)
- `trips_clean.csv` - **1.6M cleaned trips (main dataset)**
- `X_scaled_sample.csv` - 159K scaled features (10% sample)
- `df_sample.csv` - 159K sampled trips with all columns

#### Metadata
- `data/README.md` - Data directory documentation

### Artifacts (`artifacts/`)
- `feature_pipeline.joblib` - StandardScaler pipeline
- `kmeans_labels_k7.npy` - **Final K-Means k=7 cluster labels**

### Reports (`reports/`)
- `reports/IMPACT_REPORT.md` - **Comprehensive stakeholder report (UPDATED)**
- `reports/EXECUTIVE_SUMMARY.md` - **One-page summary (UPDATED)**
- `reports/cluster_characteristics_table.csv` - Summary table for K-Means k=7
- `reports/cluster_comparison_table.csv` - Algorithm comparison

### Visualizations (`reports/figures/`) - **18 KEEP, 7 DELETE**

#### KEEP - Essential Visualizations (18 files)
1. `duration_histogram.png` - Trip duration distribution
2. `hourly_distribution.png` - Trips by hour of day
3. `weekday_distribution.png` - Trips by day of week
4. `distance_histogram.png` - Trip distance distribution
5. `kmeans_elbow_analysis.png` - Silhouette/DB scores for k=3-7
6. `pca_clusters_2d.png` - **MAIN RESULT: 7 clusters in 2D**
7. `pca_feature_importance.png` - PC1/PC2 feature contributions
8. `pca_explained_variance.png` - Variance by component
9. `cluster_profile_heatmap.png` - Mean feature values per cluster
10. `cluster_distribution_duration_min.png` - Duration boxplots
11. `cluster_distribution_distance_km.png` - Distance boxplots
12. `cluster_size_distribution.png` - Cluster size bar chart
13-18. `cluster_0_hourly_weekday.png` through `cluster_6_hourly_weekday.png` - **K-Means k=7 heatmaps**

---

## ❌ DELETE THESE FILES (Cleanup)

### Old/Unused Notebooks
- `Untitled.ipynb` - Empty/scratch notebook
- `sample.ipynb` - Development scratch work


### Backup/Temp Files
- `.!88604!README.md` - Backup file from editor

### OLD Visualizations - DBSCAN Results (14 clusters, replaced by K-Means k=7)
- `cluster_7_hourly_weekday.png` ❌
- `cluster_8_hourly_weekday.png` ❌
- `cluster_9_hourly_weekday.png` ❌
- `cluster_10_hourly_weekday.png` ❌
- `cluster_11_hourly_weekday.png` ❌
- `cluster_12_hourly_weekday.png` ❌
- `cluster_13_hourly_weekday.png` ❌

**Reason**: These are from the OLD DBSCAN run (14 clusters). We switched to K-Means k=7, which only has clusters 0-6. See `DECISIONS_LOG.md` [2025-10-07] for rationale.

---

## Summary

### File Count
- **KEEP**: 72 files (essential project files)
- **DELETE**: 8 files (old/unused/duplicates)

### Total Project Size (after cleanup)
- **Raw data**: ~10GB (18 CSV files)
- **Processed data**: ~200MB (cleaned CSVs)
- **Code**: ~50KB (8 Python modules)
- **Notebooks**: ~5MB (5 notebooks)
- **Reports**: ~100KB (2 markdown, 2 CSV)
- **Visualizations**: ~5MB (18 PNG files)
- **Artifacts**: ~10KB (pipeline, labels)

**Total**: ~10.4GB (mostly raw data)

---

## Cleanup Commands

```bash
# Navigate to project root
cd "/Users/nantropova/Desktop/UNIVER/Applied Machine Learning/Clustering Urban Cyclists"

# Delete old notebooks
rm Untitled.ipynb sample.ipynb

# Delete backup file
rm .!88604!README.md

# Delete OLD DBSCAN visualizations (clusters 7-13)
rm reports/figures/cluster_7_hourly_weekday.png
rm reports/figures/cluster_8_hourly_weekday.png
rm reports/figures/cluster_9_hourly_weekday.png
rm reports/figures/cluster_10_hourly_weekday.png
rm reports/figures/cluster_11_hourly_weekday.png
rm reports/figures/cluster_12_hourly_weekday.png
rm reports/figures/cluster_13_hourly_weekday.png

# Verify cleanup
echo "Cleanup complete! Remaining files:"
find . -type f \( -name "*.py" -o -name "*.ipynb" -o -name "*.md" -o -name "*.csv" -o -name "*.png" \) -not -path "./.venv/*" | wc -l
```

---

## What to Submit

### For Course Submission
1. **Code & Notebooks**: All `src/` modules + 5 notebooks in `notebooks/`
2. **Reports**: `IMPACT_REPORT.md`, `EXECUTIVE_SUMMARY.md`
3. **Documentation**: `README.md`, `DECISIONS_LOG.md`, `PROJECT_CHARTER.md`, etc.
4. **Visualizations**: 18 PNG files in `reports/figures/` (after cleanup)
5. **Data** (optional): `trips_clean.csv` (if size permits; otherwise link to raw data source)

---

*Last Updated: October 2025*
