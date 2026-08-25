# Cancer Diagnosis — Binary Image Classification

Transfer-learning model that classifies histopathology image patches as **benign** or **malignant**. Built for a Computer Vision course assignment (The Hashemite University) using a provided Kaggle histology dataset.

## Dataset
10,879 image patches (50×50), imbalanced: 8,791 benign / 2,088 malignant. Split 80/20 train/test, with an additional 20% of train held out for validation. Class weighting applied during training to counter the imbalance.

## Model
- **Base:** MobileNetV2 (ImageNet weights, frozen)
- **Head:** GlobalAveragePooling2D → Dense(64, ReLU) → Dropout(0.3) → Dense(1, sigmoid)
- Data augmentation: rotation, horizontal/vertical flip
- Trained with Adam, binary cross-entropy, early stopping on val_loss (patience=7)

## Results (test set)
| Metric | Score |
|---|---|
| Accuracy | 83% |
| Sensitivity (Recall) | 80.4% |
| Specificity | 83.6% |
| Malignant F1 | 0.64 |
| Benign F1 | 0.89 |

Confusion matrix, ROC curve, and training curves are in the notebook.

## Usage
Open `cancer_classification.ipynb` in Jupyter/Kaggle/Colab. Dataset path is set for Kaggle (`/kaggle/input/cancer-binary-classes/...`) — update `BASE_PATH` if running elsewhere.

## Notes
Sensitivity/specificity were prioritized as the primary metrics, per the medical-diagnosis context of the assignment — false negatives (missed malignant cases) matter more than a raw accuracy number here.
