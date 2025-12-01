# In-/Out-of-Phase MRI to PDFF Mapping (IOP)

This repository contains analysis notebooks and summary outputs from a research project exploring how to predict quantitative liver fat maps (proton density fat fraction, **PDFF**) from routine in-phase and out-of-phase MRI scans.

The goal of this work is to investigate whether standard clinical MRI sequences, which are already acquired in many abdominal exams, can be used to approximate PDFF maps that typically require longer, specialized acquisitions. If successful, this approach could shorten scan times, reduce cost, and make quantitative liver fat assessment more accessible.

---

## Project Overview

**Key ideas:**

- Use paired **in-phase / out-of-phase** MRI and ground-truth **PDFF** images.
- Build an end-to-end pipeline that:
  - Loads and organizes image data.
  - Performs basic preprocessing and alignment/registration.
  - Trains a deep learning model to map from in-/out-of-phase images to PDFF.
  - Evaluates performance quantitatively and summarizes results.

---

## Repository Structure

- `iop.ipynb`  
  Main notebook for the **in-/out-of-phase → PDFF** analysis pipeline.  
  Includes data loading, preprocessing, model training, and basic evaluation.

- `totalsegmentor.ipynb`  
  Exploratory notebook using **TotalSegmentator** (or similar segmentation tools) to segment liver or related anatomy, and to extract region-based statistics from PDFF or predicted maps.

- `iop_output.xlsx`  
  Aggregate output metrics (e.g., error statistics or performance summaries) across the dataset.

- `iop_mean_sd_summary.xlsx`  
  Summary statistics (e.g., mean and standard deviation of relevant metrics) for different regions or experimental settings.

- `iop_output_circle_5.xlsx`  
- `iop_output_circle_10.xlsx`  
- `iop_output_circle_15.xlsx`  
  Output files related to experiments using circular regions of different sizes (e.g., to sample local PDFF or error distributions in a controlled way).

---

## Methods

- **Input:** Co-registered in-phase and out-of-phase MRI images.
- **Target:** Corresponding PDFF maps.
- **Preprocessing:**  
  - Intensity normalization and basic cleaning.  
  - Registration/alignment of multiple MRI series into a shared spatial frame.  
- **Modeling:**  
  - A convolutional neural network (e.g., U-Net-style architecture) that takes in-phase and out-of-phase images as input channels.  
  - Predicts a single-channel PDFF map.
- **Evaluation:**  
  - Pixel-wise comparison between predicted and ground-truth PDFF (e.g., MAE, MSE).  
  - Region-based summary statistics (e.g., mean PDFF within defined ROIs).  
  - Spreadsheet outputs in this repo capture these summary metrics.

---

## Environment & Dependencies

The notebooks are written in **Python** using **Jupyter**. Typical dependencies include:

- `numpy`, `pandas`
- `matplotlib`
- `scikit-image`, `scipy`
- `scikit-learn`
- A deep learning framework such as **PyTorch** or **TensorFlow/Keras**
- Medical imaging utilities (e.g., `pydicom`, `nibabel`) if working directly with DICOM/NIfTI files
- Segmentation toolkit (e.g., TotalSegmentator or equivalent) for the `totalsegmentor.ipynb` notebook

---

## How to Use This Repository

1. **Review the methodology:**  
   Open `iop.ipynb` in Jupyter or GitHub’s notebook viewer to follow the analysis pipeline and model training steps.

2. **Inspect summary results:**  
   Explore the `.xlsx` files (e.g., `iop_output.xlsx` and `iop_mean_sd_summary.xlsx`) to see aggregated performance metrics and experimental results.

3. **Adapt the workflow:**  
   If you have access to your own in-phase/out-of-phase + PDFF MRI data, you can adapt the preprocessing and modeling sections in `iop.ipynb` to your dataset and environment.
