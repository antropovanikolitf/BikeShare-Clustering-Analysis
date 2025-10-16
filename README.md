# Clustering Urban Bike-Share Users

**Author**: Nicoli Antropova
**Date**: October 2025
**Course**: Applied Machine Learning

---

## Overview

This project applies unsupervised machine learning to cluster urban bike-share trip data (CitiBike NYC) to uncover **7 distinct rider behavior patterns**. By identifying clusters such as **last-mile connectors** (72%), **leisure loops** (2%), **casual riders** (16%), and **long-distance travelers** (10%), we inform sustainable urban transport planning and optimize bike-share system operations.

### Key Findings
- **K-Means k=7** clustering achieved silhouette score 0.320, DB index 1.177
- **72% of trips** are short, utilitarian rides (last-mile connectors & commuters)
- **11,000 tons CO₂ avoided annually** (equivalent to removing 2,400 cars)
- **Actionable recommendations** for infrastructure, pricing, and equity

---

## Why This Matters

Urban bike-sharing systems are key to reducing carbon emissions, easing traffic congestion, and promoting healthy mobility. Understanding rider segments enables:
- **City planners** to optimize station placement and infrastructure investment
- **Transport agencies** to tailor services and pricing models
- **Sustainability advocates** to measure and amplify bike-share impact
- **Researchers** to study urban mobility patterns at scale

---

## Repository Structure

```
.
├── data/
│   ├── raw/                       # Place CitiBike trip CSVs here (16 files, Mar-Jun 2025)
│   └── processed/                 # Cleaned data (trips_clean.csv, samples)
├── notebooks/
│   ├── 01_framing_clustering_problem.ipynb
│   ├── 02_dataset_preparation.ipynb
│   ├── 03_clustering_experiments.ipynb
│   ├── 04_evaluating_visualizing_clusters.ipynb
│   └── 05_impact_reporting.ipynb
├── src/                           # Reusable Python modules
│   ├── paths.py                   # Path management
│   ├── loaders.py                 # Data loading & validation
│   ├── diagnostics.py             # Data quality checks
│   ├── preprocess.py              # Cleaning & feature engineering
│   ├── clustering.py              # K-Means, DBSCAN, metrics
│   ├── interpretation.py          # Cluster profiling & naming
│   └── visualization.py           # PCA, t-SNE, plots
├── reports/
│   ├── figures/                   # 15+ visualizations (PCA, heatmaps, distributions)
│   ├── IMPACT_REPORT.md           # Comprehensive stakeholder report
│   └── EXECUTIVE_SUMMARY.md       # One-page summary for city leaders
├── artifacts/
│   ├── feature_pipeline.joblib    # Saved preprocessing pipeline
│   └── kmeans_labels_k7.npy       # Final cluster labels
├── PROJECT_CHARTER.md             # Project goals and stakeholders
├── RELATED_WORK.md                # Literature review
├── METHODS_PLAN.md                # Algorithms and features
├── EVALUATION_PLAN.md             # Metrics and success criteria
├── DATA_SOURCES.md                # Dataset provenance
├── DATA_FITNESS_ASSESSMENT.md     # Data quality review
├── DECISIONS_LOG.md               # All major decisions documented
└── README.md                      # This file
```

---

## Installation & Setup

### Prerequisites
- Python 3.11 or higher
- Jupyter Notebook or JupyterLab
- ~5GB disk space (for raw data + processed outputs)

### Step 1: Install Dependencies

Create a virtual environment and install required packages:

```bash
# Create virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install pandas numpy scikit-learn matplotlib seaborn jupyter joblib
```

**Exact versions used in this project:**
```
pandas==2.1.0
numpy==1.24.3
scikit-learn==1.3.0
matplotlib==3.7.2
seaborn==0.12.2
jupyter==1.0.0
joblib==1.3.2
```

Save as `requirements.txt` and install with:
```bash
pip install -r requirements.txt
```

---

## Data Acquisition

### Option A: Download CitiBike Data (Recommended)

