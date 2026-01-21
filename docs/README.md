# Extended Thesis Documentation

This directory contains comprehensive documentation for the thesis research on cloud cover mitigation in satellite image time series for crop mapping applications.

## Table of Contents

1. [Introduction & Motivation](#introduction--motivation)
2. [Detailed Methodology](#detailed-methodology)
3. [Experimental Setup](#experimental-setup)
4. [Results & Analysis](#results--analysis)
5. [Limitations](#limitations)
6. [Future Directions](#future-directions)
7. [Literature Review Summary](#literature-review-summary)
8. [Reproducibility Guide](#reproducibility-guide)

---

## Introduction & Motivation

### The Cloud Cover Problem in Remote Sensing

Optical remote sensing satellites provide critical data for agricultural monitoring, environmental change detection, and climate studies. However, these systems face a fundamental limitation: **cloud obstruction**. Clouds cover more than one-third of Earth's land surface on average, creating persistent data gaps that compromise:

1. **Temporal Continuity:** Missing observations during key phenological stages (planting, flowering, harvest)
2. **Classification Accuracy:** Cloud-masked pixels may be misidentified as water bodies or non-vegetated surfaces
3. **Yield Prediction:** Incomplete time series reduce the reliability of crop productivity forecasts
4. **Resource Management:** Delayed detection of crop stress hinders timely irrigation and pest control interventions

### Why This Research Matters

- **Food Security:** Global population projected to reach 9.7 billion by 2050, requiring 70% increase in food production
- **Climate Adaptation:** Extreme weather events necessitate resilient monitoring systems for agricultural risk management
- **Precision Agriculture:** Farmers increasingly rely on satellite-based decision support tools requiring high-quality, gap-free data
- **Sustainable Development:** UN SDG 2 (Zero Hunger) and SDG 13 (Climate Action) depend on accurate agricultural monitoring

### Research Gap

While numerous cloud removal methods exist, few studies:
1. **Systematically compare** traditional and deep learning approaches on real-world agricultural datasets
2. **Validate preservation** of critical phenological patterns (seasonal peaks, senescence timing)
3. **Provide practical guidance** on method selection based on computational resources and accuracy requirements
4. **Integrate multi-source data** (optical + SAR) for robust all-weather monitoring

This thesis addresses these gaps through empirical validation on Italian agricultural regions with varying cloud conditions across multiple years (2018, 2021, 2022).

---

## Detailed Methodology

### 1. Study Area & Data Acquisition

**Geographic Focus:** Italy (Northern, Central, Southern regions)

**Temporal Coverage:** 2018–2022 (selected years: 2018, 2021, 2022)

**Datasets:**

| Sensor | Product | Resolution (Temporal/Spatial) | Spectral Bands | Purpose |
|--------|---------|-------------------------------|----------------|---------|
| VIIRS | FPAR | 8 days / 1000m | N/A (derived index) | Primary vegetation metric |
| Sentinel-2 | MSI L2A | 5 days / 10-60m | 13 (VIS-SWIR) | High-resolution optical context |
| Sentinel-1 | GRD | 12 days / 10m | C-band VV/VH | Cloud-penetrating structural data |
| MODIS | MOD13Q1 | 16 days / 250m | 7 (VIS-NIR) | Long-term trend validation |

**FPAR (Fraction of Absorbed Photosynthetically Active Radiation):**
- Quantifies proportion of incoming solar radiation (400-700nm) absorbed by vegetation
- Range: 0 (bare soil/water) to 1 (dense, healthy vegetation)
- Critical for monitoring photosynthetic capacity, biomass estimation, and stress detection

### 2. Preprocessing Pipeline

#### Step 1: Cloud Masking (Fmask Algorithm)
```python
# Pseudocode for cloud detection
for each_image in time_series:
    # Brightness threshold
    bright_mask = (blue_band > 0.25) & (nir_band > 0.25)
    
    # Temperature threshold (cirrus clouds)
    temp_mask = thermal_band < 270  # Kelvin
    
    # Cloud probability (machine learning classifier)
    cloud_prob = fmask_classifier(spectral_features)
    
    # Final mask
    cloud_mask = bright_mask | temp_mask | (cloud_prob > 0.65)
    
    # Shadow detection (geometric model)
    shadow_mask = project_shadows(cloud_mask, solar_zenith, solar_azimuth)
    
    # Combined quality mask
    quality_mask = cloud_mask | shadow_mask
```

#### Step 2: Atmospheric Correction

- **Method:** Sen2Cor for Sentinel-2 (converts Top-of-Atmosphere to Bottom-of-Atmosphere reflectance)
- **Aerosol Retrieval:** Dark Dense Vegetation (DDV) method
- **Water Vapor Correction:** APDA (Atmospheric Pre-corrected Differential Absorption) algorithm

#### Step 3: Normalization & Temporal Alignment
```python
# FPAR normalization
fpar_norm = (fpar - fpar_min) / (fpar_max - fpar_min)  # Scale to [0, 1]

# Seasonal detrending (optional for anomaly detection)
from statsmodels.tsa.seasonal import seasonal_decompose
decomposition = seasonal_decompose(fpar_series, model='additive', period=46)  # 46 = annual cycle at 8-day resolution
fpar_detrended = decomposition.observed - decomposition.seasonal
```

#### Step 4: Quality Filtering

- Remove pixels with FPAR quality flags indicating:
  - Sensor saturation
  - High aerosol optical depth (AOD > 0.3)
  - Snow/ice contamination
  - Unreliable retrieval (algorithm convergence failures)

### 3. Gap-Filling Methods

#### 3.1 Baseline: Mean Imputation

**Principle:** Replace missing values with the temporal mean of available observations
```python
def mean_imputation(time_series, mask):
    """
    Args:
        time_series: Array of shape (T, H, W) where T is time steps
        mask: Binary mask (1 = valid, 0 = missing)
    Returns:
        filled_series: Reconstructed time series
    """
    filled_series = time_series.copy()
    for h in range(H):
        for w in range(W):
            pixel_series = time_series[:, h, w]
            valid_values = pixel_series[mask[:, h, w] == 1]
            if len(valid_values) > 0:
                fill_value = np.mean(valid_values)
                filled_series[mask[:, h, w] == 0, h, w] = fill_value
    return filled_series
```

**Advantages:**
- Computationally efficient (O(T × H × W))
- No training required
- Stable, deterministic results

**Limitations:**
- Ignores temporal trends and seasonal patterns
- Oversimplifies natural vegetation dynamics
- Cannot capture abrupt changes (e.g., harvest events)

#### 3.2 Advanced: CRLI Framework

**Full Name:** Clustering Representation Learning on Incomplete Time-Series Data

**Architecture:**
