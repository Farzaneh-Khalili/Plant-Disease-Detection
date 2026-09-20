# Plant Disease Detection

An image classification project for detecting plant diseases using the **PlantVillage dataset**, CNN-based feature extraction, classical machine learning, and explainability techniques.

## Dataset

- **Dataset:** PlantVillage
- **Plant species:** 14
- **Classes:** 38
- **Image type:** RGB leaf images
- **Split:** 80% train / 10% validation / 10% test

The dataset is not included in this repository.

## Methods

The project was developed in two phases:

- **Phase 1:** Data preprocessing, augmentation, baseline CNN, and feature extraction.
- **Phase 2:** Classification using pretrained CNN features, explainability, and uncertainty analysis.

Pretrained **VGG16, ResNet50, and InceptionV3** models were explored for feature extraction. VGG16 FC6 features were used for the main classification experiments, producing **4096-dimensional feature vectors**.

The extracted features were classified using:

- **SVM (RBF kernel)**
- **KNN**

Several explainability techniques were also explored, including **Grad-CAM, SmoothGrad, Guided Backpropagation, and Guided Grad-CAM**. Monte Carlo Dropout was used to investigate prediction uncertainty.

## Results

| Approach     | Classifier | Test Accuracy |
| ------------ | ---------- | ------------: |
| VGG16 + FC6  | SVM (RBF)  |    **96.93%** |
| VGG16 + FC6  | KNN        |        89.58% |
| Baseline CNN | CNN        |           74% |

The **VGG16 FC6 + SVM** approach achieved the highest accuracy among the evaluated models.

## Project Structure

```text
Plant-Disease-Detection/
├── notebooks/
│   ├── preprocessing.ipynb
│   └── baseline-cnn.ipynb
├── reports/
│   ├── phase-1-report.pdf
│   └── phase-2-report.pdf
├── .gitignore
└── README.md
```

## Reports

Detailed methodology, experiments, results, explainability, and uncertainty analysis are available in the `reports/` directory.

## Authors

**Farzaneh Khalili**
**Hasti Javazadeh**
**Atefeh Peymani**
