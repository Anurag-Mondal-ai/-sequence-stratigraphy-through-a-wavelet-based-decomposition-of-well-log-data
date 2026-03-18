# Sequence-stratigraphy-through-a-wavelet-based-decomposition-of-well-log-data
Identifying sequence boundaries is crucial for gas reservoir characterization. This study uses continuous wavelet transform (CWT) to analyze gamma ray and porosity logs at multiple scales. Discrete wavelet transform (DWT) further decomposes logs into approximations (A) and details (D) for frequency-based analysis.
# Wavelet-Based Sequence Stratigraphy Analysis from Well Logs

## Overview

This project implements a wavelet-based workflow for identifying stratigraphic features (e.g., sequence boundaries, maximum flooding surfaces) from well log data. The approach follows methodologies presented in research literature, using Continuous Wavelet Transform (CWT) and Discrete Wavelet Transform (DWT) for signal decomposition and interpretation.

The workflow integrates geophysical logs such as Gamma Ray (GR), Porosity (NPHI), Density (RHOB), and Resistivity (RT) to analyze subsurface stratigraphic variations.

---

## Objectives

* Select the most suitable wavelet for well log analysis
* Perform signal decomposition using wavelet transforms
* Generate scalograms for visual interpretation
* Identify stratigraphic boundaries and systems tracts

---

## Input Data

The input dataset (`df_cwt`) contains the following well log curves:

* **DEPT** – Depth (m)
* **HSGR_clean** – Gamma Ray log
* **NPHI_shcorr** – Shale-corrected neutron porosity
* **RHOB_clean** – Bulk density
* **APLC_clean** – Porosity log
* **RT_clean** – Resistivity
* **HCGR_clean** – Corrected gamma ray
* **Vsh** – Volume of shale

---

## Methodology

### 1. Signal Preprocessing

* Remove missing values
* Normalize signals
* Ensure consistent depth sampling

---

### 2. Wavelet Selection (Matching Pursuit Approach)

* Test multiple wavelet families:

  * Haar, Daubechies (db), Symlets (sym), Coiflets (coif)
  * Biorthogonal (bior), Reverse Biorthogonal (rbio), Meyer (dmey)
* Perform sparse reconstruction
* Compute Mean Squared Error (MSE)
* Select optimal wavelet (e.g., **db5**)

---

### 3. Continuous Wavelet Transform (CWT)

* Apply CWT on Gamma Ray log
* Use scales from 1 to 32
* Generate scalogram (time-frequency representation)

**Purpose:**

* Detect stratigraphic discontinuities
* Highlight energy distribution across scales

---

### 4. Multi-Track Visualization

A 4-track well log panel is generated:

| Track   | Description                                 |
| ------- | ------------------------------------------- |
| Track 1 | Gamma Ray (HSGR_clean)                      |
| Track 2 | Porosity (APLC) + Density (RHOB, dual axis) |
| Track 3 | Resistivity (RT, log scale)                 |
| Track 4 | CWT Scalogram                               |

---

### 5. Interpretation Strategy

* **High-energy bands (CWT)** → Sequence boundaries
* **Broad maxima (GR)** → Maximum Flooding Surface (MFS)
* **Low GR + high RT** → Sand / reservoir zones

---

## Key Results

* Optimal wavelet identified using MSE-based selection
* Scalogram provides enhanced resolution of stratigraphic features
* Wavelet transform amplifies both sharp and subtle variations in logs

---

## Dependencies

* Python 3.x
* NumPy
* Matplotlib
* PyWavelets (`pywt`)
* Scikit-learn

Install dependencies:

```bash
pip install numpy matplotlib pywavelets scikit-learn
```

---

## Usage

1. Load cleaned well log data into `df_cwt`
2. Run wavelet selection code
3. Apply CWT on Gamma Ray log
4. Generate 4-track visualization
5. Interpret stratigraphic features

---

## Notes

* CWT is applied only to the Gamma Ray log as it best captures lithological variation
* Shale-corrected porosity (`NPHI_shcorr`) is used for wavelet selection
* Proper depth alignment is critical for accurate interpretation

---

## Future Work

* Automated detection of sequence boundaries (SB, MFS)
* Integration with machine learning for classification
* Extension to 3D seismic attributes

---

## References

* Kadkhodaie, A., & Rezaee, R. (2017). Sequence stratigraphy using wavelet transform
* Wavelet-based signal processing literature

