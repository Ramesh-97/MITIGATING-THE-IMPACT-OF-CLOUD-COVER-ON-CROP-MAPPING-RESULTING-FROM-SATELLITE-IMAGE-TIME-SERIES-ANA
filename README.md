# Mitigating the Impact of Cloud Cover on Crop Mapping from Satellite Image Time Series Analysis

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)](https://www.tensorflow.org/)
[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.XXXXXXX-blue)](https://doi.org/10.5281/zenodo.XXXXXXX)

**Master's Thesis**  
University of Genoa, Department of Naval, Electrical, Electronic and Telecommunication Engineering (DITEN)  
**Author:** Ramesh Kumar Menghwar  
**Supervisor:** Prof. Gabriele Moser  
**Co-Supervisor:** Priscilla Indira Osa  
**March 2025**

---

## Abstract

Cloud cover remains a critical challenge in optical remote sensing, causing significant data gaps that compromise the accuracy and reliability of crop mapping and agricultural monitoring systems. This thesis presents a comprehensive investigation of cloud mitigation strategies for Satellite Image Time Series (SITS), with particular emphasis on Fraction of Absorbed Photosynthetically Active Radiation (FPAR) vegetation indices.

We evaluate both traditional statistical methods and advanced deep learning frameworks, including the Clustering Representation Learning on Incomplete Time-Series Data (CRLI) model, which optimizes imputation and clustering simultaneously using adversarial learning. Our analysis demonstrates that deep learning approaches substantially outperform conventional techniques like mean imputation in preserving seasonal vegetation dynamics and phenological patterns critical for precision agriculture.

The research integrates multi-source remote sensing data, including optical imagery (Sentinel-2, MODIS, VIIRS) and Synthetic Aperture Radar (SAR) data (Sentinel-1), to develop robust, cloud-resilient crop mapping solutions applicable to regions with persistent cloud cover.

**Keywords:** Remote Sensing, Cloud Removal, Satellite Image Time Series, Crop Mapping, Deep Learning, FPAR, SAR-Optical Fusion, Agricultural Monitoring

---

## Problem Statement

Optical remote sensing systems rely on reflected sunlight, making them inherently vulnerable to cloud obstruction. According to climate statistics, clouds cover more than one-third of Earth's land surface on average, causing:

- **Temporal Data Gaps:** Missing observations during critical crop growth stages
- **Reduced Monitoring Accuracy:** Incomplete time series compromise phenological analysis
- **Classification Errors:** Cloud-covered regions may be misidentified as water bodies or barren land
- **Decision-Making Delays:** Agricultural stakeholders lack timely information for irrigation, pest management, and yield prediction

These limitations are particularly severe in tropical and temperate regions with persistent cloud cover, where continuous crop monitoring is essential for food security and climate resilience.

---

## Research Objectives

1. **Systematic Review:** Analyze state-of-the-art cloud removal and gap-filling methodologies across supervised, unsupervised, and semi-supervised paradigms
2. **Performance Evaluation:** Compare traditional interpolation techniques with advanced deep learning models on real-world FPAR time series data
3. **Multi-Source Integration:** Investigate SAR-optical fusion approaches for all-weather crop monitoring
4. **Practical Validation:** Demonstrate effectiveness on Italian agricultural regions (2018, 2021, 2022) with varying cloud conditions
5. **Framework Development:** Establish guidelines for selecting appropriate reconstruction methods based on computational resources, accuracy requirements, and application constraints

---

## Methodology Overview

### Data Sources

- **VIIRS FPAR:** 8-day temporal resolution, 1000m spatial resolution covering Italy (2018–2022)
- **Sentinel-2:** Multispectral optical imagery (10-60m resolution, 13 spectral bands)
- **Sentinel-1:** C-band SAR data for cloud-penetrating structural information
- **MODIS:** Long-term time series for atmospheric correction and trend analysis

### Preprocessing Pipeline

1. **Cloud Masking:** Fmask algorithm for cloud and shadow detection
2. **Atmospheric Correction:** Surface reflectance conversion
3. **Normalization:** Scaling to [0,1] range with seasonal adjustment
4. **Quality Filtering:** Removal of low-quality observations

### Gap-Filling Techniques Evaluated

#### Traditional Methods
- **Mean Imputation:** Simple averaging of available temporal data
- **Gaussian Process Regression (GPR):** Probabilistic interpolation with uncertainty quantification
- **Savitzky-Golay Filtering:** Polynomial smoothing for noise reduction

#### Deep Learning Approaches
- **CRLI Framework:** Adversarial learning for joint imputation and clustering
- **Temporal Attention GANs:** Context-aware reconstruction with multi-scale features
- **Transformer Models:** Self-attention mechanisms for long-range temporal dependencies
- **SAR-Guided CNNs:** Multi-modal fusion networks leveraging radar backscatter

### Evaluation Metrics

- **Structural Similarity Index (SSIM):** Perceptual quality assessment
- **Peak Signal-to-Noise Ratio (PSNR):** Reconstruction fidelity
- **Mean Absolute Error (MAE):** Pixel-wise accuracy
- **Phenological Preservation:** Accuracy of seasonal peak detection

---

## Key Contributions

1. **Comprehensive Literature Analysis:** Systematic categorization of 50+ recent methods (2020–2025) by supervision paradigm, methodological approach, and input modality
2. **Empirical Validation:** Quantitative comparison of CRLI vs. mean imputation on multi-year FPAR datasets, demonstrating superior preservation of seasonal dynamics
3. **Practical Guidelines:** Decision framework for method selection based on accuracy-efficiency tradeoffs, computational constraints, and application requirements
4. **Multi-Source Integration:** Analysis of SAR-optical fusion benefits for cloud-resilient monitoring in persistently cloudy regions
5. **Open Research Foundation:** Reproducible experimental setup and comprehensive documentation for future research

---

## Architecture & Workflow
