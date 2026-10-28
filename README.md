# Evaluating Dataset Reliability and Real-World Feasibility in Machine Learning for Rare Skin Disease Classification

**MSc Artificial Intelligence Dissertation Project**  
**Heriot-Watt University, School of Mathematical and Computer Sciences**

**Author:** Rishav Ranjan  
**Supervisor:** Dr. Marta Vallejo

---

## Project Overview

Skin disease diagnosis relies heavily on visual assessment by clinicians, making rare dermatological conditions particularly challenging to research and diagnose. This project investigates a key question in applied medical AI:

> **Can a real-world, uncurated dermatology dataset support reliable skin disease classification, and what technical barriers prevent clinical-level performance?**

To explore this question, a multi-class skin disease classifier was developed using images sourced from the DermNet image library. The project focused on addressing class imbalance through preprocessing and augmentation techniques, comparing the performance of two transfer learning architectures (VGG16 and ResNet50), and deploying the best-performing model within an interactive Flask web application.

---

## Research Objectives

### Data Augmentation
Implement image augmentation techniques to increase the diversity and volume of training data for under-represented classes.

### Model Development
Investigate and train deep learning models suitable for medical image classification, specifically:

- VGG16
- ResNet50

### Optimisation and Deployment

- Perform hyperparameter tuning using Keras Tuner.
- Evaluate models using multiple classification metrics.
- Deploy the most suitable model through a Flask-based web interface.

---

## Dataset

### Source

**DermNet Image Library**

- Approximately 20,000 dermatology images
- 23 disease categories
- Variable image quality and resolutions
- No demographic metadata (age, gender, ethnicity)

### Selected Disease Classes

1. Actinic Keratosis, Basal Cell Carcinoma and Other Malignant Lesions
2. Warts, Molluscum and Other Viral Infections
3. Melanoma, Skin Cancer, Nevi and Moles
4. Atopic Dermatitis
5. Vasculitis

### Dataset Split

| Dataset | Images |
|----------|---------:|
| Training | 4,415 |
| Validation | 633 |
| Testing | 1,263 |
| **Total** | **6,311** |

**Split Ratio**

- Training: 70%
- Validation: 10%
- Testing: 20%

---

## Preprocessing Pipeline

### 1. Image Resizing

All images were standardised to:

```text
240 × 240 pixels
```

### 2. Contrast Enhancement

Contrast Limited Adaptive Histogram Equalization (CLAHE) was applied to improve local image contrast while limiting noise amplification.

### 3. Data Augmentation

Applied to minority classes to reduce class imbalance:

- Random rotation (up to 45°)
- Width shift (20%)
- Zoom (20%)
- Shear transformation (20%)
- Brightness adjustment (0.5x to 1.5x)
- Horizontal flip (50% probability)

---

## Model Training

### Environment

- Google Colab
- NVIDIA Tesla T4 GPU
- TensorFlow
- Keras

### Transfer Learning Models

#### VGG16
ImageNet-pretrained VGG16 architecture fine-tuned for multi-class classification.

#### ResNet50
ImageNet-pretrained ResNet50 architecture fine-tuned using the same dataset.

### Hyperparameters

| Parameter | Value |
|------------|--------|
| Learning Rate | 0.001 |
| Batch Size | 32 |
| Dense Units (VGG16) | 192 |

Hyperparameter optimisation was performed using **Keras Tuner Random Search** with early stopping.

---

## Results

### Performance Comparison

| Model | Accuracy | Precision | Recall | F1 Score | Specificity |
|---------|---------:|---------:|---------:|---------:|---------:|
| **VGG16 (Deployed Model)** | **54.71%** | **0.2102** | **0.2169** | **0.2017** | **0.8016** |
| ResNet50 | 35.78% | 0.1753 | 0.2137 | 0.1857 | 0.7995 |

---

## Key Findings

### Real-World Datasets Remain Challenging

Model performance demonstrated that real-world, uncurated dermatology datasets introduce significant challenges for automated classification systems.

### VGG16 Outperformed ResNet50

VGG16 consistently achieved superior performance across all evaluation metrics.

ResNet50 showed limited class discrimination and frequently collapsed predictions into dominant classes.

### Visual Similarity Between Diseases

Binary classification experiments revealed that visually similar diseases remain difficult to distinguish, particularly:

- Actinic Keratosis
- Warts and Molluscum

### Accuracy Alone Is Misleading

Because of dataset imbalance, accuracy did not adequately represent model quality.

Metrics such as:

- Precision
- Recall
- F1 Score
- Specificity

provided a more realistic assessment of real-world performance.

---

## Flask Web Application

A lightweight Flask application was developed to demonstrate model inference on user-uploaded images.

### Features

- Image upload interface
- Real-time skin disease prediction
- User-friendly frontend
- Local deployment

### Privacy-First Design

Uploaded images are:

- Processed entirely in memory
- Not stored on disk
- Deleted immediately after prediction

---

## Repository Structure

```text
.
├── app.py
├── VGG16_model.h5
├── VGG16_multiclass_model_training.ipynb
├── ResNet50_model_training.ipynb
├── skin_disease_augmented/
├── Sample images/
├── templates/
├── static/
└── requirements.txt
```

---

## Installation

### Clone Repository

```bash
git clone https://github.com/rishavranjan808/skin_disease.git
cd skin_disease
```

### Create Virtual Environment

#### Linux / macOS

```bash
python -m venv venv
source venv/bin/activate
```

#### Windows

```bash
venv\Scripts\activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Run Application

```bash
python app.py
```

Open:

```text
http://127.0.0.1:5000
```

and test predictions using images from the `Sample images` folder.

---

## Technologies Used

- Python
- TensorFlow
- Keras
- OpenCV
- CLAHE
- Transfer Learning
- Keras Tuner
- Flask
- NumPy
- Pandas
- Google Colab
- NVIDIA Tesla T4 GPU

---

## Limitations

- Low precision, recall, and F1-score indicate the model is not suitable for clinical deployment.
- Significant class imbalance remains despite augmentation.
- High visual similarity across disease categories affects classification performance.
- Dataset contains no demographic metadata, preventing analysis of demographic bias.
- Results were obtained from a single dataset and lack external validation.
- Developed solely as a research prototype.

---

## Resources

### Application Demonstration

🎥 **Video Walkthrough**  
https://youtu.be/Phx5LvqYRfM

### Dataset

📚 **DermNet Image Library**  
https://dermnetnz.org/image-library

---

## Ethics and Disclaimer

This project was developed for academic research purposes as part of an MSc Artificial Intelligence dissertation.

It is **not a medical diagnostic tool** and must not be used for clinical decision-making. Any medical concerns should always be evaluated by a qualified healthcare professional.

