# Spatial-Temporal Defect Segmentation in CFRP Laminates using Active Thermography

This repository implements a deep learning pipeline for pixel-level defect segmentation in Carbon Fiber Reinforced Polymer (CFRP) laminates using active thermal imaging data. The system is based on a U-Net architecture trained on paired infrared images and expert-annotated masks.

---

## Problem Statement

Detecting subsurface defects in composite materials is challenging due to:

- Extremely low contrast between defect and background
- Severe class imbalance (very small defect regions)
- Noise in thermal response signals
- High variability in defect shape and depth

This project addresses these challenges using a supervised segmentation approach with deep convolutional networks.

---

## Dataset

Garcia Vargas, I., & Fernandes, H. (2025).  
Thermal Inspection Dataset for Defect Segmentation in CFRP Laminates.  
https://data.mendeley.com/datasets/jrsb4b9yy5

- Composite material: Carbon/PEEK (APC-2/AS4)
- Layup: [0₂/90₂]₆
- Specimen size: 100 × 100 mm
- Defect type: Kapton inserts simulating delaminations
- Defect sizes: 2×2 mm, 3×3 mm, 4×4 mm
- Depths: 0.13 mm, 0.26 mm, 0.39 mm
- Imaging method: Pulsed thermography
- Sensor: MWIR infrared camera (640 × 512, 55 Hz)

---

## Data Preprocessing

Performed in Google Colab:

- Extract dataset from Google Drive ZIP file
- Unzip `originalData.zip` and `annotatedData.zip`
- Flatten directory structure
- Remove system files (`._*`, `__MACOSX`)
- Match images and masks by filename
- Normalize pixel values to [0, 1]
- Resize images to 234 × 234
- Convert to PyTorch tensors

Final dataset size:
- 1034 image-mask pairs

---

## Model Architecture

U-Net segmentation model:

- Encoder-decoder structure
- Skip connections
- 3 downsampling + 3 upsampling stages
- Double convolution blocks (Conv → BatchNorm → ReLU)
- Output: 1-channel binary segmentation mask

---

## Loss Function

Combined loss:

- Binary Cross Entropy with Logits Loss (BCEWithLogitsLoss)
- Dice Loss (handles extreme class imbalance)

---

## Training Setup

- Train/validation split: 80/20
- Batch size: 8
- Optimizer: Adam
- Learning rate: 1e-4
- Epochs: 30
- Best model selected using validation loss

Checkpoint path:
```
/content/drive/MyDrive/spatial-temporal-defect-segmentation/best_unet.pth
```

---

## Evaluation Metrics

- Dice Coefficient
- Intersection over Union (IoU)
- Precision
- Recall

Metrics are computed on validation set using the best saved model.

---

## Results

- Dice: ~0.97
- IoU: ~0.95
- Precision: ~0.97
- Recall: ~0.97

Note: High scores are influenced by strong class imbalance in the dataset.

---

## Visualization

Outputs include:

- Input thermal image
- Ground truth mask
- Predicted segmentation mask

Used for qualitative validation of defect localization.

---

## Key Observations

- Strong class imbalance (very small defect regions)
- Dice loss improves sensitivity to small objects
- Validation loss used for model selection
- Model converges quickly due to dominant background class

---

## Citation

```bibtex
@dataset{garciafernandes2025cfrp,
  author = {Garcia Vargas, Iago and Fernandes, Henrique},
  title  = {Thermal Inspection Dataset for Defect Segmentation in CFRP Laminates},
  year   = {2025},
  publisher = {Mendeley Data},
  version = {V1},
  doi = {10.17632/jrsb4b9yy5.1},
  url = {https://data.mendeley.com/datasets/jrsb4b9yy5}
}
```