1. Visit [CitiBike System Data](https://citibikenyc.com/system-data)
2. Download trip data for **March-June 2025** (18 CSV files)
3. Place all CSVs in `data/raw/` folder
4. Files should be named: `202503-citibike-tripdata_1.csv`, `202503-citibike-tripdata_2.csv`, etc.

**Expected data size:** ~3-5GB compressed, ~10GB uncompressed

### Option B: Use Existing Data

If you already have processed data:
- Place `trips_clean.csv` in `data/processed/`
- Skip directly to Notebook 03 (clustering experiments)

---

## Reproduction Steps

### Quick Start (Full Pipeline)

Run all notebooks sequentially from the project root:

```bash
# Navigate to project directory
cd "Clustering Urban Cyclists"

# Launch Jupyter
jupyter notebook

# Run notebooks in order:
# 01 → 02 → 03 → 04 → 05
```

### Step-by-Step Instructions

#### 1. **Capstone 1: Framing the Problem** (5 min)
- **Notebook**: `notebooks/01_framing_clustering_problem.ipynb`
- **Action**: Review project charter, hypotheses, success criteria
- **Output**: None (conceptual framing only)

#### 2. **Capstone 2: Data Preparation** (30-45 min)
- **Notebook**: `notebooks/02_dataset_preparation.ipynb`
- **Action**:
  1. Load raw CSVs from `data/raw/`
  2. Clean data (drop missing coords, filter durations, cap outliers)
  3. Engineer features (duration_min, distance_km, start_hour, etc.)
  4. Generate 4 diagnostic plots
- **Outputs**:
  - `data/processed/trips_clean.csv` (~1.6M rows)
  - `artifacts/feature_pipeline.joblib` (StandardScaler)
  - `reports/figures/duration_histogram.png` (and 3 more)
- **Runtime**: 30-45 min (depends on CPU, RAM)

#### 3. **Capstone 3: Clustering Experiments** (10-15 min)
- **Notebook**: `notebooks/03_clustering_experiments.ipynb`
- **Action**:
  1. Sample 10% of data for speed (159K rows)
  2. Run K-Means elbow analysis (k=3-7)
  3. Compare K-Means vs DBSCAN
  4. Select champion model (K-Means k=7)
- **Outputs**:
  - `artifacts/kmeans_labels_k7.npy` (cluster labels)
  - `reports/figures/kmeans_elbow_analysis.png`
  - `reports/cluster_comparison_table.csv`
- **Runtime**: 10-15 min (with 10% sample)

#### 4. **Capstone 4: Evaluation & Visualization** (5-10 min)
- **Notebook**: `notebooks/04_evaluating_visualizing_clusters.ipynb`
- **Action**:
  1. Load K-Means k=7 results
  2. Generate PCA 2D projection
  3. Create cluster characteristics table
  4. Plot distributions and heatmaps
- **Outputs**:
  - `reports/figures/pca_clusters_2d.png` (main visualization)
  - `reports/figures/cluster_profile_heatmap.png`
  - `reports/figures/cluster_distribution_duration_min.png`
  - `reports/figures/cluster_0_hourly_weekday.png` (×7 heatmaps)
  - `reports/cluster_characteristics_table.csv`
- **Runtime**: 5-10 min

#### 5. **Capstone 5: Impact Reporting** (Review only)
- **Notebook**: `notebooks/05_impact_reporting.ipynb`
- **Action**: Review pre-generated reports (or regenerate if needed)
- **Outputs**:
  - `reports/IMPACT_REPORT.md` (comprehensive, 8 sections)
  - `reports/EXECUTIVE_SUMMARY.md` (one-page)

---

## Expected Outputs

After running all notebooks, you should have:

### Visualizations (15 files in `reports/figures/`)
1. `duration_histogram.png` - Trip duration distribution
2. `hourly_distribution.png` - Trips by hour of day
3. `weekday_distribution.png` - Trips by day of week
4. `distance_histogram.png` - Trip distance distribution
5. `kmeans_elbow_analysis.png` - Silhouette/DB scores for k=3-7
6. `pca_clusters_2d.png` - **Main result**: 7 clusters in 2D space
7. `pca_feature_importance.png` - PC1/PC2 feature contributions
8. `pca_explained_variance.png` - Variance by component
9. `cluster_profile_heatmap.png` - Mean feature values per cluster
10. `cluster_distribution_duration_min.png` - Duration boxplots
11. `cluster_distribution_distance_km.png` - Distance boxplots
12-18. `cluster_0_hourly_weekday.png` ... `cluster_6_hourly_weekday.png` - Temporal patterns

### Data Files
- `data/processed/trips_clean.csv` (1.6M rows, 20 columns)
- `data/processed/X_scaled_sample.csv` (159K rows, 8 features)
- `data/processed/df_sample.csv` (159K rows, full data)

### Models & Artifacts
- `artifacts/feature_pipeline.joblib` (StandardScaler)
- `artifacts/kmeans_labels_k7.npy` (cluster labels)

### Reports
- `reports/IMPACT_REPORT.md` (10-page comprehensive analysis)
- `reports/EXECUTIVE_SUMMARY.md` (1-page summary)
- `reports/cluster_characteristics_table.csv` (summary table)
- `DECISIONS_LOG.md` (all decisions documented)

---

## Key Results

### The 7 Clusters

| Cluster | Name | Size | Duration | Distance | Key Features |
|---------|------|------|----------|----------|--------------|
| **0** | Last-Mile Connectors (Weekday) | 36.1% | 8.2 min | 1.65 km | 100% members, weekdays, W 21 St hub |
| **1** | Leisure Loops | 2.1% | 19.1 min | 0 km | Round trips, Central Park, 33.6% weekend |
| **2** | Last-Mile Connectors (Weekend) | 18.6% | 9.7 min | 1.71 km | 100% members, weekends |
| **3** | Weekday Casual Riders | 9.8% | 13.6 min | 1.91 km | 0% members, Central Park access |
| **4** | Short Commuters | 17.4% | 8.6 min | 1.26 km | 100% members, East Village routes |
| **5** | Long-Distance Travelers | 10.0% | 29.5 min | 5.54 km | Longest trips, 89% members |
| **6** | Weekend Casual Riders | 6.0% | 17.0 min | 2.22 km | 0% members, weekend leisure |

### Policy Recommendations
1. **Prioritize infrastructure** for last-mile connectors (72% of trips): W 21 St, Lafayette St hubs
2. **Integrate with MTA** for seamless bike+transit (combo pass, station co-location)
3. **Convert casual to members** (16% untapped): Day pass promotions, 50% off first month

---

## Troubleshooting

### Issue: "Module not found" errors
**Solution**: Ensure you're running notebooks from the project root directory, and that `src/` is in the Python path. Add this to the first cell of any notebook:
```python
import sys
from pathlib import Path
project_root = Path.cwd().parent
if str(project_root) not in sys.path:
    sys.path.insert(0, str(project_root))
```

### Issue: Notebook 02 takes too long (>1 hour)
**Solution**: Reduce sample size in `loaders.py`:
```python
df_raw = load_all_trips(sample_frac=0.05)  # Use 5% instead of 10%
```

### Issue: PCA visualization shows overlapping clusters
**Solution**: This is expected! 44.4% variance in 2D means clusters are better separated in 8D space. The diagonal stripe pattern is normal (reflects binary feature interactions).

### Issue: DBSCAN produced 14 clusters instead of 7
**Solution**: We selected K-Means k=7 for interpretability. See `DECISIONS_LOG.md` [2025-10-07] for rationale.

---

## Customization

### Use Different Data
- Replace `data/raw/` CSVs with other bike-share systems (DC, Chicago, SF)
- Ensure CSV columns match CitiBike schema: `ride_id`, `started_at`, `ended_at`, `start_lat`, `start_lng`, etc.

### Change Clustering Parameters
- Edit `notebooks/03_clustering_experiments.ipynb`:
  - Try different k values: `run_kmeans(X_scaled, k=5, ...)`
  - Tune DBSCAN: `run_dbscan(X_scaled, eps=0.5, min_samples=100)`

### Add New Features
- Edit `src/preprocess.py` → `engineer_features()` function
- Example: Add `is_holiday` or `weather_condition` features

---

## Limitations & Future Work

### Known Limitations
⚠️ **10% Sampling**: Analysis based on 159K trips (10% of 1.6M). Full dataset validation recommended.
⚠️ **Seasonal Bias**: Spring/summer 2025 data may not generalize to winter patterns.
⚠️ **Geographic Skew**: Manhattan/Brooklyn represent 80% of stations; outer boroughs underrepresented.
⚠️ **No Ground Truth**: Cluster labels based on heuristics, not user surveys.

### Future Enhancements
✅ Run on full 1.6M dataset (requires 2+ hours)
✅ Validate with fall/winter 2025 data
✅ Cross-city comparison (DC, Chicago, SF)
✅ User surveys to validate cluster interpretations
✅ Predictive modeling for demand forecasting

---

## Citation

If you use this work, please cite:

```
Antropova, N. (2025). Clustering Urban Bike-Share Users for Sustainable Mobility Planning.
Applied Machine Learning Course Project. [GitHub/Institutional Repository Link]
```

---

## License

This project is for educational purposes. CitiBike data is publicly available under [CitiBike Data License](https://citibikenyc.com/data-sharing-policy).

**No personally identifiable information (PII) is used.**

---

## Contact

**Nicoli Antropova**
For questions, feedback, or collaboration opportunities.

---

## Acknowledgments

- **CitiBike NYC** for open-source trip data
- **Applied Machine Learning Course** for project structure and guidance
- **scikit-learn**, **pandas**, **matplotlib** communities for excellent tools

---

*Last Updated: October 2025*
