# Plant Disease Detection

An image classification project for plant disease detection using the PlantVillage dataset, CNN-based feature extraction, classical machine learning classifiers, and explainability techniques.

## Project Overview

This project investigates image-based plant disease classification using the PlantVillage dataset, which contains images from 14 plant species across 38 classes.

The project was developed in two main phases:

- **Phase 1:** Dataset preprocessing, data augmentation, baseline CNN development, and preparation of CNN-based feature extraction pipelines.
- **Phase 2:** Classification using deep features extracted from VGG16 with SVM and KNN, together with model explainability and uncertainty analysis.

## Dataset

- **Dataset:** PlantVillage
- **Plant species:** 14
- **Classes:** 38
- **Data type:** RGB leaf images

The dataset is not included in this repository due to its size.

## Data Preprocessing

The preprocessing pipeline includes:

- Class distribution analysis
- Stratified train/validation/test splitting
- Image resizing to `224 × 224`
- Pixel normalization
- Data augmentation
- Class weight calculation

The dataset was divided into:

- **80%** training
- **10%** validation
- **10%** testing

A fixed random seed (`42`) was used for reproducibility.

### Data Augmentation

The training images were augmented using:

- Rotation up to 40°
- Width and height shifting
- Shearing
- Zooming
- Horizontal flipping
- Nearest-neighbor filling

## Baseline CNN

A simple convolutional neural network was implemented as a baseline model to validate the image preprocessing and classification pipeline.

### Architecture

```text
Conv2D (16 filters)
        ↓
MaxPooling
        ↓
Conv2D (32 filters)
        ↓
MaxPooling
        ↓
Flatten
        ↓
Dense (64)
        ↓
Dropout
        ↓
Softmax Classification
```

The baseline model was trained for a small number of epochs as an initial experiment.

## CNN Feature Extraction

Transfer learning was explored using pretrained CNN architectures:

- **VGG16**
- **ResNet50**
- **InceptionV3**

The networks were initialized with ImageNet pretrained weights and used as feature extractors.

For the main classification experiments, **VGG16** was used to extract deep features from the FC6 layer, producing a **4096-dimensional feature vector** for each image.

## Classical Machine Learning Classification

The extracted VGG16 features were classified using:

- **Support Vector Machine (SVM)** with an RBF kernel
- **K-Nearest Neighbors (KNN)**

## Results

The main classification results are:

| Approach     | Classifier | Test Accuracy |
| ------------ | ---------- | ------------: |
| VGG16 + FC6  | SVM (RBF)  |    **96.93%** |
| VGG16 + FC6  | KNN        |    **89.58%** |
| Baseline CNN | CNN        |       **74%** |

The combination of **VGG16 FC6 features and an RBF-kernel SVM** achieved the best performance among the evaluated approaches.

## Explainability and Uncertainty

Several techniques were explored to better understand model predictions and confidence:

### SmoothGrad

SmoothGrad was used to reduce noise in gradient-based saliency maps by averaging gradients obtained from multiple noisy versions of an input image.

### Monte Carlo Dropout

Monte Carlo Dropout was investigated for estimating predictive uncertainty through multiple stochastic forward passes with dropout enabled.

The analysis considered:

- Mean class probabilities
- Prediction variance
- Predictive entropy

### Grad-CAM

Grad-CAM was used to visualize the image regions contributing to model predictions.

The visualizations generally showed attention on leaf regions. However, some highlighted regions were broad and did not always correspond precisely to disease symptoms.

### Guided Backpropagation

Guided Backpropagation was used to visualize fine-grained input features such as edges, veins, and textures.

### Guided Grad-CAM

Guided Grad-CAM combined the localization information from Grad-CAM with the high-resolution visual information from Guided Backpropagation.

## Key Findings

- Deep features extracted from VGG16 were effective for plant disease classification.
- SVM substantially outperformed KNN when using the extracted VGG16 features.
- The VGG16 + FC6 + SVM approach achieved **96.93% test accuracy**.
- Explainability methods generally indicated that the model focused on leaf regions.
- Some visualizations suggested that the model may rely on broader characteristics such as color and texture rather than only disease-specific symptoms.
- Predictive uncertainty tended to increase for more difficult or incorrectly classified samples.

## Project Structure

```text
Plant-Disease-Detection/
│
├── notebooks/
│   ├── preprocessing.ipynb
│   └── baseline-cnn.ipynb
│
├── reports/
│   ├── phase-1-report.pdf
│   └── phase-2-report.pdf
│
├── .gitignore
└── README.md
```

## Reports

Detailed documentation of the project methodology, experiments, and analysis is available in the `reports/` directory.

- `phase-1-report.pdf` — Data preparation, CNN pipelines, feature extraction, and project infrastructure
- `phase-2-report.pdf` — Classification results, explainability, and uncertainty analysis

## Future Work

Potential directions for further development include:

- Fine-tuning pretrained CNN architectures
- Comparing additional CNN feature extractors
- Hyperparameter optimization for classical classifiers
- Improving model robustness through more diverse training data
- Integrating uncertainty estimates into the classification pipeline
- Further investigation of class-specific explainability
- Comparing additional machine learning classifiers

## Authors

- **Farzaneh Khalili**
- **Hasti Javazadeh**
- **Atefeh Peymani**
