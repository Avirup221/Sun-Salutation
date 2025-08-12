# Multimodal Hierarchical CNN for Sun Salutation Pose Classification

This project presents a deep learning pipeline for classifying yoga poses within the Sun Salutation (Surya Namaskar) sequence from video frames. The core of this work is a novel, multi-scale CNN architecture that processes both visual and numerical landmark data to achieve high-accuracy pose recognition.


---

## 📋 Project Overview

The goal of this project is to accurately classify the distinct asanas (poses) in the Sun Salutation sequence. This is achieved by moving beyond simple image classification and adopting a multimodal approach that fuses two data streams:

1.  **Visual Data:** The raw pixel information from video frames.
2.  **Numerical Data:** A 47-dimensional feature vector extracted using MediaPipe, containing joint angles, landmark visibility, and normalized distances.

The project explores several custom CNN architectures, including a `QuadtreeCNN` and an advanced `HierarchicalQuadtreeCNN`, and compares their performance against standard models like ResNet, VGG, and MobileNet.

---

## ✨ Features

* **Multimodal Fusion:** Combines image features with numerical pose data for enhanced accuracy.
* **Hierarchical Feature Extraction:** A custom `HierarchicalQuadtreeCNN` analyzes images at three spatial scales (global, quadrant, and sub-quadrant) to capture both holistic and fine-grained details.
* **Attention Mechanism:** An implementation of an attention gate that allows the model to learn and focus on the most relevant sub-regions of an image.
* **Comparative Analysis:** A full framework for training and evaluating multiple modern CNN architectures on the same dataset.
* **Explainable:** Integrated visualization tools like Grad-CAM to understand the model's decision-making process by highlighting important image regions.

---

## ⚙️ Methodology

The project follows a structured pipeline from data preprocessing to model evaluation:

1.  **Data Preprocessing:** Video frames are extracted and organized. For each frame, 47 numerical features are calculated using MediaPipe and saved alongside the image.
2.  **Model Development:** Several custom and standard CNN architectures are implemented. The key model, `HierarchicalQuadtreeCNN`, processes a `28x28` feature map at three levels of detail in parallel.
3.  **Training & Evaluation:** Models are trained using a custom dataloader that feeds both image and numerical tensors. The training process includes early stopping to prevent overfitting.
4.  **Visualization:** Grad-CAM is used to generate heatmaps, providing a visual explanation of which parts of a pose the model focuses on.

---

## 🚀 Models Implemented

* **`QuadtreeCNN`**: The original custom model that analyzes a feature map at a global scale and a quadrant scale.
* **`HierarchicalQuadtreeCNN`**: An advanced version that uses a three-level hierarchy (global, quadrant, sub-quadrant) for more detailed analysis.
* **`AttentionHierarchicalCNN`**: A modification of the hierarchical model that includes an attention gate to learn and focus on the most important sub-quadrants.
* **Standard CNNs**: A comparative study was performed using **ResNet18**, **VGG16**, and **MobileNetV2** adapted for our multimodal framework.

---

## 📈 Results

The custom hierarchical models performed exceptionally well, achieving **~97% validation accuracy**. The `HierarchicalQuadtreeCNN` demonstrated the effectiveness of multi-scale analysis, and Grad-CAM visualizations confirmed that the models learned to focus on relevant body parts to make their predictions.

---

## 🔮 Future Work

The next phase of this project is to move from static frame analysis to true sequential and video-based classification.

* **CNN+LSTM Model:** Implement a model where a CNN acts as a feature extractor for each frame in a sequence, and an **LSTM (Long Short-Term Memory)** network processes the sequence of features to understand the temporal dynamics and transitions between poses.
* **3D CNN Model:** Treat frame sequences as small video clips and use a **3D CNN** architecture. This will allow the model to learn spatiotemporal features (patterns in both space and time) directly from the video data, capturing motion itself as a key feature.
* **Error Analysis:** Conduct a deep dive into the model's misclassifications, using Grad-CAM on failure cases to understand their root cause and guide further model improvements.
