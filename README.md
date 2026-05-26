# Spatial-Temporal Defect Segmentation in Composite Laminates using Active Thermography

This repository contains an independent engineering implementation and benchmarking framework for subsurface defect detection in Carbon Fiber-Reinforced Polymer (CFRP) laminates. The project focuses on processing multi-frame temporal thermal signatures to segment hidden structural anomalies, serving as a practical exploration of advanced industrial metrology pipelines.

## Project Overview
Detecting sub-surface defects in multi-layered structures presents severe signal-to-noise ratio (SNR) challenges, as anomalies are heavily obscured by surface non-uniformity and sensor background noise. 

This framework takes a physics-informed approach to machine vision:
1. **Signal Preprocessing & Enhancement:** Evaluates temporal heat dissipation behavior following an active thermal excitation pulse.
2. **Feature Extraction Layer:** Isolates peak-contrast frames to compile low-noise multi-channel input tensors.
3. **Semantic Segmentation Network:** Trains deep learning architectures (U-Net / DeepLabv3+) to precisely map the geometries of subsurface delaminations.

---

## Dataset Characteristics
This implementation utilizes the public **Thermal Inspection Dataset for Defect Segmentation in CFRP Laminates** provided by Garcia Vargas & Fernandes (2025) via Mendeley Data.

### Specimen Metrology & Parameters:
* **Material Composition:** Unidirectional carbon/PEEK laminate (APC-2/AS4), 61% fiber volume fraction.
* **Structural Lay-up:** $[0_2/90_2]_6$ stacking sequence, dimensions $100 \times 100\text{ mm}$.
* **Target Anomalies:** Artificial Kapton tape inserts introduced during moulding to simulate internal voids and delaminations.
  * **Nominal Dimensions:** $2 \times 2\text{ mm}$, $3 \times 3\text{ mm}$, $4 \times 4\text{ mm}$.
  * **Target Depths:** $D1 = 0.13\text{ mm}$, $D2 = 0.26\text{ mm}$, $D3 = 0.39\text{ mm}$.

### Sensor Configuration:
* **Modality:** Pulsed Thermography (PT) under active optical excitation.
* **Detector:** Midwave Infrared (MWIR) photon-counting camera.
* **Resolution & Dynamics:** $640 \times 512$ pixels captured at a transient frame rate of $55\text{ Hz}$ (1,034 total sequence frames).

---

## Implementation Details

### Core Technical Focus:
* **Data Allocation:** Automatic pipeline synchronization of raw thermal tracking arrays and corresponding expert-labeled ground-truth masks.
* **Imbalance Optimization:** Custom implementation of specialized loss configurations (Dice and Focal Loss options) to counteract high class-imbalance boundaries where sound laminate background values dominate over defect regions.
* **Industrial Validation Strategy:** Post-processing layers engineered to isolate regional cluster statistics, determining continuous defect coverage areas ($mm^2$) to simulate real-world automated quality verification criteria.

---

## Technical Stack & Dependencies
* **Language Environment:** Python
* **Vision & Matrix Processing:** OpenCV, NumPy, Scikit-Image
* **Deep Learning Framework:** PyTorch, Torchvision
* **Hardware Utilization:** Google Colab Pro Runtime (NVIDIA T4 / V100 Acceleration)

---

## Data License, Citations, and Acknowledgments

### Data Source Attribution
The original raw thermal sequences, ground-truth annotations, and expert-labeled masks are used under license from the contributors via Elsevier Mendeley Data. 

* **Repository Link:** [Mendeley Data - Thermal Inspection Dataset for Defect Segmentation in CFRP Laminates](https://data.mendeley.com/datasets/jrsb4b9yy5)

### Academic Citations
If you utilize this repository or build upon this derivative framework, please properly credit the original authors of the dataset and the associated baseline methodology:

```bibtex
@misc{garciavargas2025dataset,
  author = {Garcia Vargas, Iago and Fernandes, Henrique},
  title = {Thermal Inspection Dataset for Defect Segmentation in CFRP Laminates},
  year = {2025},
  publisher = {Mendeley Data},
  version = {V1},
  doi = {10.17632/jrsb4b9yy5.1}
}

@article{garciavargas2025methodology,
  author = {Garcia Rosa, Renan and Barella, Bruno Pereira and Garcia Vargas, Iago and Tarpani, Jos{\'e} Ricardo and Herrmann, Hans-Georg and Fernandes, Henrique},
  title = {Advanced Thermal Imaging Processing and Deep Learning Integration for Enhanced Defect Detection in Carbon Fiber-Reinforced Polymer Laminates},
  journal = {Materials},
  volume = {18},
  number = {7},
  pages = {1448},
  year = {2025},
  doi = {10.3390/ma18071448}
}
